---
title: Redux = 事件驅動系統 = 伺服器
tags:
  - event system
  - one way data flow
  - react
  - redux
date: 2015-11-08 14:58:00
---

<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Redux 做的事情其實很簡單 ( [主程式才99行](https://gist.github.com/gaearon/ffd88b0e4f00b22c3159)&nbsp;)，就是可客制 Event 的 Event System。這概念在別的領域已經很成熟。但因為 Redux 的目標使用者是 Flux 的使用者，套用了很多原來 Flux 裡的專有名詞，所以對非 Flux 使用者變得很難懂。這邊透過類比大家都知道的名詞，目標讓 Redux 的概念連六歲小孩都能理解。</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span>

## <span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Flux：</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Actions trigger reducer to update states in the store.</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span>

## <span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Redux 的行為等於事件驅動系統 ( Event-driven System ) / 有限狀態機 ( FSM )：</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Events trigger event handler to update states in the machine.</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><table class="graytable">  <tbody><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Action</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Event | Signal | Message</span></td>    </tr><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Reducer</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Event Handler | Finite State Machine 中的 transducer</span></td>    </tr></tbody></table><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span>

## <span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Redux 的行為等於一個網頁伺服器：</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">When a request came, using route table mapping to get a method to process it。 </span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><table class="graytable">  <tbody><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Action</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Http Request</span></td>    </tr><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Store.dispatch(Action)</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">送 Request 到 Server</span></td>    </tr><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Reducer</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Router 把 Request 送到對應的 Router Method，更新 Database</span></td>    </tr><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Store</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Database</span></td>    </tr><tr>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">UI / React</span></td>    <td><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Http Response</span></td>    </tr></tbody></table><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Redux的行為等於巷口那家... 哎 想不出來比較生活的說法。</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">現在有沒有覺得 Redux 很 Awesome？好像沒有啊... 但我們回到瀏覽器的環境重新看一下，因為 HTML 的元件很小，開發者會組合 HTML元件成為可重複使用的「大元件」。但問題是瀏覽器中的 「事件處理系統」 是針對 HTML 小元件的，沒有給「大元件」的。於是Redux 提供了給開發者可以自行定義事件的「大元件」事件處理系統，因為你可以控制整個事件處理系統，重播和紀錄事件都變成毫不費力的事。現在又感覺到 &nbsp;Redux 很 Awesome了吧!!!</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">故事到了這邊，一定會想這樣解說，哪個六歲小孩能了解啊，相信這是大家共同的疑惑，不過 「投資一定有風險，基金投資有賺有賠，申購前應詳閱公開說明書」，我會反省的...</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">---</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
</span><span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">延伸閱讀：</span>
<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">[redux 的專有名詞解釋](http://rackt.org/redux/docs/Glossary.html)</span>
[<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Redux Issue 891：Is redux conflating actions with events?</span>](https://github.com/rackt/redux/issues/891)
[<span style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">六歲小孩也能懂的 Javascript Closure 說明</span>](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)