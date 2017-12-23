---
title: 'Be predictable, not correct. by Pete Hunt (from Instagram)'
tags:
  - functional programming
  - react
  - state machine
date: 2015-11-04 20:27:00
---

<div class="separator" style="clear: both; text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><iframe allowfullscreen="" class="YOUTUBE-iframe-video" data-thumbnail-src="https://i.ytimg.com/vi/e7A6EUe3XGM/0.jpg" frameborder="0" height="266" src="https://www.youtube.com/embed/e7A6EUe3XGM?feature=player_embedded" width="320"></iframe></span></div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Pete Hunt from Instagram Web Team.</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>**<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">What makes UI hard?</span>**
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">最難的是管理所有使用者的狀態 ( state )，更可怕的是隨時間改變的狀態。然後 Unit Test 不能完全測試 UI 的所有情況 ( 太多例外 )、靜態分析 ( JSLint / JSHint ) 也不行。因為這樣的複雜度，我不曾試著讓 UI 完全正確。我只是試著讓 UI 變得可預測。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Two silver bullet:</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">1\. Composition: 讓簡單的 function 組合成更大的 function。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">2\. Idempotence: 讓每次同樣的 Input 得到同樣的 Output。不變性 ( Immutability ) 的資料結構讓我免費得到 Idempotence。努力讓 mutable state 的數量越少越少，mutable state只有一個owner。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">React.js 讓工程師照著上面的兩個規則。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">React 是 宣告式的 ( declarative ) JQuery。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">**
****React**</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp;&gt; Data 輸入 =&gt; virtual DOM 輸出。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp;&gt; 當資料改變的時候，就整個重繪，所以少掉很多 State。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>**<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Demo Example (從15- 分)</span>**
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Demo on jsfiddle.net jsbin.com</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">一直在看Code</span>