# Flurry

[flurry 連結](https://login.flurry.com/home?continue=https%3A%2F%2Fauth.flurry.com%2Fauth%2Fv1%2Fauthorize%3Fresponse\_type%3Dtoken%26client\_id%3Dflurry\_ngdp\_unified%26grant\_type%3Dimplicit%26state%3D260491%26redirect\_uri%3Dhttps%253A%252F%252Fdev.flurry.com%252Fmetrics%252F1)

帳號: 公司email 密碼: 可以和核心確認一下

記得請PO幫你開專案的權限

### 1. Flurry埋點

有模組可以埋，iOS，怎麼埋可以去gitLab看，埋點的用途就是要研究用戶行為及留存率等等:

* 指南針Explorer - 針對個別的app進行埋點數據的分析
  * Funnels和UserPath比較像，都是作行為的分析
  * Journey比較像是針對個別用戶的使用狀況觀察
  * Measure可以根據想比較參數進行數據分析,ex: 過去幾個月下載年齡層及男女比例 詳細使用可以參考[這個連結](https://medium.com/@a4728tw/flurry-explore%E5%B7%A5%E5%85%B7%E6%95%99%E5%AD%B8-f0a31be38f37)
* 圖表Analytics - 觀察新用戶及留存率

### 2. User Property

「User Property」是拿來對於各項事件指標做分群檢視用的，比較適用於長期不會頻繁變動的特性，例如：訂閱／非訂閱 Flurry本身已經有內建 ![](https://i.imgur.com/kI2ZWok.png)

如果要額外建製也可以客製化建立自己的User Property，最多500個。

[使用參考連結](https://developer.yahoo.com/flurry/docs/analytics/userproperties/?guccounter=1#swift)
