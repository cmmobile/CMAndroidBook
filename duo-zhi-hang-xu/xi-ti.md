---
description: 依照順序完成習題，千萬不要直接跳到二。
---

# 習題

### 習題一

嘗試完成[Use Coroutines in your Android App](https://developer.android.com/codelabs/kotlin-coroutines#0)\(請忽略第6, 9, 10,12步驟\)

### 習題二

目前有四種API要發送，分別為[UserName](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/company_first_name.json)、[Company](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/company_name.json)、[Guid](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/guid.json)、Detail。其中UseName、Company、Guid要同時執行，當這三道API執行完畢後，才會執行Detail。

Detail的API會依照UserName、Company、Guid的結果依照順序組合而成，  
請以三道API回傳內容取代{}，來多次執行Detail API請求\(預計共要執行五次喔\)。

API模板：https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/{UserName}\_{Company}\_{Guid}.json

實際案例：  
[https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/Chasity\_EXOTECHNO\_01fe1948-4210-4082-9235-5051d3cdeb96.json](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/Chasity_EXOTECHNO_01fe1948-4210-4082-9235-5051d3cdeb96.json)

以上以Coroutines實作。

請輸出每一次API請求的URL及Response，  
並於每個請求輸出間間隔一行，  
答案要顯示在螢幕上或Console，  
以下為輸出Console輸出範例

```text
RequestUrl: https://...
Response: { ... }

RequestUrl: https://...
Response: [ ... ]
```

