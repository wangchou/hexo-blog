---
title: 淺談函數式編程和 React
tags:
  - functional programming
  - react
date: 2016-01-29 16:08:00
---

函數是有定義介面的運算單元。<space><space><space><space>

介面有用的地方是抽象化，你只需要知道輸入什麼(Input)、會得到什麼輸出(Output)，你不用知道它細節是怎麼做到的。其實有個超能力在背後，也沒關係。當然這是在沒有碰到 bug 和有良好文件、不需要修改它的前提之下。<space><space><space><space>

再強調一次，你只需要理解輸入(input)會對應到什麼輸出(output)就夠了。<space><space>

### <u>問題來了，怎樣的輸入和輸出的對應「介面」會容易讓人理解？</u>

- 有意義的函數名稱
- 多寫沒有副作用的純函數
  - 有可預測性：
       每次輸入得到相同的輸出、函數內部不存狀態    
  - 沒有副作用：
       運算過程中不會改到外界的變數，像是不改傳進來的參數、不改可以存取的全域變數。    
  - 顯式(Explict)：
       函數和外界溝通的管道只有，傳進來的參數和回傳值。

- 簡化參數、對資料結構的 Information Architecture 做良好設計

- 用函數來定義函數
  - 柯里化(Currying)：
       透過不同給參數來產生新的函數
  - 合成(Compose)：
       透過 pipeline 串接函數的input和output、隱藏參數，產生新的函數。

### <u>函數式編程為什麼強大、有彈性？</u>

- 把每個函數切得很小，容易更新、維護、平行處理、多人共同開發、被理解

- 透過合成(Compose)把小函數變成大函數，比用繼承有彈性的多

- 對集合實做 Functor 介面，讓一般函數都可以對集合操作。(array, matrix, tensor)

- 把純和不純的函數分開來管理，容易找到問題點。

### <u>函數式編程為什麼難寫？</u>

因為函數式編程想要把程式變簡單。但大家都知道「變複雜是簡單的、變簡單是複雜的」。所以這種方式寫程式需要設計、思考，你會是一個程式「設計師」。但如果你現在的專案寫完之後沒人會看、不會再改、不用維護、規模不大，也許函數式編程並不能幫到這個專案多少。

### <u>寫 React 就是實踐函數式編程</u>

- 透過自定義元件，定義畫 View 的抽象化函數樹

- 透過 JSX 語法把小函數組合成大的函數 (等同於 compose)

- 鼓勵大家寫 dumb 元件、也就是純函數

- 用唯讀的 props，限制大家不能改傳進來的參數、減少副作用

- 透過導入 flux，把純和不純的函數分開來管理
  - 純的 (對資料只做讀的動作)：每個元件中的 render function
  - 不純的 (對資料做讀和寫的動作)：
       flux中對 action 的 callback、redux 中的 reducer、父元件傳給子元件的 callback
  - glue code：元件中其他的 javascript
![](http://2.bp.blogspot.com/-wg5mnU0UosE/VqsbPjd6AfI/AAAAAAAA4Ak/FN1MAFQndCY/s640/unnamed.jpg)

### <u>從函數式編程的角度看 React 的問題？</u>

- 沒有什麼高階的集合操作方法：
  - 把 lodash.js 集合操作拉進來用？
  - 用 lenses 的方式來穿透深長不露的 states?

- 沒有簡單的 currying 語法
  - 像是傳不同參數給 html5 input 元件，生出各式各樣對數字的、email、submit、text的自定義元件。最簡單寫法應該是 
  - export function NumberInput(props) { 角括弧input type=“number” {…props} /> }
  - PS: function 一定要有名字不然 debug 會很慘。

- 雖然集中管理了不純的函數，但還是很難寫：現在透過修改 store 中的 state 來控制元件，這邊 action 觸發的都是不純的函數，如果元件架構一深，還是會很難改。有解嗎？這邊還沒找到什麼 coding guideline…
  - 多個 container smart 元件
  - flux 的多個 store
  - redux 的階層式 reducers

-----------
延伸閱讀：
[deku: functional alternative to react ](https://segment.com/blog/deku-our-functional-alternative-to-react/)
[how to use classes and sleep at night (in a functional way)](https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4#.jkarowg5n)
