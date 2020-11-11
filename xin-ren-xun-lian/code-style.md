# Coding Style

### 前言

Android Coding Style 包含以下

* Java Coding Style 
* Kotlin Coding Style
* Android各種命名規則
* Android 需要遵守的規則

這邊程式碼範例會以Kotlin的語法來做說明，由於Java與Kotlin的CodingStyle規則基本上相同。所以，只有當Java 部分需要特別解釋時，才會補上Java範例。

PS.Kotlin在Android平台上會轉譯成Java，如果有會Java但不懂Kotlin的，可以在Android Studio工具列上點擊 Tools -&gt; Kotlin -&gt; Show Kotlin ByteCode ， 在Kotlin ByteCode上點擊 Decompile 就會顯示Java版本的程式碼

### 命名

* 程式碼除了註解與字串外，不得使用中文字
  * UnitTest或AndroidTest的方法名稱可以使用中文以方便辨識功能
* 禁用region
* 所有 MagicNumber 一律宣告 常數 或 變數 或 enum\(列舉\) 或 seal class\(for kotlin\)，禁止直接在程式碼內使用

Don't

```java
for(int i = 0; i < 10; i++) {
    ...
}
```

Do

```java
final int MAX_COUNT = 10;
for(int i = 0; i < MAX_COUNT; i++) {
    ...
}
```

* 所有要對外的欄位:
  * Java一律使用屬性的方式，禁止直接使用 public 變數公開
  * Kotlin直接使用變數\(\)。沒有必要公開的屬性就不該公開    
* 禁用無大刮號單行else \(DanglingElse\)
* 你不該交出 Compile 後有一堆警告的程式碼，更不該交出有 Error 的程式碼
* Java變數使用小駝峰命名，private變數不需要m開頭
* kotlin變數使用小駝峰命名
* 常數成員一律 全大寫配底線分隔 =&gt; VERSION\_NUMBER
* 在命名時，請不要自己縮寫單字來命名，能用的縮寫只有大家常用的縮寫。

  例如：`ResponseMessage` 縮寫成 `RspMsg`

  上面的`Message` 縮寫成`Msg`，大多數人都還看得懂。但是將`Responses`縮寫成`Rsp`，如果不看原本的樣子，基本上是沒辦法看懂的，所以如果要用縮寫，只有像是`Msg`這樣大家都可以懂的縮寫可以用，不然請好好的把原本的單字寫出來。

  另外，使用縮寫時大小寫不照原縮寫，應使用大寫開頭+小寫的方式，即使是像`iOS`這樣，大多數人習慣第一個`i`小寫的，也請這樣寫`IosVersionSetting`，而不是`iOSVersionSetting`。

以下針對不同地方的命名做詳細規則的說明

**檔案的命名**

* 檔案名以大駝峰式命名。例如：NumberExtension.kt,NumberExt.kt
* 檔案名稱與類別同名

  正確寫法：

  ```kotlin
    // 檔名：MyClass.kt
    class MyClass {
    }
  ```

  錯誤寫法：

  ```kotlin
    // 檔名：MyClass.kt
    class OtherClass {
    }
  ```

* 原則上一個檔案中只有一個主要類別 例外:非泛用類別可以直接寫在類別裡面

  正確寫法：

  ```kotlin
  // 檔名：FirstClass.kt
  class FirstClass {
  }
  ```

  ```kotlin
  // 檔名：SecondClass.kt
  class SecondClass {
  }
  ```

  錯誤寫法：

  ```kotlin
  // 檔名：FirstClass.kt
  class FirstClass {
  }
  class SecondeClass {
  }
  ```

* 擴充方法檔案命名
  * 檔名以擴充的物件命名加上Extension、Ext為後綴。例如：NumberExtension.kt,NumberExt.kt
  * 檔案名以大駝峰式命名。例如：NumberExtension.kt,NumberExt.kt,NumberUtils.kt
* 工具類方法檔案命名
  * 檔名以目標功能命名加上Helper、Utils為後綴，例如:ChartCalculateHelper.kt, DateTimeFormatUtils.kt
  * 檔名以大駝峰式命名

**類別的命名**

* 大寫駝峰式命名

  正確寫法：

  ```kotlin
    class Setting {
    }
  ```

  錯誤寫法：

  ```kotlin
    class setting {
    }
  ```

* 名詞 或 形容詞+名詞

  正確寫法：

  ```kotlin
    class NestedStucture {
    }
  ```

  錯誤寫法：

  ```kotlin
    class CalculateStock {
    }
  ```

* 類別繼承Android原生類別時在名稱尾部加上原生類別的名稱，需要寫的有Application,Activity,Fragment,Service,Adapter,ViewHolder。

  正確寫法：

  ```kotlin
    class ArticleViewHolder(cell: ConstraintLayout) : RecyclerView.ViewHolder(cell)  {
        ...
    }
  ```

  錯誤寫法：

  ```kotlin
    class ArticleCell(cell: ConstraintLayout) : RecyclerView.ViewHolder(cell) {
        ...
    }
  ```

**方法的命名**

