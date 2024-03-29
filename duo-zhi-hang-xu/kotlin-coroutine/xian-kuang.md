---
description: 探討背後的原理
---

# Suspend修飾符

## 創建Coroutine

簡單創建一個Coroutine

```kotlin
 val suspendFunction = suspend {
        println("In Coroutine")
        5
    }.createCoroutine(object : Continuation<Int>{
        override val context: CoroutineContext
            get() = EmptyCoroutineContext

        override fun resumeWith(result: Result<Int>) {
            println("Coroutine End: ${result.getOrThrow()}")
        }

    })
```

以下為createCoroutine的宣告，這個Coroutine並不會馬上執行。

```kotlin
public fun <T> (suspend () -> T).createCoroutine(
    completion: Continuation<T>
): Continuation<Unit>
```

* suspend \(\) -&gt; T是一個Function Type，createCoroutine是suspend \(\) -&gt; T的Extension Function。
* 參數completion會在執行Coroutine完成後執行，也就是說完成Callback。
* 回傳值是一個Continuation物件，由於現在只是被創建出來，之後會使用這個回傳值來觸發Coroutine的啟動。

Continuation是一個介面，如果不管Context，作用有點像是使用Callback。

```kotlin
public interface Continuation<in T> {
    public val context: CoroutineContext

    public fun resumeWith(result: Result<T>)
}
```

## 啟動Coroutine

在上面我們已經知道怎麼創建Coroutine了，接下來要怎麼啟動一個Coroutine呢？

回想一下之前提到的概念，Coroutine是一個**中斷及繼續執行的函式呼叫**，允許函式被暫停\(suspended\)執行之後再回復\(resumed\)執行。

目前我們正在suspend的狀態，接下來只要resume就會開始執行。

```kotlin
suspendFunction.resumeWith(Result.success(Unit))
```

 有人會問resume\(\)和resumeWithException\(\)是什麼？它們是Continuation的Extension Function，裡面只是簡單的呼叫resumeWith\(Result\)。

以下為啟動後結果

```kotlin
In Coroutine
Coroutine End: 5
```

有了以上的基本概念，接下來看一下Complier幫我們做了什麼。

[https://medium.com/androiddevelopers/the-suspend-modifier-under-the-hood-b7ce46af624f](https://medium.com/androiddevelopers/the-suspend-modifier-under-the-hood-b7ce46af624f)

