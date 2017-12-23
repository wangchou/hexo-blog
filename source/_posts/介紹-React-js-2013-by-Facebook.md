---
title: 介紹 React.js (2013 by Facebook )
tags:
  - facebook
  - react
date: 2015-11-05 19:04:00
---

<div class="separator" style="clear: both; text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><iframe allowfullscreen="" class="YOUTUBE-iframe-video" data-thumbnail-src="https://i.ytimg.com/vi/XxVg_s8xAms/0.jpg" frameborder="0" height="266" src="https://www.youtube.com/embed/XxVg_s8xAms?feature=player_embedded" width="320"></iframe></span></div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Introduction to React.js by Tom Occhino and Jordan Walke</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">整個React.js的由來是很多Facebook內部對一個問題的討論。這個問題是 **<u>開發Javacript的應用時，它的結構應該是如何？&nbsp;</u>**( " How should we structure a javascript application? " )。特別是瀏覽器端的 Javascript 應用。前人透過各式各樣的 framework 提出一大堆的解答。這些 framework 通常試著去實踐 MVC, MVVM, MVW 各種概念。這些架構或 framework 共同點就是 M，也就是 Model... 基本就只是一種可觀察的物件 ( observable object )，然後這些可觀察的物件有一些Event API，讓你訂閱物件改變的通知 ( subscribe changes )。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">實際上發生的事 是開發者建立了這些雙向資料綁定 ( bi-directional data-binding )，讓你可以訂閱物件改變的通知。當某個東西改變了，你就可以變動 ( mutate ) / 更新你的 View。但這種觀察模式 ( observation pattern ) 實際上鼓勵 UI 的變動 ( mutation )。每次先把元件畫出來，然後當改變發生時，就試著更新之前畫出來的 UI 元件。這邊的關鍵字是變動 ( mutation )。**變動 ( mutation ) 是複雜的。**大概兩年半前，Facebook試著重寫聊天室。我們試著把事情變簡單，試著把開發者要處理的變異 ( mutation ) 減到最少。讓我來解釋一下那是什麼意思，下面是一個簡單應用的架構：</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>
<div class="separator" style="clear: both; text-align: center;">[<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">![](http://2.bp.blogspot.com/-PorkT6ZQGj0/VjsVKyXT1DI/AAAAAAAA35M/1-KLZL7tYfs/s400/Screen%2BShot%2B2015-11-05%2Bat%2B4.36.02%2BPM.jpg)</span>](http://2.bp.blogspot.com/-PorkT6ZQGj0/VjsVKyXT1DI/AAAAAAAA35M/1-KLZL7tYfs/s1600/Screen%2BShot%2B2015-11-05%2Bat%2B4.36.02%2BPM.jpg)</div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">要注意到的一件事是 在這個系統中的所有更新 ( updates ) 都會走一個單一的通道 ( go through a single channel )。它們都朝著單一方向流動，讓我們叫它 單向資料綁定 ( one directional data-binding )。所有輸入到這個系統的更新，不管是來自使用者輸入、即時的server updates或是起始的Loading。這些所有的更新都只透過單向的流動，不管怎樣最後都會流到 View 方格那裏。這一塊是所有前端工程師，我最關心的地方... 對嗎? 我關心使用者經驗、使用者真正看到和接觸的地方。**概念上來說，我們發現建造這一塊 / View 最簡單的方式就是避免變異 ( mutation )。**基本上是完全避免變異。我們發現，如果每次更新發生我們可以把整個&nbsp;**View 砍掉，整個重繪**，那會變得超簡單。因為這樣，**你只要寫怎麼把 View 畫出來就好，不用管 View 怎麼更新的程式碼。**</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">但這樣亂搞，可行嗎？</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">從瀏覽器的角度來看這一定會很慢，記憶體還會不夠之類的。但概念上來說 ( conceptually )，我們還是想要用這個Model。因為每次更新就重繪真的很方便，但前提是要速度可行和還是能給使用者好的經驗。我們提出來的解法就是React.js。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">React：一個為了建立使用者介面的Javascript程式庫。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">我們想要所有來自 **更新就重繪這理念** 好的部分，但避免其中壞的副作用 ( bad performance &amp; bad ux )。從此之後你不用管你的應用中從 state a -&gt; state b -&gt; state c，只剩下 零 -&gt; 畫出來。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">React 的核心是宣告元件 ( Declarative components )：</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">在任何時間點都只要描述你的元件長什麼樣子，這不只是一個樣板 ( template )，這不是呼叫一個函式然後回傳一段字串那種事。因為那樣的話，你要整個 DOM 砍掉，然後把新的 HTML 掛上去。元件實際上是可重複使用的 API，封裝了一大堆東西，像是 markup、這東西看起來怎樣、它的功能是什麼、它的行為、CSS、Javascript 和這些東西的結構是什麼，是這些全部的東西。對於使用者元件隱藏了實作的細節，讓我給你一個實例：</span>
<table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;">[<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">![](http://3.bp.blogspot.com/-IILmalknzQ4/VjsfYKsVFrI/AAAAAAAA35c/7SNGkiIPlWQ/s320/Screen%2BShot%2B2015-11-05%2Bat%2B5.20.09%2BPM.jpg)</span>](http://3.bp.blogspot.com/-IILmalknzQ4/VjsfYKsVFrI/AAAAAAAA35c/7SNGkiIPlWQ/s1600/Screen%2BShot%2B2015-11-05%2Bat%2B5.20.09%2BPM.jpg)</td></tr><tr><td class="tr-caption" style="text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">輸入元件：提供互動的 auto-complete search box，只要用跟原始 HTML &lt;input&gt; 一樣多的程式碼。然後我應該可以對她註冊事件、設定它的行為 ( behavior ) 有哪些。</span></td></tr></tbody></table><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">No explicit data binding：不像 AngularJS，React 不需要實際上 Wire 你的 View 到你的 Model，你只要說哪一個屬性 ( property ) 你的 Model 想要在你的 View 中使用，然後當 Model 改變時、你的 View 就會被更新。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">它是怎麼運作的? ( How does it work? ) 我們這邊說兩件事。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">1) 它一開始是如何畫出來的。 ( Initial Render )</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">2) 更新是如何發生的。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Initial Render：在 React 我們只找一個 render function，這個 render function 完美的地方是它一直能告訴你這元件在任何時間的樣子。你提供的這個 render function 不會回傳一個字串，它回傳的是你的 View 的表現 ( representation ) ，我們做的事是... 既然元件可以由其他元件組成 &nbsp;( composited by other components )，我們遞迴的呼叫render來建立UI架構。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Two Pass Rendering：</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">1\. 先建立 markup</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">2\. 在最上層用 Event Delegation 附加上事件處理器</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">因為步驟一，先把元件畫出來，我們可以做 Server-side Rendering。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">更新是如何發生的？</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">我們不稱這個動作為<strike>Update</strike>，我們叫它 一致 ( reconciliation )。它的目的是保持你的 UI 元件 新鮮、當資料變化時自動更新。每個人應該現在都感到懷疑，如果不懷疑你大概剛剛都在睡覺。但你應該記得剛剛說的 Initial Rendering function，任何時間點它要回傳一個元件的表現 ( representation )。當改變發生時，我們重新呼叫一次 Render，然後比較原來 Render 的結果和改變過後 Render的結果，計算出兩個時間點元件的差別 ( diff )。接著批次計算出最少的變動量，然後一次 把變動更新到 DOM Tree 上面。所以很快。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">---</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">12:20 開始 Show Code Sample 和 JSX 語法</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">&nbsp; &nbsp;程式碼還是看影片比較清楚... XD</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">26分開始大概一小時的Q &amp; A 還蠻精彩的~~~</span>