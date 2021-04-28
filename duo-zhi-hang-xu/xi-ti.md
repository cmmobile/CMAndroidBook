---
description: 依照順序完成習題，千萬不要直接跳到二。
---

# 習題

### 習題一

嘗試完成[Use Coroutines in your Android App](https://developer.android.com/codelabs/kotlin-coroutines#0)\(請忽略第6, 9, 10,12步驟\)

### 習題二

目前有四道API要發送，分別為[API-1](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/company_first_name.json)、[API-2](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/company_detail.json)、[API-3](https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/api_test_one.json)、[API-4](%20https://raw.githubusercontent.com/cmmobile/AndroidApiFakeResponse/master/api_test_two.json)。其中API-1、API-3、API-4會同時執行，當API-1、API-3、API-4執行完畢後，才會執行API-2。

API-2的參數，會依照API-1、API-3、API-4的結果依照順序組合而成。例如：

拿著被組合的結果，來執行API-2。

合併來組出參數結果來執行，取得最後的答案。

以上以Coroutines實作，答案要顯示在螢幕上或Console。

