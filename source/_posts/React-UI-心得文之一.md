---
title: React UI 心得文之一
tags:
  - react
  - javascript
date: 2015-12-02 02:07:00
---

<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">這週在忙著刻一個大元件，中間有包兩三個中元件、然後中元件下面又會有小元件。要記得React 是負責 UI 的啊，千萬個不該在小元件裡面存 state。存了改了兩天還是會有問題，小元件如果存了狀態，常會有那大元件重 render 的時候，設 property 卻無法更新小元件，因為小元件的 state 不一樣了。兩天之後把大中小元件全部改成 dumb component 真的快樂的不得了，程式碼變少了、邏輯也清楚了。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">刻 React 元件的方法：</span></span>

1.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">盡量刻 Dumb Component，把它當成 function 去想要提供什麼參數</span>
2.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">parent component 要對 child componet 命名和設 handler(childId, value)</span>
3.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">事件發生時就呼叫 parent 傳來的 handler，說你是哪個 child和發生了什麼</span><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">就這樣遞迴做下去，最上層的 App component 就可以知道，哪第三個child component 的第四個 child component 發生了什麼事，然後做一些處理。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">客制化 React 元件外觀的方法：</span></div><div>

1.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">幫元件的各種 property 類別放置對應的className</span>
2.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用 webpack 的 css loader 幫元件建立 local 的 css scope，然後用一個 scss 檔去管理一個元件，這樣一切都會輕鬆的多。( 參考 React Toolbox )</span><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">其他刻外觀小心得：</span></div>

1.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">多用 em, rem</span>
2.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用 css 幫背景上色的方式，快速看物件是否對齊</span>
3.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用 Mac 的放大鏡 ( ctrl + 雙指滑動 trackpad )</span>
4.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用 css trick cursor 去引導 behavior</span>
5.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用 font-weight 和 color 的 alpha channel 去做細部微調</span><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">學各種 React 相關 Library的方法：一定要**<span style="font-size: x-large;"><u>從看完官方的 Tutorial/Guide 開始</u></span>**，網路上的介紹文章通常都挑簡單的地方說，十篇有九篇都講一樣的東西，還不如看官方的 Tutorial/Guide 把重要的東西有系統的一次學會。很重要所以特別粗體一下...</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">使用者經驗部分：</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">碰到客戶想要重新客製化系統的時候</span></div><div>

1.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">照他們舊有的行為，模擬跑自己刻的新系統幾次，很快就可以知道缺了什麼、哪裡會生出問題，這樣的方法比在那邊天馬行空的猜測會方便的很多。例子: 新報表系統拿舊系統的許多報表重新打一次。</span>
2.  <span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">用心智圖的方式窮舉可能的行為，不然光是用腦袋想一定會漏掉很多細節。</span><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">和他人合作的部分</span></div></div></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">一定要定時 Sync 進度，時常 commit。不要隱匿進度落後、缺失、維護 local state，想說這樣可以加班追回來。因為很多事從他人的角度來看會清楚的很多，也方便別人調整。不要裝弱、裝強，快放棄那沒用的自尊心吧。</span></div>
