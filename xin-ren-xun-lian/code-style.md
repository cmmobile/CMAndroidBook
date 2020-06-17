# Code Style

## 命名

* 少用縮寫 

正確：

```kotlin
class ResponseMessage {
}
```

錯誤：

```kotlin
class RspMsg {
}
```

* 使用縮寫時大小寫不照原縮寫，應使用大寫開頭+小寫 

正確：

```kotlin
class IosVersionSetting {
}
```

錯誤：

```kotlin
class iOSVersionSetting {
}
```

## 檔案

* 與類別同名 

正確：

```kotlin
// MyClass.kt
class MyClass {
}
```

錯誤：

```kotlin
// MyClass.kt
class OtherClass {
}
```

* 原則上一個檔案中只有一個主要類別

 正確：

```kotlin
// FirstClass.kt
class FirstClass {
}
```

```kotlin
// SecondClass.kt
class SecondClass {
}
```

錯誤：

```kotlin
// FirstClass.kt
class FirstClass {
}
class SecondeClass {
}
```

## 類別

* 大寫駝峰式命名
* 名詞 或 形容詞+名詞
* 繼承的Android類別放在名稱尾部

 正確：

```kotlin
class Setting {
}

class NestedStucture {
}

class MainActivity : AppCompatActivity() {
}

class ArticleViewHolder(cell: ConstraintLayout) : RecyclerView.ViewHolder(cell) {
}
```

錯誤：

```kotlin
class setting {
}

class CalculateStock {
}

class Main : AppCompatActivity() {
}

class ArticleCell(cell: ConstraintLayout) : RecyclerView.ViewHolder(cell) {
}
```

## Package Name

* 全部小寫

## 註解 \(Comment\)

註解可以記下開發流程和緣由和思緒流程，特殊的邏輯一定要寫註解。 註解要和程式碼一起維護，不要留下過時的註解。

#### 單行註解

可用 `/* ... */` 或 `// ...` 。

```java
// End-Of-Line Comments
/* Single-Line Comments */
```

#### 區塊註解

註解區塊的縮排，和其接連的程式碼同一層級。可用 `/* ... */` 或 `// ...` 。若是這種註解風格`/* ... */`有多行時，其子行的起始必需有`*`，而該星號需對齊上一行的 `*`。

```java
/*
 * This is
 * okay.
 */
```

```java
// And so
// is this.
```

```java
/* Or you can
 * even do this. */
```

#### Javadoc

置於 Class 宣告、Method 宣告、Field 宣告或 Property 宣告之前。 必須要寫 Javadoc 的有 public class 以及所有的 public 或 protected 成員 \(member\) 。 1. 使用`/** ... */`註解，其子行的起始必需有`*`，而該星號需對齊上一行的 `*`。

```java
    /**  
     * Multiple lines of Javadoc text are written here, 
     * wrapped normally... 
     */
     public int method(String p1) { ... }
```

```text
如果只有單行可以縮成

```java
/** An especially short bit of Javadoc. */
```
```

1. 不用寫 Javadoc 的例外
   * 在子物中覆寫 \(override\) 父類別的方法不一定要寫上 Javadoc。
   * 有些「簡單、明確」的方法也不一定要寫上 Javadoc，像是 `getFoo` 這種簡明的案例，好像除了寫上「返回 foo 值」也什麼好寫的。但如果對於一般人來說並不能馬上知道 **Foo** 是什麼意思，那就要寫 Javadoc。

#### TODO

善用 IDE 的 TODO 功能，對那些臨時的、短期的解決方案，或已經夠好但仍不完美的程式碼使用 `TODO` 或 `FIXME` 註解。 `TODO` 是總稱， `FIXME` 是細分。 用 `FIXME` 來表示存在問題或優先度較高的 `TODO` 事項（可選）

```java
// TODO: 2019/2/14 待重構
// FIXME: 2019/2/14 有未知的狀況會Crash
```

#### 註解程式碼

盡可能不要註解程式碼，不如直接拿掉。 若真的有需要，一律使用`// ...`。

## 例外處理

