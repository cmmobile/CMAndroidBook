# Postman

Postman就是一個可以讓你知道一到服務他到底回傳什麼資料的工具 如果很想知道到底是幹嘛的可以參考[這篇](https://www.wrpypl.com/postman.html) 這裡只會針對公司的使用情境來教學

### 事前準備

* 事前請先下載[postman](https://www.postman.com/downloads/)

![](https://i.imgur.com/9WM7McZ.png)

* 看到空空如也的畫面表示成功

![](https://i.imgur.com/nPATeyM.png)

### <mark style="color:orange;">起步走  ---＞</mark>

#### <mark style="background-color:orange;">1. Gitlab上面有一個PostmanTest的</mark>[<mark style="background-color:orange;">檔案</mark>](http://192.168.10.147/CG\_Tool/PostmanTest)<mark style="background-color:orange;"></mark>

* 從上面下載下來並解壓縮(順帶一個很好用的[解壓縮工具](https://www.developershome.com/7-zip/))

![](https://i.imgur.com/6GcOgdk.png)

* 解壓縮後會看到以下資料夾

![](https://i.imgur.com/m3eTpfn.png)

#### <mark style="background-color:orange;">2. 開啟postman建立workspaces</mark>

* 建立一個workspaces&#x20;

![](https://i.imgur.com/9yx3e5w.png)

* 點下去

![](https://i.imgur.com/VtEoG8m.png)

* 建立完成

![](https://i.imgur.com/79yR9Uy.png)

#### <mark style="background-color:orange;">3. 用postman import剛剛下載的檔案</mark>

* 點import匯入

![](https://i.imgur.com/l9EJaI9.png)

* 記得選folder資料夾

![](https://i.imgur.com/dtBBbqL.png)

* 把剛剛解壓縮檔案的資料夾整包丟進來

![](https://i.imgur.com/kGS411r.png)

* 匯入後就會看到左邊劈哩啪啦出現一堆資料夾，這樣就表示你成功了&#x20;

![](https://i.imgur.com/qeDpStS.png)

#### <mark style="background-color:orange;">4. 選環境(正式機或測試機)+jwt登入</mark>

**補充：常常聽到正式測試環境，意思其實就是後端在完成一個服務的時候通常會先放在測式的domain上，當測試完成後，他們才會放到正式的domain上面，讓正式產品可以使用。**

* 右上方眼睛的左邊請選擇"第一組-正式機\_93"

![](https://i.imgur.com/53xHCCo.png)

* 點一下眼睛，會看到"第一組-正式機\_93"裡的相關預設資訊 可以把它改成你自己已經有註冊過的CMoney帳密，好處是不容易被踢掉（別人如果也登入這個帳號你的驗證資料會失效） 如果你想打的服務是針對各個作者的，appId也記得要改一下

![](https://i.imgur.com/1jCzkrW.png)

* 公司大多的服務都需要驗證資訊，因此打你想要的服務之前，請先打登入服務(現在都走jwt新版登入方式)，登入後驗證資訊會自動幫你帶到你剛剛選的環境設定參數裡面 左邊點選 \[服務組-通用]簡易登入(authToken & jwt)->新版登入(設定access\_token) 右邊點send&#x20;

![](https://i.imgur.com/oYsUw3V.png)

#### <mark style="background-color:orange;">5. 打服務(恭喜你，終於走到最後一哩路)</mark>

* 找到想要查的服務並做send，這裡以即時盤後服務7-2為例子，下面就會跑出回傳的資料了&#x20;

![](https://i.imgur.com/Lw5TTxL.png)

**補充1: dtno服務測試**

*   可以直接找即時盤後服務9(不用登入拿驗證就可以直接打這道服務了) 輸入對應的參數資訊，filterNo不知道是多少就填0



![](https://i.imgur.com/h9F4SZc.png)

**補充2: 盡量不要用polling**

* polling其實就是短時間一直去打同一道api，因為時間夠短所以可以一直拿到新的資料，達到即時資料的效果，但這樣其實會對後端造成比較重的負擔 可以先問問看服務有沒有新附加有提供相關資料的服務