* 使用小駝峰命名
* 使用 動詞\(load, fetch, preLoad, ...\) 或 動詞+名詞\(getData, fetchFileList, ...\) 作為命名

  ```kotlin
    fun loadData(){
        ...
    }
  ```

* 方法參數或區域變數的命名 ，參數或區域變數用小寫開頭變數名\(小駝峰命名\)

  ```kotlin
    fun getFundList(token: String, pushToken: String){
        ...    
    }
  ```

* 有Boolean回傳值時的命名，以is, can, has 或xxxable為結尾，例如：isOpened , canRead, hasValue, visiable

  ```kotlin
    fun isFinish : Boolean{
        return false
    }
  ```

* 如果方法的參數，無法用一行表達時，須將參數個別單獨為一行。

  ```kotlin
    fun joinToString(
        separator: CharSequence,
        prefix: CharSequence,
        postfix: CharSequence): String {
        // …
    }
  ```

  如果只有一行可使用以下兩種方式

  ```kotlin
    fun sayHello(): String {
        return "Hello"
    }
  ```

  只有Kotlin可以寫成一行

  ```kotlin
    fun sayHello(): String = "Hello"
  ```

* 如果callBack方法以Lambda寫法

  Lambda傳遞的參數放在第一行

  ```kotlin
    setOnclickListener { prop ->
        val propertyValue = prop.get(obj)
    }
  ```

**Package name 的命名**

* 全部小寫

**Resource 的命名**

全小寫  
規則：以畫面使用的位置＋功能 來命名，例如以下

* activity\_xxx.xml
* fragment\_xxx.xml
* item\_xxx.xml
* layout\_xxx.xml
* dialog\_xxx.xml
* shape\_xxx.xml
* selector\_xxx.xml
* .....

例外: 模組因Gradle合併資源可能會與專案衝突，所以命名要加prefix

舉例:

社團模組之發文頁Layout

* community\_layout\_activity\_newpost

自選股模組之編輯自選股頁Layout

* customgroup\_layout\_activity\_editcustomgroup

**View Id的命名**

規則：功能＋使用元件 來命名，例如以下

* login\_textView
* reply\_us\_editText
* xxx\_textView
* xxx\_editText
* xxx\_button
* xxx\_linearLayout\(constraintLayout,..\)
* ...

### 修飾詞

* 可見性修飾詞
  * Kotlin 可見性修飾詞 private、 protected、 internal 和 public ，預設可見性是 public。
  * Java 可見性修飾詞 private、package-private、 protected 和 public，預設可見性是 package-private。[參考連結](https://openhome.cc/Gossip/JavaEssence/PackageAndModifier.html)
* 順序

  ```kotlin
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

  ```java
    public protected private 
    abstract default 
    static final 
    transient volatile 
    synchronized native strictfp
  ```

### 型別

對於Kotlin基礎型別有疑惑的，可以去[這邊](https://www.kotlincn.net/docs/reference/)尋找答案，這邊只寫需要注意的部分。Java的往[這邊](http://www.codedata.com.tw/book/java-basic/index.php)。

* [實質型別與參考型別的差別](http://tianchyi1955.pixnet.net/blog/post/101762587-4-----%E8%B3%87%E6%96%99%E7%9A%84%E5%AF%A6%E5%80%BC%E5%9E%8B%E5%88%A5%E5%8F%8A%E5%8F%83%E8%80%83%E5%9E%8B%E5%88%A5)
* 注意boxing與unboxing的成本，[相關連結](https://github.com/JustinSDK/JavaSE6Tutorial/blob/master/docs/CH04.md)

#### 轉型

* 數值向下轉型會有遺失資料的風險

**安全轉型 vs 不安全轉型**

* 安全轉型方式
  * kotlin

    ```kotlin
    安全
    class Car {
    }

    class Taxi extends Car {
    }

    val tempCar: Car = Car()

    val tempTaxi: Taxi? = tempCar as? Taxi

    if (tempTaxi == null) {
      return
    }
    ```

    ```kotlin
    不安全
    val tempTaxi: Taxi = Taxi()

    val tempCar: Car = tempTaxi as Car // 轉型成功

    if(tempCar is Car) {
        tempCar.xxx()
    }
    ```

  * java

    ```java
    安全
    class Car {
    }

    class Taxi extends Car {
    }

    Car tempCar = new Taxi();

    if (tempCar instanceof Taxi)) {
      Taxi tempTaxi = (Taxi)tempCar;
      do something..
    }
    ```

    ```java
    不安全
    class Car {
    }

    class Taxi extends Car {
    }

    Car tempCar = new Taxi();

    Taxi tempTaxi = (Taxi)tempCar;
    do something..
    ```

#### 字串

* 字串的不變性請參考[這裡](https://blog.csdn.net/u012830807/article/details/17068091)
* 不要什麼東西都存字串，成本很重。
* 有需要迴圈來組字串時只能使用StringBuilder
* 除了需要在迴圈裡組字串情況外，都使用+號或StringTemplate，使用+號是因為在編譯時會把+轉成StringBuilder來實現，所以不必擔心記憶體使用問題，而且使用+能使可讀性與可維護性提升

  ```kotlin
  // StringTemplate範例
  val s = "abc"
  println("$s.length is ${s.length}")
  ```

* 三個以上參數時不要用String.format，會造成可讀性與維護性下降

  ```kotlin
  don't
  String.format("first:%d second:%d third:%d",a,b,c)
  ```

* 字串轉型態 可以直接 `"String".toIntOrNull()`、`"String".toDoubleOrNull()`....
* 比較字串可以直接用 `"FirstString" == "SecondString"` 的寫法 ，Kotlin有幫你做好了。如果需要忽略大小寫可以這樣寫 `"FirstString".equals("SecondString",true)`
* 請使用 `string.IsNullOrEmpty()` 來檢查 null or 空字串，而非 `str == null` 或 `str == ""`

Java 特別注意的部分：

* [Java String Concatenation: Which Way Is Best?](https://redfin.engineering/java-string-concatenation-which-way-is-best-8f590a7d22a8)
* 比較字串請不要用以下的寫法 ，這是比較物件是否相等

  ```java
  if( "originalString" == "compareString" )
  ```

  正確寫法為

  ```java
  if( "originalString".equals("compareString") )
  ```

  或

  ```java
  if( "originalString".compareTo("compareString") == 0 )
  ```

#### Nullable與NonNullable

Kotlin的型別皆可以Nullable，因此在使用上有幾項要注意的地方

* 非必要不將型別、屬性及欄位設為Nullable型態
* 非必要不使用`!!`\(斷定NonNullable\)，因為這樣就拋棄了Kotlin自動安全檢查null的優勢

  * 若是在一定要用到值的時候則可以使用`!!` or `requireNotNull`，以確保流程正確，但是如此做需要做例外處理，不可直接使APP崩潰
  * 範例: LiveData已經設定為Boolean，但是方法因為是從Java編譯，所以還是可能為Null，故可以使用`!!`or`requireNotNull`進行取值

  ```kotlin
  val isLoading: LiveData<Boolean> = MutableLiveData<Boolean>(false)
  val state = isLoading.value!!
  ```

* 使用`?.`及`?:`處理Null狀態

### 註解

註解可以記下開發流程和緣由和思緒流程，特殊的邏輯一定要寫註解。 註解要和程式碼一起維護，不要留下過時的註解。

* 單行註解

  可用 `/* ... */` 或 `// ...` 。

  ```java
    // End-Of-Line Comments
    /* Single-Line Comments */
  ```

