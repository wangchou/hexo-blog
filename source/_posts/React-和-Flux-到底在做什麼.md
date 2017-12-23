---
title: React 和 Flux 到底在做什麼?
tags:
  - flux
  - react
date: 2015-11-05 23:52:00
---

看了下面兩個文章，終於知道 React 和 Flux 在做什麼了。
<span style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">1.&nbsp;[ReactJS For Stupid People](http://blog.andrewray.me/reactjs-for-stupid-people/)</span>
2.&nbsp;[Flux For Stupid People](http://blog.andrewray.me/flux-for-stupid-people/)

以下開始和主題不很相關的廢話，可以直接跳到最後一段「好啦，說了一大堆廢話。」

前兩天一直迷惑，到底這套新的 UI 開發流程和我過去接觸過的 framework 們有什麼不同？以前用過 Java AWT, JAVA SWING, ZK Markup Language, JQuery UI, iOS UI Kit, Android, QT Component, OpenGL, xxxRendering Engine ... 列出來才發現，真的是有的沒的一大堆。

在螢幕上生出畫面大概可以分成三群：
1\. 網頁開發
2\. 桌上 / 手機的原生應用程式
3\. 遊戲 / 動畫

3) 寫遊戲和動畫的流程最簡單，大二用組語刻了魔法氣泡遊戲 / 大三參加趨勢比賽徒手硬幹JAVA Swing ( 真的超慢的 T.T ) / 研究所用 3DS Max 和 Blender 做動畫 / 工作上用 OpenGL 做了動態路徑規劃的資料展示。這一類大概每次就是重畫，隨時檢查物件狀態一直重畫。看一下 FPS 有到 Real-Time 就好。

2) 開發原生應用程式的流程就是用原生的物件，不管太元件長什麼樣子，反正就是設計互動，註冊事件，最多就小改一下背景、顏色之類的。反正最差就是比較醜，功能都沒問題啊。話說 MFC 到底是什麼鬼東西啊... 記得花了兩三天從來沒搞懂過。

1) 網頁開發不像開發原生應用程式，有功能性較大完整的原生元件。只有一堆小到不行的 HTML 元件。然後問題就來了... 網頁上一塊塊重複的物件，像是 部落格、購物網站、討論區上面一個個的模組要怎麼搞。

如果是靜態的網頁，就背後用 php 弄個模組 ( 喔 交作業而已別太嚴格啦 )，Header 一個Template、商品一個 Template、側邊欄一個 Template、導覽列一個 Template，然後就很開心地從資料庫抓一些資料填進去Template就好啦。有什麼事件發生就傳資料到伺服器端，整個重新畫頁面就好。老實說還挺簡單的，怎麼流程聽起來很像ReactJS。但是 2004 年，總是有一些天才們發明了一些讓人很累的東西叫做 Ajax 把 Gmail 推上了時代尖端。Ajax 告訴所有開發者：「喔 什麼!!! 你把使用者輸入送到伺服器再傳回來，然後才更新 UI，太慢了喔 弱~」。然後從這時候開始，網頁設計師就很苦情的開始在客戶端開始亂刻元件，MVC 邏輯的重擔就移交給 HTML、CSS、Javascript。但主流的開法方式是，不管 MVC 也行啦，反正網頁會動看起來有設計感就好。

JQuery Library 在這亂世中應運而生，讓我苦讀 vanilla Javascript 的經典「ppk談Javascript」變得英雄無用武之地，JQuery 的 selector 就像用 matlab 來處理資料的有快感、dot chain rule 讓語法看起來糖分很高、不用打 getElementById 就像 C++11 中用 STL 不用打 Iterator 一樣清爽。可以快速開發出很難維護的網頁。解決了 Javascript 操作 DOM 會讓人想罵髒話的問題。為什麼很難維護，因為沒有元件化，Javascript有很有力量，讓人在網頁裡隨性的的東改西改，但不知道誰改的就很難 Debug，漸漸變得複雜就不能開發大型網頁。

然後 AngularJS 把後端流行的 資料綁定搬到瀏覽器來，用 Javascript 的 Closure 來做封裝、一區區的資料分別藏起來，限制一部分 Javascript 只能操作 一部分的資料和 HTML，充分發揮了各個擊破的演算法 ( Divide and Conquer )，可是問題又來了... 媽的我花了兩天，學不會 AngularJS 啊一直 Typos 很煩，雙向綁定怎麼那麼複雜，讓我寫程式一直 NG NG。所以我沒太多研究，只聽說是雙向資料綁定會引起 DOM Tree 的 Cacading Update，導致效能容易有問題。另外 HTML 裡塞了太多髒髒的東西，容易消化不良。

### **<u>好啦，說了一大堆廢話，React 和 Flux 到底做了什麼？</u>**
React 讓人用 Javascript 和 HTML 刻更高級的元件 ( Virtual DOM )，像是 Angular 元件做的限制 讓一小段 Javascript只負責一小塊的UI / HTML更新，使用各個擊破的演算法，刻完元件之後就像開發原生應用程式時一樣，有了較大的元件，讓人跳脫低級 ( low level ) 的思考，少說一點髒話，透過 JSX 讓人從模組化的角度看 UI。簡單的譬喻就是讓人用組語開發高階語言的語法，之後可以用高階語言寫程式。

React 只 Update 新的 DOM Tree 中和前一次 DOM Tree 差異之處，他們管這叫 一致 (reconciliation) 讓重繪的速度快很多，當重繪夠快，網頁的開發者就可以回到 pre-AJAX時代，回憶2004年之前的寫開發體驗：把資料送回伺服器，然後收到新資料，整個網頁重繪。

只是這回，資料來源的不是 Database，是 <u>Flux 資料集中管理辦法</u>中的各個 Store ( Client-side Database )。Flux的單向資料流理念，強迫你在客戶端有一個像資料庫的資料集中處，Store裡有來自使用者輸入的資料、有來自伺服器端的資料更新。然後這個資料商店把每一家元件訂閱的資料送上門，元件看了看送來的資料商品然後就更新。Store 像是介於 CPU 和 硬碟中間的 Cache / Memory，是資料的 暫存處和Hub，或是你叫它客戶端的暫存資料庫也行 ( 用 Javascript 物件存的 )。

原來：
Browser -- Client Side ......................................... Server

有了 React + Flux 之後 :
Browser -- Client Side -- Client Side VM + Server ( React + Flux ) .......................................... Server

有點像是在 Client Side 包了一層 VM + Server 一樣，會把 JSX 轉譯成JS / HTML、集中把資料放在客戶端資料庫裡 ( Flux 的 Store )。

簡單總結一下：
React + Flux 是大規模動態資料網頁的解法。

React 讓需要大型互動元件的客戶端，可以用自己刻的、封裝良好的元件，並在新元件的高度思考。用了個 Reconciliation 的 Trick使得重繪很快，和 <u>Flux 的資料集中管理辦法</u>，讓開發者只要專注做好一件事「當資料來到元件時，把元件要畫好」。

---
Flux 目的是提出一個客戶端的資料管理辦法。其中的單向資料流 / 資料環其實隱含了 Two way Data Binding，只是不是綁死，比較像是 Two way Data Notification。Dispatcher 管的是 <span style="color: blue;">View Actions -&gt; Store ( Models )</span>。Store 除了存資料外還包含了 <span style="color: blue;">Store ( Models ) -&gt; View&nbsp;</span>的通知。還有人覺得 Dispatcher 很多餘，就寫了一個 reflux.js 把 Dispatcher 拿掉。

延伸閱讀：
[聊一聊基於Flux的前端系統](http://bbs.react-china.org/t/flux/615)