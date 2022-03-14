# Firebase

以下提供最最最初步的使用教學，手把手教你使用Firebase最重要功能。&#x20;

RD要執行Firebase的引入及程式碼才會實現功能，[請參考](https://firebase.google.com/docs/android/setup)

### <mark style="background-color:orange;">1.推播</mark>

<mark style="color:blue;">**1-1一般推播**</mark>

* 打開[Firebase](https://firebase.google.com)，左上方點選對應專案（沒看到就是沒有權限要請PO開）&#x20;

![](https://i.imgur.com/iDKDccX.png)

* 設定標題及內文，點擊下一步

![](https://i.imgur.com/RuoSOT8.png)

* 點擊"指定其他應用程式"，選擇指定推播的平台(通常雙平台都會選)，選完後會出現在藍色框框，點下一步

![](https://i.imgur.com/sH80fmQ.png)

* 輸入排定的時間，點審查，就完成啦，是不是很簡單 p.s.審查一旦點下去，就會按照排定時間直接送出喔! 可以先儲存草稿

![](https://i.imgur.com/Q6oepsK.png)

![](https://i.imgur.com/iDKDccX.png)

<mark style="color:blue;">**1-2跳轉網頁推播**</mark>

* 前面步驟一樣，不一樣的地方在於要設定其他選項設定一些參數，範本如下&#x20;

![](https://i.imgur.com/gYMTay6.png)

* 公司對於這些參數的名稱都有定規範，請參考[規範](https://docs.google.com/spreadsheets/d/1n-qPQY5NHNJsd\_DIIpUmbbN3KOK41vhLS18EROvzZ\_0/edit#gid=1804919660)
* 主要參數說明

> commonTargetType設定成4為跳轉網頁
>
> commonParameter裡面要用json格式放入跳轉的網址 {"webUrl":"http://www.cmoney.tw/"}

<mark style="color:blue;">**1-3預先測試**</mark>

不知道大家在新增通知時有沒有發現右邊有一個測試通知，究竟那是幹嘛用的呢？ 其實就是跟字面上一樣可以給我們測試用的，在這個通知還沒發建立完之前我們可以先在測試機或虛擬機上測試

* 點擊測試通知，他會要求你要輸入FCM憑證，那這憑證是從哪裏拿呢？點選連結會有對應的教學&#x20;
* 依照指示在在專案中加入程式碼，就會log出來，再將長長的一串憑證貼上去即可&#x20;

![](https://i.imgur.com/EP2rbHN.png)

![](https://i.imgur.com/kslRxKv.png)

<mark style="color:blue;">**1-4深度連結推播**</mark>

* 依樣去設定其他選項的參數

![](https://i.imgur.com/tAFAAxw.png)

* 主要參數說明

> targetType依照每個專案自己定義的targetType參數來決定行為，以全方位來說targetType為1的時候要設定深度連結畫面
>
> paramete要用json字串格式放入依照各專案的深度連結參數 ex: {"linkType":7} json字串格式產出請參考[連結](https://docs.google.com/spreadsheets/d/1lPhM\_rnFIbTyxBU1ZlckhN\_HewEyHJv0jWfyknDXOdw/edit#gid=1843281444)

### <mark style="background-color:orange;">2. 深度連結</mark>

簡單來說就是可以透過PM設定的參數告訴我們打開APP時要跳到哪一個畫面

* 到dynamic links頁面，點擊新增動態連結

![](https://i.imgur.com/BjVm4Zz.png)

* 系統自動幫你建立一個短連結網址，點下一步

![](https://i.imgur.com/OjxUh2I.png)

* 將要跳轉畫面的參數用JSON格式寫在深層連結網址，並為這個深度連結命名 `？以前得網址是預設網址，實際參數會看？以後的`&#x20;

![](https://i.imgur.com/G7ycpVX.png)

* 分別設定iOS及Android上指定的應用程式

![](https://i.imgur.com/qJ2PhRR.png)

* 最後點選儲存就完成了，等工程師將深度連結對應參數設定好，只要點選這個短連結就可以到指定的頁面

### <mark style="background-color:orange;">3. Remote Config</mark>

*   **用途:**

    可以藉由建立參數即條件，即時去更改app上的接收到的資料和行為，像是可以設定app彈窗廣告文案內容，或是app強制更新等狀態，也可以將試用金鑰用此功能設定，只樣以後要改參數就只需要更動網站參數，不用動到app&#x20;

![](https://i.imgur.com/ocsEHdp.png)

有兩種設定方式：

<mark style="color:blue;">**3-1. 一個參數名稱搭配json字串**</mark>

![](https://i.imgur.com/onUWkAD.png)

> 優點: 工程師只需要跟firebase要一次資料，再將json裡的字串截去需要的資料，可以減少跟firebase取資料可能失敗的機會
>
> * PM要學習JSON字串建立

&#x20;

![](https://i.imgur.com/o5xjHnb.png)

＜做法＞

* 先點擊新增參數，並輸入參數名稱和內容（參數名稱要用英文，然後盡量好好設定，工程師會依照設定的參數名稱去抓資料內容），內容就是將要傳送的資料用JSON格式字串表示
* 可以點擊左下方新增說明，將參數內容表示的意義放在上面方便其他人理解（可設可不設）
* 如果有需要這個參數只有某些版本(condition，下面會提到)可以接收到的話，點擊又上方的新增條件值，並輸入在那個條件裡要放什麼參數

<mark style="color:blue;">**3-2. 一個資料夾裡面有多個參數，每個參數只有一個值**</mark>

![](https://i.imgur.com/Vm5Chja.png)

> 優點: PM可以很快設定
>
> 缺點: 工程師需要跟firebase要很多次資料

＜做法＞

* 重複上面新增參數的方式，新增多個需要的參數，就是新增完一個參數之後再按新增參數，重複Ｎ次 ![](https://i.imgur.com/GcLJ4Yp.png)
*   將要群組起來的參數左邊框框打勾勾，點上方遷移至群組，新建群組，按儲存，大功告成！ ![](https://i.imgur.com/BybirQc.png)

    ![](https://i.imgur.com/vSbJVMF.png)

### <mark style="background-color:orange;">4. condition設定</mark>

還記得前面有說可以設定條件值限定特定版本接收資料，但在新增條件值之前，首先要先設定condition -> 白話文就是你要跟firebase說你的哪幾個版本是在哪一個條件

* **點擊condition，進到畫面就會看到已經有４個條件（release,develop,maintain,update）**

他會依照你排列的順序（順序可以調等等再教），從上面往下面走，直到符合那個條件裡的規則就會停在那個狀態，如果你在那個條件裡沒有設定任何規則，就是表示任何版本都可以接受

以下圖為例，3.0.8版本就會進develop，3.0.0-3.0.9就會進到release(不包含3.0.8)，剩下版本就會進到update； 但在5/23 02:00後到 08:15前這段時間，所有版本都會進maintain

![](https://i.imgur.com/hoQDumV.png)

* **如何設定條件規則**

大部分狀況下我們都會是以版本號(app:gradle的versionName)來區分，可以用兩種方式設定

**1. 點擊要設定的條件方框會出現以下畫面，選擇應用程式和想要規範的版本**

![](https://i.imgur.com/YhjG6J9.png)

* 版本可以多選

![](https://i.imgur.com/D2XpUYk.png)

* 但不想點多個的話，也可以用正規表達式表述（網路上很多教學），在搜尋框裡輸入表達式來新建，這裡表示接受3.0.0-3.0.9的版本

![](https://i.imgur.com/tGwLuKg.png)

* 選好後按儲存但不表示就好了喔!還要點擊右上方的發布變更才會生效&#x20;

![](https://i.imgur.com/y0Yf971.png)

* 點擊左邊的六筒(?)就可以調整條件的順序

![](https://i.imgur.com/NuoYpPd.png)

### <mark style="background-color:orange;">5. remoteConfig模組內已經有預設的remoteConfig，建新專案時記得要建上去</mark>

[模組連結](http://192.168.10.147:10080/CG\_Mobile/CG\_Module\_Android/remoteconfig\_android\_sample)

* **appStatus參數 ：當前APP狀態，停機時就是這個參數控制的**

![](https://i.imgur.com/SrbG7n9.png)

* **statusAnnouncement參數 ：如果維修或強制更新時要彈出的彈窗內文**

![](https://i.imgur.com/GNigrIe.png)

* **ApiConfig群組 ：API的Domain**

參數:vipServerPushUrl / vipServerUrl / serverPushUrl / serverUrl

> domain主要就這兩種 https://www.cmoney.tw/ https://mobile.cmoney.tw/

![](https://i.imgur.com/VmkL8Fi.png)

* **RealTimeConfig群組 ：websocket的Domain**

參數:vipRealtimeWebSocketUrl / realtimeWebSocketUrl ![](https://i.imgur.com/MErVxgD.png)

### <mark style="background-color:orange;">6. 當停機維運，APP要怎麼關閉還有公告怎麼設定？？</mark>

學會以上的小技能後，停機維運設定就難不倒你啦！！

* 首先要在maintain上建立停機的時間，並移到最上面
* 在remoteConfig的statusAnnouncement參數裡針對停機維護設定相關的內文
* 當然也別忘了在停機的前一兩天要發送推播先溫馨提醒用戶以免用戶森七七喔

當然前提是工程師要在app裡面有接好remoteConfig模組和推播模組而且都有做了對應的設定，否則奇蹟不會發生

### <mark style="background-color:orange;">7. Crashlytics</mark>

簡單說一下，左邊的Crashlytics顧名思義就是可以看到app的閃退率狀況，只要RD有在程式碼裡面做相關引入設定，就可以在這裡看到資料，並且依照篩選器選擇版本機型即解決狀態，右邊可以選擇時間，建議固定時間可以記錄下來，因為資料有保存期限（目前看起來是只保留近4個月的資料） 另外建議RD每天可以上來看一下目前閃退的問題並及時修正。 ![](https://i.imgur.com/dgp3YyS.png)

### <mark style="background-color:orange;">8. 事件埋點查詢</mark>

為了追蹤使用者在app中的使用狀態，PM會定義一些參數讓RD在程式碼中建立紀錄，幾乎都是用Firebase或Flurry這兩種方式埋點

以Firebase來說，可以在events裡看到埋點的資料，並可以藉由上方的篩選器來篩選你想要的條件 ![](https://i.imgur.com/pXiOOuv.png)

### <mark style="background-color:orange;">9. App Distribution</mark>

方便讓pm測試的小工具，就是包一版APK檔之後丟上去，在測試群組內加入測試人員的email

未來你只要丟一版上來，群組內的人就會接到即時的email通知，滿方便的！！\




以上 大家下次見～！
