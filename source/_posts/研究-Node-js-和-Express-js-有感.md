---
title: 研究 Node.js 和 Express.js 有感
tags:
  - backend
  - express
  - node
date: 2015-11-04 15:50:00
---

<div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">簡單來說網頁設計，就是設計ㄧ個讓在給了Key 後把相關資料轉換成網頁的 function。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Node 提供ㄧ個可以用 JS 與其溝通的 non-blocking http server。Express 在上面提供了簡易建立 RESTFUL API、在頁面間 (在 server 上) 傳遞資料的方法。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">從外部來看，就是一個 JavaScript 程式，然後你對它送一些 Request，他就會吐 http response 回來。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Http response 包含了資料 ( ex: 文章、作者、照片、標題、按鈕文字 ) 和 UI/排板 ( CSS / HTML / client-side JavaScript )。通常資料是不重複的。但根據不同的資料，UI 很多重複的地方就變成用 UI Template/UI 元件來表示。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">傳統產生網頁的方式是把資料和 UI 原件混成一個個各別的網頁然後傳給 Browser 畫出來；最近流行的方式是把資料和UI原件分別傳給 Browser，在 client-side browser 再用 JavaScript 把資料和 UI 原件組合成網頁。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">近年流行的 json 是一顆用 ( key:value or array ) pair建起來的關聯式資料樹。因此後端資料庫不再用關聯式資料庫，用簡單 NoSql 資料庫 ( 即 dictionary ) 就夠了。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">簡單來說現代的網頁開發就是開發一個程式：從後端抓一顆 json 資料樹，然後轉成前端美美的 DOM Tree。就是模組化的 Data Visualization，這樣想一切都輕鬆多了。</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">
</span></div><div><span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">這樣的想法很自然的催生了一堆 UI 的程式庫，像是 Angular.js 和 react.js，然後還有 mobile上的 react native。</span></div>