# IDE

#### <mark style="background-color:orange;">**快捷鍵**</mark>

* **windows**

```
註解 (Ctrl + /)
複製至下一行 (Ctrl + D)
跳至定義 (Ctrl + B)
搜尋文字 (Ctrl + F)  
全域搜尋文字(Ctrl + Shift + F) 
全域搜尋檔案 (Shift + Shift)
自動排版(Ctrl + alt + L)
直接跳下一行(crtl+shift+enter) 
刪除多餘 import(ctrl +alt + o )
單字的頭尾(ctrl + 左右鍵)
左右頁籤(alt + 左右鍵)
關頁面(alt + F4)
休眠(windows+L)
放大(windows+"+")
縮小(windows+"-")
```

* **mac**

```
F3： Bookmarks
F3+Command(Win)：  檢視Bookmarks List
Command(Win)+O：  快速搜尋Class
Command+Shift+[：    左切Tab
Command+Shift+]：   右切Tab
Alt+上： 直接選股單字 
ctrl+option+T  (Win+Alt+T)： 一段Code 選取後可以快速用IF Else  或是 Try catch include起來
ctr+option+M  (Win+Alt+M)： 把一段code快速輸出成Function
```

#### <mark style="background-color:orange;">**Setting**</mark>

* inlay hints - 型別提示&#x20;
* livetemplate - 客製化模板&#x20;
* gradle - jdk版本

<mark style="background-color:orange;">**Plugins**</mark>

* adb // 模擬器相關動作執行&#x20;
* markdown (md)&#x20;
* Progress Bar// 就是build的時候比較療癒

<mark style="background-color:orange;">**Debug**</mark>

* #### Debug/Attach App <a href="#1-debugattach-app" id="1-debugattach-app"></a>

![](https://i.imgur.com/bbrbcZf.png)

– 點選圖中紅色圓圈圈起的左邊綠色按鈕，執行app的debug模式，快捷鍵Shift F9

– 點選圖中紅色圓圈圈起的右邊按鈕，可以選擇正在執行的程序attach debugger，第二種方法比較常用,我們可以在啟動apk之後,直接下斷點,然後attach process到制定程序,條件觸發之後就可以直接進入除錯模式。

* #### BreakPoint 斷點 <a href="#2-breakpoint" id="2-breakpoint"></a>

![鼠點選編輯框左側，出現紅色圓點/方點](https://i.imgur.com/nDBPJbI.png)

\-屬性斷點：打在類的成員變數上，當變數初始化或變數的值改變時觸發斷點。

\-方法斷點：打在一個函式的首行，進行函式級別的除錯。可以打在JDK的原碼裡，普通的斷點是不能打在原始碼裡。

* #### &#x20;Step Over/Into/Out <a href="#3-step-overintoout" id="3-step-overintoout"></a>

![從左到右依次](https://i.imgur.com/NlCXQXn.png)

Step Over 單步執行&#x20;

Step Into 進入正在執行的方法(必須是自定義的方法)&#x20;

Focus Step Into 可以進入原始碼&#x20;

Step Out 跳出正在執行的方法

* #### Debug Logger＋條件判斷 <a href="#1debuglogger-tiao-jian-pan-duan" id="1debuglogger-tiao-jian-pan-duan"></a>

透過DebugBreak Point 的Message Log功能 在原本要設定BreakPoint的地方，按下右鍵進行進階設定，可以看到有Evaluate and log

這樣的方式就可以印出Log也不會弄髒你的程式碼，但要注意的是，他不會出現在你原本的logcat中，而是出現在Debug Panel中，在Debug中點選 Console按下Contrl+F可以找到你的訊息

![在condition可以為中斷點設定中斷條件](https://i.imgur.com/sboGMVk.png)

![](https://i.imgur.com/PwiIwQO.png)

* [SVG 轉 Drawable](https://blog.csdn.net/xiao\_yuanjl/article/details/86677024)
