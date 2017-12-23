---
title: ”redux.js --- 可預測的狀態容器“ 的 API 使用說明
tags: []
date: 2016-04-10 15:58:00
---

<pre>
這邊只會透過理解 Redux 的 API來簡介如何使用 Redux。這邊假設讀者都知道 web 中 event / listener 的 pattern。

如果想要知道 redux 背後的實作細節、原理、動機、Flux、Design Pattern、如何和 UI App 做連結，請看 Dan 的 Redux gitbook、Redux tutorial on EggHead。

**redux 是一個狀態容器 (state container / state machine)**

狀態容器要提供幾個功能
1\. 初始容器狀態 _by Redux.createStore(**reducer**)_
2\. 取得現在的狀態 _by store.getState()_
3\. 狀態改變時，通知相關的程式 _by store.subscribe(**listener**)_
3\. 接收事件發生的通知、改變狀態 _by store.dispatch(**action**)_
4\. 建立之後改變事件處理方式 _by store.replaceReducer(**reducer**)_
5\. 由小的狀態容器組成全域狀態容器 _by 只能透過 combineReducers 來組成 root reducer，再用它來建全域狀態容器_

Flux 專有名詞：store、action、reducer。

store := 一個狀態容器
action := 一個像 Event 一樣有 type 屬性的 javascript object
reducer := 一個輸入 state 和 action、回傳新 state 的函數, (state, action) -> new_state

但 store 是 redux 中唯一一個狀態容器的名字。其實 API 等同於下方這樣子
1\. _by Redux.createStore(**reducer**)_ 等於 _by Redux(**reducer**)_
2\. _by store.getState()_ 等於 _by Redux.getState()_
3\. _by store.subscribe(**listener**)_ 等於 _by Redux.addListener(**listener**)_
3\. _by store.dispatch(**action**)_ 等於 _by Redux.dispatch(**action**)_
4\. _by store.replaceReducer(**reducer**)_ 等於 _by Redux.replaceReducer(**reducer**)_
5\. _by 無直接 API，只能透過 combineReducers 來組成root reducer，然後用 root reducer 來建全域 store_

一個狀態容器 = 狀態 + reducer，但 reducer 中可以指定初始狀態、所以一個 reducer 其實可以定義一個狀態容器、等同於一個狀態容器，所以 API 等同於下方這樣子
1\. _by Redux.initContainer(**reducer**)_ 等於 _by Redux(**container**)_
2\. _by Redux.getState()_
3\. _by Redux.addListener(**listener**)_
3\. _by Redux.dispatch(**action**)_
4\. _by Redux.replaceReducer(**reducer**)_ 等於 _by Redux.container.replaceReducer(**container.reducer**)_
5\. _by 只能透過 combineReducers 來組成 root reducer，再用它來建全域狀態容器_ 等於 _Redux.combineContainer_

把 combineContainer 用 addContainer 取代，API 可以改寫成這樣子
1\. 初始容器狀態 _by Redux()_
2\. 取得現在的狀態 _by Redux.getState()_
3\. 狀態改變時，通知相關的程式 _by Redux.addListener(**listener**)_
3\. 接收事件發生的通知、改變狀態 _by Redux.dispatch(**action**)_
4\. 建立之後改變事件處理方式 _by Redux.getContainer(**name**).replaceReducer(reducer)_
5\. 由小的狀態容器組成全域狀態容器 _by Redux.addContainer(**container**)_
6\. 建立小的狀態容器 _by Redux.container(name, initialState, reducers)_

`
所以翻譯過後 redux api 的使用流程就會變成
let addReducer = (state, ADD_ACTION) => state++
let subtractReducer = (state, SUBTRACT_ACTION) => state--

counterContainer = Redux.container(
  'counter', 
  0, 
  [addReducer, substractReducer]
)

Redux.addContainer(counterContainer)

class CounterComponent {
  constructor(props) {
    this.stateChangeListener = (state) => this.setState(state)
    Redux.addListener(this.stateChangeListener)
  }
  componentWillMount() {
    this.setState(Redux.getState().counter)
  }
  onAddButtonClick() {
    Redux.dispatch(ADD_ACTION)
  }
  onSubtractButtonClick() {
    Redux.dispatch(SUBSTRACT_ACTION)
  }
  ...
} 

`

總結，可以看出來 redux 最大的特點就是用 reducer 來定義 container state 的處理範圍，不能用 event callback 的概念去理解它，一個 reducer 對應到“一組” state、多個 actions。

所以在 Redux 中 reducer 差不多是 container state scope 等價。也因此在 Redux 中 sub-container / sub-store 的名字完全被省略了，你只能用 reducer 的名字來找到他們影子。只要知道這個規則大概就能夠理解 Redux 了。

reducer := (state, action) -> new_state (你找不到 container 的名字、它被省略了)

老實說，我覺得這樣子的開發者經驗很不舒服 (bad UX)
---
不知道 re-frame 的 UX 會不會比較好？
</pre>