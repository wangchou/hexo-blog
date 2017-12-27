---
title: 用 Redux 實踐「狀態機導向的介面開發」
tags:
  - redux
date: 2015-11-06 15:44:00
---

<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">BIG WORD ALERT!!!</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">———</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">研究了Redux.js之後，對State Machine有了更深的領悟。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">上個月解了一百多題 LeetCode，深深覺得程式解問題很重要的一點就是，想出一個「資料的表達的方式」讓問題運算過程中的所有「狀態」能夠清楚的表達，之後只要叫電腦從 Initial State 算到 Final State，題目就解完了。這個「資料表達的方式」也許是 stack、也許是 Array 再加上兩個 Pointer、也許是 2D Array表達地圖狀態、或複雜一點的像是 八皇后(N-queens) 問題用四個 array 來表達row, column, 兩個斜線方向有沒有皇后。只要想完「怎麼用資料來清楚表達所有狀態？」這個題目就解一半了，如果是 backtracking / 窮舉的問題的話，那你就已經解完了。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">不過，這個跟 Redux 有什麼關係呢？Redux做為Flux概念的實現，設計中 Store 是唯一的資料儲存中心，它把所有「元件狀態的資料」集中放在一起。</span><span style="font-family: '&quot;helvetica neue&quot;', '&quot;arial&quot;', '&quot;helvetica&quot;', sans-serif;">讓開發者很容易用</span><span style="font-family: 'helvetica neue', arial, helvetica, sans-serif;">抽離 UI 的角度思考，一開始就把應用程式中「0\. 怎麼用資料來清楚表達所有邏輯狀態？」這個問題給想清楚。這個問題解完了之後，剩下的只有兩件事：</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp;1\. 收到使用者 Action 或伺服器的更新，要從哪個 state 換到 哪個 state：應用程式的運作邏輯，這部分 Redux 用 Reducer 做掉了。在 Reducer 中你要清楚定義狀態機中的 Transition 也就是 ( previousState, Action ) =&gt; newState 這件事</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp;2\. 在每個state的時候，應用程式 / 元件要畫成什麼樣子：React 想解的問題</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">0 和 1 兩個步驟常常會平行設計、互相影響，這部分會定義你的產品功能面。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">2 的步驟就是視覺化、資料傳達的部分。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">—</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">總結，從State Machine的角度來開發只要做下面三件事：</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><span class="Apple-tab-span" style="white-space: pre;"> </span>1\. 想好怎麼表達 state。 ( Redux Store )</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><span class="Apple-tab-span" style="white-space: pre;"> </span>2\. 想好有哪些事件，事件會讓 state 間怎麼切換。 ( Redux Reducer )</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><span class="Apple-tab-span" style="white-space: pre;"> </span>3\. 如何把狀態傳達給使用者。 ( React )</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">從此開發就有了 SOP。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">PS: 「資料的表達方式」包含了「資料結構」和裡面結構中資料代表的意義。</span>
