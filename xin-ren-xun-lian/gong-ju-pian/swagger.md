# Swagger

### <mark style="color:orange;">Swagger簡介</mark>

swagger和postman有異曲同工之妙，不同的是，後端可以利用工具在創建服務的同時直接產出來swagger，並只需要在上方另外寫上文件說明，會快速很多&#x20;

我主要都是在查新附加資訊回傳值，因此會以新附加使用說明為主

* swagger服務例子: [自選股](https://outpost.cmoney.tw/CustomGroupService/swagger/index.html) [ForumOcean](https://outpost.cmoney.tw/forumocean/swagger/index.html) [新附加資訊](http://outpost.cmoney.net.tw/AdditionInformationRevisit\_v2/swagger/index.html)

### <mark style="color:orange;">新附加資訊介紹</mark>

#### <mark style="background-color:orange;">1. 服務位置</mark>

簡單來說就是為了要讓用戶使用體驗步卡卡或是打爆後端，每個專案都會區分各自屬於的domain，然後會分正式機和測試機，在實際接服務的時候要記得看一下有沒有寫對domain&#x20;

![](https://i.imgur.com/wVduqt1.png)

#### <mark style="background-color:orange;">2. 驗證資訊</mark>

公司幾乎所有服務都會需要帶驗證資訊

* 在一開始用postman打新版登入拿到token(要記得用測試環境拿token) ![](https://i.imgur.com/zPrzUBK.png)
*   開啟新附加，點擊authorize，value輸入

    > bearer 你自己的token //中間記得有空格

![](https://i.imgur.com/uiobFrc.png)

* 這樣你接下來json都不用輸入appid, guid, authtoken，帶空json就好

![](https://i.imgur.com/m2sOhje.png)

#### <mark style="background-color:orange;">3. 訊號頻道</mark>

這是針對Signal的服務的不同資料訊號，每個訊會回傳特定資料(有點像dtno報表號碼的概念)&#x20;

![](https://i.imgur.com/6i6QY5a.png)

#### <mark style="background-color:orange;">4. 使用介紹</mark>

![](https://i.imgur.com/B8qSNh1.png)

其實swagger裡面已經有部分教學可以參考，以下只會進行補充

*   <mark style="color:blue;">**取得此電腦的服務清單**</mark>

    就是讓你知道現在新附加有提供哪些服務，每一個type都會對應到一種服務 所以pm如果在寫需求文件的時候就是要寫上type，rd才會知道要接什麼 右上角按鈕點下去，貼上剛剛上面提到的驗證資訊，按execute，你就會看到一長串密密麻麻的東西

![](https://i.imgur.com/0gC6MXg.png)

我們最常用到的就是即時股價資訊(Stockcalculation)，寫websocket表示他有即時資料，api則代表平常一般的服務(就是打一次只會回你一次資料)，getTarget則是表示他可以進行個別的查詢&#x20;

![](https://i.imgur.com/c04Irma.png)

getAll就是會吐給你全部標的資訊

![](https://i.imgur.com/FK4Oajo.png)

*   <mark style="color:blue;">**資料類型說明**</mark>

    會告訴你這個type會回傳哪些類型的資料，操作方式跟上面一樣，只要多加一個typeName，有點像查字典的概念

    執行後你會看到下面有很多回傳資訊，columnName就是你要接資料的名字，type則是資料型態

![](https://i.imgur.com/NkaG8vN.png)

*   <mark style="color:blue;">**取全部資料GetAll**</mark>

    在取得此電腦的服務清單中如果有看到getAll，就可以用這個來查尋當前回傳資料 要填的內容跟之前一樣

#### - columns:按照資料類型說明回傳的columnName來放你想查的值，建議不要放太多因為全樣本加全部資料會超大包，有時候會跑不出來

![](https://i.imgur.com/ZP8PSWz.png)

#### &#x20;- 回傳值就會是\[標的,累計成交總額]

![](https://i.imgur.com/XEaSlvr.png)

*   <mark style="color:blue;">**GetTarget,GetMultiple,GetOtherQuery**</mark>

    就是按照服務清單時看到的資料，然後依照對應的需求欄位填上去這樣，這邊以GetMultiple舉例，MinuteInterval就是幾分k

    ```
    {
        "描述": "股票N分K",
        "目標載體": "Api",
        "route": "GetMultiple",
        "typeName": "CandlestickChartTick<StockCommodity,StockTick>",
        "keyNamePath": "Key",
        "驗證資料": {
          "appId": 6,
          "guid": "45f0b62e-a73d-4f03-9aa5-d69465608fd6",
          "authToken": "f681d630-d8bd-4360-85c4-dfa1dba5e7fe",
          "json": "{\"Commodity\":\"2330\",\"MinuteInterval\":5}"
            }
      }
    ```



![](https://i.imgur.com/6Nixph5.png)

<mark style="color:red;">**<<重要提醒>>**</mark><mark style="color:red;">N分K資料要取CandlestickChartTick\<xxx,xxx>這種type的</mark>

*   **篩選訊號Signal**

    就是id放上去用逗號分隔就好
