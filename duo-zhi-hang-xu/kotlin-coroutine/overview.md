# Overview

## 為什麼要使用

* 解決[Callback Hell](http://callbackhell.com/)，讓我們可以更直觀的閱讀。
* 在Android上切換Thread更加的方便，比起runOnUiThread、[Handler](http://givemepass-blog.logdown.com/posts/296606-how-to-use-a-handler)更加方便。
* 比起Thread更加輕量，在下一章會說明。

## 為什麼要切換Thread?

如果所有工作都在Main Threa執行會導致App的UI畫面卡頓、刷新頻率太低，影響使用者體驗。必須將這些跟UI沒有相關的工作，交給其他的執行緒處理，讓Main Thread專心處理UI的刷新，保持每隔16毫秒就可以更新一幀，也就是一秒可以刷60幀（遊戲常聽到的60fps）。

如果我們在Main Thread執行費時的工作或是API的請求，將會造成Main Thread被主塞，導致App被凍結。超過5秒，就會產生ANR\(Application Not Responding\)。

## Callback vs Coroutine

情境一：現在使用者要輸入帳號密碼登入我們的伺服器，最後會得到使用者相關數據。

### Callback

```kotlin
class LoginViewModel(){
    fun login(){
        //don't do this in prodcut code
        task1 = thread {
            respority.login(account, password, object: Callback<User> {
                fun onSuccess(user: User) {
                
                }
                fun onFailure(exceptione: Exception) {
                
                }
            })
        }
    }
    
    onCleared(){
        task1.cancel()
    }
}

class Respority {
    fun login(account: String, password: String, result: Callback<User>) {
        //do some connection
        if(task is successful) {
            result.onSuccess(user)
        } else {
            result.onFaliure(exception)
        }
    }
}
```

### Coroutine

```kotlin
sealed class Result<out R> {
    data class Success<out T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
}

class LoginViewModel(){
    fun login(){
        viewModelScope.launch(Dispatchers.IO) {
            val loginResult = login(account, password)
            if (loginResult is Result.Success<User>) {
            
            } else {
            
            }
        }
    }
}

class Respority {
    suspend fun login(account: String, password: String): Result<User> {
        //do some connection
        if(task is successful) {
            return Result.Success(user)
        } else {
            return Result.Error(exception)
        }
    }
}
```

讓我們來解構一下 `login` function:

* `viewModelScope` 是一個預先定義在`ViewModel`KTX擴展方法的`CoroutineScope` 。所有的Coroutines都必須在一個`CoroutineScope`內執行。一個`CoroutineScope` 管理一個或多個相關的Coroutines。
* `launch` 是一個創造Coroutine和分配方法的內容會在哪一個對應的Dispatchers執行的方法。
* `Dispatchers.IO` 決定這個Coroutine應該在I/O Thread被執行。

情境二：除了情境一，接下處理結果要在一個計算Thread，並且將使用者的Token取出。

### Callback

```kotlin
class LoginViewModel(){
    fun login(){
        //don't do this in prodcut code
        task1 = thread {
            respority.login(account, password, object: Callback<User> {
                fun onSuccess(user: User) {
                    handleResult(user, object: Callback<String> {
                        fun onSuccess(token: String) {
                            // save token
                        }
                        fun onFailure(exceptione: Exception) {}
                    })
                }
                fun onFailure(exceptione: Exception) {
                
                }
            })
        }
    }
    
    fun handleResult(user: User, callbak: Callback<String>) {
        //do some compute
        if(task is successful) {
            callbak.onSuccess(token)
        } else {
            callbak.onFaliure(exception)
        }
    }
    
    onCleared(){
        task1.cancel()
    }
}

class Respority {
    fun login(account: String, password: String, callbak: Callback<User>) {
        //do some connection
        if(task is successful) {
            callbak.onSuccess(user)
        } else {
            callbak.onFaliure(exception)
        }
    }
}
```

### Coroutine

我們暫時不管發生錯誤要怎麼處理，後面的章節會說明。

```kotlin
sealed class Result<out R> {
    data class Success<out T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
}

class LoginViewModel(){
    fun login(){
        viewModelScope.launch {
            val user = withContext(Dispatchers.IO) {
                login(account, password).getOrThrow()
            }
            val token = withContext(Dispatchers.Default) {
                handleResult(user).getOrThrow()
            }
            // save token
        }
    }
    
   suspend fun handleResult(user: User): Result<String> {
        //do some compute
        if(task is successful) {
            return Result.Success(token)
        } else {
            return Result.Error(exception)
        }
    }
}

class Respority {
    suspend fun login(account: String, password: String): Result<User> {
        //do some connection
        if(task is successful) {
            return Result.Success(user)
        } else {
            return Result.Error(exception)
        }
    }
}
```

當層級越來多會發現Callback的寫法會導致難以閱讀，這就是常說的Callbacke Hell。

如果改成Coroutine的寫法，就會發現輕鬆許多。

## 參考

[官方簡介](https://developer.android.com/kotlin/coroutines)