* 區塊註解

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

* Javadoc

  置於 Class 宣告、Method 宣告、Field 宣告或 Property 宣告之前。  
   必須要寫 Javadoc 的有 public class 以及所有的 public 或 protected 成員 \(member\) 。

  * 使用`/** ... */`註解，其子行的起始必需有`*`，而該星號需對齊上一行的 `*`。

```text
 /**  
   * Multiple lines of Javadoc text are written here, 
   * wrapped normally... 
   */
   public int method(String p1) { 
       ... 
   }
```

```text
    如果只有單行可以縮成

    ```java
    /** An especially short bit of Javadoc. */
    ```

- 不用寫 Javadoc 的例外

    - 在子物中覆寫 (override) 父類別的方法不一定要寫上 Javadoc，若執行邏輯中有不易理解的(若不清楚可以徵詢其他人CodeReview)則需要寫上註解。
    - 有些「簡單、明確」的方法也不一定要寫上 Javadoc，像是 `getFoo` 這種簡明的案例，好像除了寫上「返回 foo 值」也什麼好寫的。但如果對於一般人來說並不能馬上知道 **Foo** 是什麼意思，那就要寫 Javadoc。

- 方法的回傳
```

* TODO

  善用 IDE 的 TODO 功能，對那些臨時的、短期的解決方案，或已經夠好但仍不完美的程式碼使用 `TODO` 或 `FIXME` 註解。 `TODO` 是總稱， `FIXME` 是細分。 用 `FIXME` 來表示存在問題或優先度較高的 `TODO` 事項（可選）

  ```java
    // TODO: 2019/2/14 待重構

    // FIXME: 2019/2/14 有未知的狀況會Crash
  ```

* 註解程式碼

  請不要註解程式碼，不如直接拿掉。 若真的有需要，一律使用`// ...`。

### 擴充方法

* 放置位置：放在$root/extension的資料夾底下

### 例外處理

* 不要忽略例外

  **Don't**

  ```kotlin
    fun setServerPort(value : String) {
        try {
            serverPort = value.toInt()
        } catch (e : NumberFormatException) { 

        }
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

* 不要嵌套 try catch ，會造成可讀性與維護性下降，請把需要try-catch的地方包成一個方法，並把Exception丟出

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

### 附錄

### 參考網站

* [https://kotlinlang.org/docs/reference/](https://kotlinlang.org/docs/reference/)
* [https://www.kotlincn.net/docs/reference/](https://www.kotlincn.net/docs/reference/)
* [https://blog.csdn.net/u012830807/article/details/17068091](https://blog.csdn.net/u012830807/article/details/17068091)

