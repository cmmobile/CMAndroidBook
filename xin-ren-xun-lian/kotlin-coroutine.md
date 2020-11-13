# Kotlin-Coroutine

## Coroutine是什麼？

### 概念一

由兩個英文單字組成Cooperation + Routine，Cooperation意指合作，Routine意指例行作業，合在一起就是**合作式例行作業。**

> Routine：通常是方法、功能。

也就是說這些方法、功能會協同其他更多的方法、功能共同作業這件事情稱為Coroutine。

### 概念二

**又稱：可以中斷及繼續執行的函式呼叫**

這句話是在說，允許函式被暫停\(suspended\)執行之後再回復\(resumed\)執行，而暫停執行的函式，狀態允許被保留，復原後再以暫停時的狀態繼續執行．

![](../.gitbook/assets/1_mxsd2ch9qlnycfyht0eqrq.png)

根據上圖解釋，當main thread執行到function A並且需要等IO thread 耗時處理的結果，那我先暫停 function A，協調讓出main thread讓main thread先去執行其他的事情，等到IO thread的耗時處理結束後得到結果，再回復function A 繼續執行。

### 概念三

Coroutine通常是主動暫停\(suspended\)讓出執行權來實現協作，因此它的本質就是在討論程序控制流程的機制。

與執行緒最大的差異在於，以任務的角度來看，執行緒一旦開始執行就不會暫停，直到任務結束。整個過程是連續的。執行緒之間是搶佔式的調度，因此不存在協作問題。

