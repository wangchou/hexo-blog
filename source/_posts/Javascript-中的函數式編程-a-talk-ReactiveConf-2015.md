---
title: Javascript 中的函數式編程 (a talk @ ReactiveConf 2015)
tags:
  - functional programming
  - javascript
date: 2015-11-08 21:12:00
---

<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">影片：[Functional Programming in Javascript By Daniel Steigerwald](https://www.youtube.com/watch?v=BfzjuhX4wJ0&amp;feature=youtu.be&amp;t=2h16m7s)&nbsp;</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Daniel 是 google 前員工、也是 https://github.com/este/este 這個 React + Redux + immutable.js Starter Kit 的作者，在 Github 上有 1800 顆星。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">我認為函數式編程 ( Functional Programming ) 將在明年成為主流。像在 C++11 和 Java 8 中已經開始有 lambda function。我接下來聊我已經用在 Production 的東西。我認為函數式編程已經在前端的世界已經被 React 引入。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>**<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">什麼是函數式編程？</span>**
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">沒有什麼神秘的東西，到處都是純函式 ( Pure functions everywhere )、不可變的數值 ( Immutable values )、用組成而不用繼承 ( composition over inheritance )、紀錄代替類別 (records over classes)、處理好副作用 ( taming side-effects )。我覺得 functional programming 有點像是人工智慧，聽起來有點酷、有點奇怪，但當你了解了它以後，就只是無聊、很平常的寫程式而已。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">**為什麼要函數化 ( functional )？&nbsp;**</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">因為軟體正在吃掉這個世界，它必須要做到最好。函數式編程已經被證明，比較少臭蟲 ( less bugs)、較不複雜 ( less complexity )、程式碼更可讀 ( more readable code ) 和更好的效能 ( more performance )。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">**物件導向程式設計 ( OOP ) 有什麼問題？**</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">沒有問題，只是很難、常被誤用，而且有時是難以避免的。整個物件導向程式設計的模式 (paradigm) 是基於「送訊息給物件是唯一跟狀態 ( state ) 互動的方法」，因此狀態就會被分散。於是在分散式系統中狀態的一致的難度是跟世界和平一樣的 XD</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>
<table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;">[<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">![](http://2.bp.blogspot.com/-NqF8whIlX1E/Vj9BEosEl7I/AAAAAAAA35w/csXWLMH0e3w/s640/Screen%2BShot%2B2015-11-08%2Bat%2B8.32.45%2BPM.jpg)</span>](http://2.bp.blogspot.com/-NqF8whIlX1E/Vj9BEosEl7I/AAAAAAAA35w/csXWLMH0e3w/s1600/Screen%2BShot%2B2015-11-08%2Bat%2B8.32.45%2BPM.jpg)</td></tr><tr><td class="tr-caption" style="text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">物件導向程式設計 和 函數式編程的設計模式比較</span></td></tr></tbody></table><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Scott Wlaschin是很好的講者，不像我鼓勵大家去聽他的演講。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">在 OOP 中，每次方法在某個實體上被呼叫其實就是副作用。副作用很難被追蹤、被理解，沒有人喜歡驚喜。驚喜在生活中是好的，但驚喜在程式碼裡面沒有任何好的地方。我們被教導要用繼承，但他是陷阱，程式碼會不夠彈性、很難之後改變。設計模式最難的是如何幫這些模式取名字，動詞偽裝成名詞。策略、工廠、Commands...</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">React 中最耀眼的原則是函式組成法 ( function composition )。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>**<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">純函數 ( pure function ) vs 髒類別 (dirty class)</span>**
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">純函數沒有任何副作用。他很難去違反只負責一件事的原則 ( single responsibility principle) 因為純函數只有一個明顯的目的 --- 把輸入轉成輸出。所以測試就變得超簡單。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">類別是髒的。互叫一個簡單的類別函式，就會改變它。誰做的？為什麼做？我們永遠不知道 ( 直到我們 debug 後)...</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">推薦這本 github 上的書[適當的函數式編成指南](https://github.com/MostlyAdequate/mostly-adequate-guide)&nbsp;( 在 github 上有 6000 顆星)</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>
<table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;">[<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">![](http://4.bp.blogspot.com/-trYOXa5g8dY/Vj9HW1kBZYI/AAAAAAAA36A/XOIr5LVtpiI/s640/Screen%2BShot%2B2015-11-08%2Bat%2B8.59.38%2BPM.jpg)</span>](http://4.bp.blogspot.com/-trYOXa5g8dY/Vj9HW1kBZYI/AAAAAAAA36A/XOIr5LVtpiI/s1600/Screen%2BShot%2B2015-11-08%2Bat%2B8.59.38%2BPM.jpg)</td></tr><tr><td class="tr-caption" style="text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">如果你不理解這個程式，沒關係。我也不懂。在函數式編程裡它等於 ( (4 + 0) * 2) + (4 * 2)</span></td></tr></tbody></table><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">**Immutable.js**</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">不可變資料一旦被建立就不能被改變，這使得更簡單的應用程式開發，不用預防性的回傳複製品，更可以使用間單的邏輯來達到進階的 memoization 和改變偵測。一個針對不變資料的可變 API 並不改變原來資料，而是總是產生新的資料。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp; &nbsp;- 和 原生的 Javascript array 有很相似的 API</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp; &nbsp;- 保持永遠的不可變 (List, stack, map, orderedMap, Set, OrderedSet and Record)</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp; &nbsp;- 非常快</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">---</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">PS：作者講的不多，上面很多都是照投影片上大量文字打的。</span>