#### 不要忽略例外

**Don't**

```kotlin
fun setServerPort(value : String) {
    try {
        serverPort = value.toInt()
    } catch (e : NumberFormatException) { }
}
```

* 如果沒有要處理，就不要 catch，只在可以處理的地方 catch。
* 不要直接 catch 最上層的 Exception 或 Throwable

**Don't**

```kotlin
  catch (e1 : Exception) {
  }
```

* Finally 區塊裡面只用來作資源回收或清理資料結構的工作，或使用 Try-with-resources 來自動處理資源回收。

  ```kotlin
    resource = acquireResource()
    try {
        useResource(resource)
    } finally {
        releaseResource(resource)
    }
  ```

  或是

  ```kotlin
    val writer = FileWriter("test.txt")
    writer.use {
        writer.write("something")
    }
  ```

* 不要嵌套 try catch ，會造成可讀性與維護性下降，可接受包成一個方法

**Don't**

```kotlin
  try {
      ...
      try {
          ... 
      } catch (e2 : WhateverException) {  
          // Exception Message  
        }  
  } catch (e1 : FooException) {  
      // Exception Message  
  }
```

**Do**

```kotlin
  try {
      ...
      throwExceptionMethod()
  } catch (e1 : FooException) {  
      // Exception Message  
  } catch (e2 : WhateverException) {  
      // Exception Message  
  }
```

## 型別

#### 基礎型別

* 注意boxing與unboxing的成本

#### **Booleans**

* 只有`true`及`false`兩種
* 可進行`&&`/`||`/`!`操作

#### **Numbers**

* Double: 64 bit
* Float: 32 bit
* Long: 64 bit
* Int: 32 bit
* Short: 16 bit
* Byte: 8 bit
* 善用`.MAX_VALUE`/`.MIN_VALUE`/`.NaN`/`.POSITIVE_INFINITY`/`.NEGATIVE_INFINITY`表達特殊狀態

#### **Characters and Strings**

* `'a'`單引號表示Char，`"string"`雙引號表示字串

#### **Arrays**

* 使用`[]`進行get和set
* 使用`arrayOf()`方法建立實體
* Kotlin中Array的T是不可變的，因此不能將`Array<Int>`直接轉為`Array<Any>`
* 除了`Array`，另有`ArrayList`/`List`/`Set`/`Map`/`HashMap`/`Dictionary`...等類型，及對應的`Mutable`系列

#### Nullable與NonNullable

* 明確區分該型別是否可為Null
* 非必要不將型別、屬性及欄位設為Nullable型態
* 不濫用`!!`
* 善用`?.`及`?:`處理Null狀態

## 建構子

* 所有類別必須包含至少一個建構子
* 可多載
* 初始化可寫在`init {}`區塊，或直接寫成屬性的初始化宣告

  ```kotlin
  class MyClass(name: String) {
      val firstProperty = name
      val secondProperty: String
      val thirdProperty = "Third"

      init {
          secondProperty = name
      }
  }
  ```

  亦可簡化成

  ```kotlin
  class MyClass(val firstProperty: String, val secondProperty: String, val thirdProperty) {

  }
  ```

* 可將建構子設為私有

  ```kotlin
  class MyClass private constructor() {

  }
  ```

#### 繼承

* 最基礎的class是`Any`
* 類別中宣告的屬性及方法需設為`open`才可在繼承後進行覆寫
* 避免在自定義的BaseClass的建構子或初始化時使用標記為`open`的屬性及方法
* 使用`abstract`及`interface`使繼承的類別強制要求實作對應方法
* Kotlin中沒有static關鍵字，真的需要可使用`companion object`

#### 列舉

