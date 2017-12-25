---
title: Redux 簡介：我終於看穿它了
tags:
  - firebase
  - MobX
  - Model
  - redux
date: 2016-11-06 16:41:00
---

Redux 把資料放在 store 中，它是個資料庫，但 Redux 不用常見的 SQL 介面，要開發者自訂指令介面。這介面有簡單的標準，他只接受 Action = {type, payload} 物件的輸入。在傳統的資料庫中，下了 SQL 資料庫就會照指令，來更新資料庫，但在 Redux 中，開發者需要自行寫一個 Reducer 來處理輸入的 Action 指令。和傳統資料庫不同的是，這個 Redux 資料庫變了之後，Redux 會 push 變動了的資料到訂閱者 (一個 Javascript 物件)，行為就像是 Baas 服務 (parse, firebase) 常見的 push message。Redux 和傳統關聯式資料庫最大的不同點是，Redux 用 JS 物件或變數來儲存資料；傳統資料庫因為有大量相關的資料，所以用資料表 (data array, data table) 來儲存。這讓 Redux 的狀態樹一直呈現很難視覺化的情況，目前樹狀結構最好的視覺化就是，Browser 的 dev tool 了。如果能把 Redux state 架構轉成 html，也許會有很好的效果也不一定。 另一個選項是 D3.js 的 Simple Tree。

# 簡單的資料庫列表比較
![](https://4.bp.blogspot.com/-sSMTas7I6yk/WB7sjh1ylYI/AAAAAAAA45k/E5kCkDcf1F0ZYe-Xf4Yv4KGeIfnnowtUwCLcB/s1600/Screen%2BShot%2B2016-11-06%2Bat%2B4.37.19%2BPM.jpg)

Redux 和 Firebase 的資料儲存方式很相近，可以很好的一起運用整合。也許進一步把 client 的資料再切為，Server Data 和 View Data 的設定會更好。Server Data will always synced with Firebase.

另外一提，Redux 實際上就只是個資料庫 (Model)，只有 input & outpt，哪有什麼 middleware… in the middle of what？Redux-middleware 實際上是一部分的 controller，跟 Redux 無關啊。React 也包含 Controller。畫成圖來表示
![](https://3.bp.blogspot.com/-iuJOF3G-YCg/WB7sNkMUYfI/AAAAAAAA45g/-T3GLN0twVwBwHN2hm9_ncod0-qlG4krQCLcB/s1600/Screen%2BShot%2B2016-11-06%2Bat%2B4.38.55%2BPM.jpg)

Flux 把傳統的 MVC 切成了上行和下行，形成了一個循環資料流，它最大的優點是有 paper 支持的 Single Source of Truth。想像一下 bug 在房間亂跑好抓還是... bug 繞著固定的圈圈跑，bug 繞圈圈跑的話，在原地等 bug 跑過來就抓到了。

總結一下，說穿了 Redux 就是一個啥功能都沒有的資料庫設計規範。也因此，他的文件很長、相關模組很多。
