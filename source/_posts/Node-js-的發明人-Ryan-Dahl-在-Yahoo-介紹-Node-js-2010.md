---
title: Node.js 的發明人 Ryan Dahl 在 Yahoo 介紹 Node.js (2010)
tags:
  - node
  - yahoo
date: 2015-11-03 23:04:00
---

<div class="separator" style="clear: both; text-align: center;"><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;"><iframe allowfullscreen="" class="YOUTUBE-iframe-video" data-thumbnail-src="https://i.ytimg.com/vi/M-sc73Y-zQA/0.jpg" frameborder="0" height="266" src="https://www.youtube.com/embed/M-sc73Y-zQA?feature=player_embedded" width="320"></iframe></span></div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Node.js主要專注在Performance。Node的特點是對I/O有特別的處理方式，特別快。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">在有100個client下，每次回應1MB的Benchmark</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">node &nbsp;822 reqs/secs</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">nginx 7xx reqs/secs</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">others &nbsp;1x reqs/secs</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">node用javascript寫，但居然跑的比純C寫的nginx還要快!!! nginx快的原因是它不用一個Process來接處理一個 client，而是用Event Loop。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">All about non-blocking I/O</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">non-blocking I/O: &nbsp; L1 / L2 / L3/Memory &lt; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 250 cycles</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">blocking I/O: &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;disk / network &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &gt; 41,000,000 cycles (ex: select .. from database)</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">應該用不同的方式來處理這兩種I/O，他們從根本上根本不一樣。L1 cache像是拉開抽屜拿東西，存取memory像是到樓下買個東西回來，但從硬碟上拿東西像是跳上飛機、飛到地球的另一邊再飛回來一樣。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">要用non-blocking I/O，就要全部的API Call都用non-blocking I/O，即時用了第三方的程式庫去存取資料庫，可能就變成blocking I/O了。要實現的方法有幾種，event loop、using callback function。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">database_query("select ...", &nbsp;callback function); //應該這樣做</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">但是大部份的語言都不預設這種寫程式的方式，如果要達成這種功能，通常要花很大的心力，最後大部份程式員最多就做到多個執行緒，然用用一個執行緒去處理一個I/O Operation。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">但Javascript是個特別的例外，因為這語言從第一天就一直在處理瀏覽器的Event Loop，**callback function、anonymous function、Closure&nbsp;**是在平常也不過的方法了。Javascript的文化就是Event Programming。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Node.js 就是讓你單純只用Event、non-blocking的infrastructure來寫高度concurrent的程式。設計的目標是任何的function都不能直接存取I/O，一定要用callback的function來處理。其他特性還有專注在Low level、什麼都用串流、不強迫buffering、提供DNS/HTTP/TLS的內建支援。</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">HTTP包含: Chunked encoding, Pipelined message, hanging message.</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Node的API要用client side JS Programmer熟悉的慣例，幾乎100% MIT/BSD Licensed。(唯一例外是openssl)</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">架構</span>
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span>
Javascript &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Node standard library
------------------------------------------------------------
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Node binding
C &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; -------------------------------------
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;V8 &nbsp; Thread pool &amp; event pool

努力把使用者關在non-blocking的環境，用C語言當作屏障... XD

**Node execution stack : only one stack**

| load(index.html) &nbsp; &nbsp;|
-------------------------
| http_parse(1) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
-------------------------
| socket_readable(1) |
-------------------------
| ev_loop &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
-------------------------
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| |
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;V

| file_loaded() &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
-------------------------
| ev_loop &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
-------------------------

然後是一大堆的小段程式範例。
包含web server和 file system的non-blocking I/O.
然後是2010年接下來的 Road Map。