* [列舉](https://kotlinlang.org/docs/reference/enum-classes.html)

#### 其他型別

* [Nested Class](https://kotlinlang.org/docs/reference/nested-classes.html)
* [Inner Class](https://kotlinlang.org/docs/reference/inline-classes.html)

#### Delegate

* [Delegate](https://kotlinlang.org/docs/reference/delegation.html)
* [Delegated Properties](https://kotlinlang.org/docs/reference/delegated-properties.html)

## 字串

* [字串的不變性](https://blog.csdn.net/u012830807/article/details/17068091)
* 不要什麼東西都存字串。
* 一般情況使用+號或StringTemplate
* 有迴圈只能使用StringBuilder
* 多個參數時少用String.format，會造成可讀性與維護性下降
* 字串轉型態 可以直接 `"String".toInt()`、`"String".toDouble()`....
* 比較字串可以直接用 `"FirstString" == "SecondString"` 的寫法 ，Kotlin有幫你做好了。如果需要忽略大小寫可以這樣寫 `"FirstString".equals("SecondString",true)`
* 請使用 `string.IsNullOrEmpty()` 來檢查 null or 空字串，而非 `str == null` 或 `str == ""`

## 方法

#### 命名

使用 動詞\(load, fetch, preLoad, ...\) 或 動詞+名詞\(getData, fetchFileList, ...\) 作為命名

```text
fun loadData(){
    ...
}
```

#### 參數的命名\(簽名\)

參數 或 區域變數 用小寫開頭變數名\(小駝峰命名\)

```text
fun getFundList(token: String, pushToken: String){
    ...    
}
```

#### 有Boolean回傳值時的命名

以is, can, has 或xxxable為結尾，例如：isOpened , canRead, hasValue, visiable

```text
fun isFinish : Boolean{
    return false
}
```

#### 表達方式

如果方法的的參數，無法用一行表達時，須將參數個別單獨為一行。

```text
fun <T> Iterable<T>.joinToString(
    separator: CharSequence = ",",
    prefix: CharSequence = "",
    postfix: CharSequence = ""
): String {
    // …
}
```

如果只有一行可使用以下兩種方式

```text
fun sayHello(): String {
    return "Hello"
}
```

```text
fun sayHello(): String = "Hello"
```

## 修飾詞順序

```text
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation
companion
inline
infix
operator
data
```

## Lambda

Lambda傳遞的參數放在第一行

```text
setOnclickListener { prop ->
    val propertyValue = prop.get(obj)
}
```

## 繼承方法\(extension function\)

#### 放置位置

放在$root/extension的資料夾底下

#### 檔案命名

* 檔名以擴充的物件命名加上Extension或Ext為後綴。例如：NumberExtension.kt,NumberExt.kt
* 檔案名以大駝峰式命名。例如：NumberExtension.kt,NumberExt.kt

```text
NumberExtension.kt

fun Number.dpToPx() = ...
fun Number.spToPx() = ...
```

## 轉型

#### 實質型別\(數字\)或字串

Every number type supports the following conversions:

* `toByte(): Byte`
* `toShort(): Short`
* `toInt(): Int`
* `toLong(): Long`
* `toFloat(): Float`
* `toDouble(): Double`
* `toChar(): Char`
* 字串有Nullable EX: `toDoubleOrNull()` 的轉型方法 \*

#### 實質\(數字\)轉型

數值向小型別轉型會有遺失資料的風險， 如果要如此操作， 請確認並不影響結果， 且是必要的

#### 參考\(物件\)轉型

要被繼承的物件需要open且要滿足建構式

```text
open class Car() {
    val gas
}

class Taxi(): Car() {
    val money
}
```

#### 不安全轉型

範例一

```text
val tempTaxi: Taxi = Taxi()

val tempCar: Car = tempTaxi as Car // 轉型成功
```

範例二

```text
val tempCar: Car = Car()

val tempTaxi: Taxi = tempCar() as Taxi // Throw Exception
```

#### 安全轉型

範例一

```text
val tempCar: Car = Car()

val tempTaxi: Taxi? = tempCar as? Taxi

if (tempTaxi == null) {
    return
}
...
```

範例二 經實際測試，大多數內建實質型別以及字串在程式碼編寫時，若Int is Double會直接跳Error提醒

```text
val tempCar: Car = Car()

if (tempCar !is Taxi) {
    return
}
val tempTaxi: Taxi = tempCar as Taxi
```

