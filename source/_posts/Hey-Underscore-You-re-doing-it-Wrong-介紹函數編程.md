---
title: 'Hey Underscore, You''re doing it Wrong! (介紹函數編程)'
tags:
  - composition
  - currying
  - functional programming
  - functors
date: 2016-01-28 22:05:00
---

<iframe allowfullscreen="" class="YOUTUBE-iframe-video" data-thumbnail-src="https://i.ytimg.com/vi/m3svKOdZijA/0.jpg" frameborder="0" height="266" src="https://www.youtube.com/embed/m3svKOdZijA?feature=player_embedded" width="320"></iframe>

----------------------------------------------------------
Curried Function：到拿到所有需要的參數前... 一直回傳新函數的函數。
```js
var add = function(x) {
  return function(y) {
    return x + y;
  }
}

var add3 = add(3);
add3(4); //return 7

add(3)(4); //weird thing 
</pre> autoCurry in Wu.js will save us <pre style="background-color: rgba(0,0,0,0.1); padding: 10px;">
var add = function(x, y) {
  return x + y;
}.autoCurry();

var add3 = add(3);
add3(4) //7

add(3,5) //8 => not weird any more!!!
</pre> 但我們為什麼需要 curry？參考下面這個組成新 function getTheOdds 的例子。 有了currying，我們可以透過給予不同參數來建立新的函數。 <pre style="background-color: rgba(0,0,0,0.1); padding: 10px;">
var filter = function(f, xs) {
  return xs.filter(f);
}

filter(isOdd, [1,2,3,4,5]) // [1,3,5]

var getTheOdds = filter(isOdd);
getTheOdds([1,2,3,4,5]) //[1,3,5]
</pre> 再來一個用loadash的酷例子 <pre style="background-color: rgba(0,0,0,0.1); padding: 10px;">
//沒用currying、不函數化的寫法
var firstTwoLetters = function(words){
  return _.map(words, function(word){
    return _.first(word, 2);
  });
}

//函數化的寫法(如果underscore吃參數的方式是反過來的話)
var firstTwoLetters = _.map(_.first(2));

//更函數化的寫法
_.map(_.first(2), ['jim', 'kate']) //['ji', 'ka'] 
``` 
=> Underscore.js的參數排列法讓currying變得不可能  總結currying的優點有下面四個： 
* 一般化函數、要傳的變數名消失了 
* 透過給不同參數就可以生成不同的函數 
* 更簡潔的定義 
* 讓函式的組合/合成 (composition) 變的可能  
---------------------------------------------------------- 
組合/合成 (composition):用多個函數來組成新函數  簡單的例子，用 first() 和 reverse() 來合成 last 函數 
```js
var last = function(xs) {
  var sx = reverse(xs);
  return first(sx);
}

var last = compose(first, reverse);

last([1,2,3]) //3
``` 
另一個例子，chain backwardly 
```js
var wordCount = function(str){
  var words = split(' ', str);
  return length(words);
}

var wordCount = compose(length, split(' '));
wordCount("There is a way to save the world") //8
``` 
**Category Theory:** 多個函數組合(compose)，作用域互相對應的理論。Connecting the dot.  總結組合：
* 能從其他函數組成新函數 
* 組合過程中把參數藏起來 
* 極為高階的寫程式 
* 有數學理論在後面支持  
------------------------------------------------------------------ 
Functors  map 打開了後面的 object 然後做一些事、再放回 object 
```js
var plus1 = function(x){ return x + 1 }

plus1([3]) //wrong!!

map(plus1, [3]) //4
```
剛剛舉的例子，map 只能操作 array object、但下面試圖用 map 操作所有 object 
```js
map(plus1, MyObject(3)) //MyObject(4)

MyObject = function(val) {
  this.val = val;
}

MyObject.prototype.map = function(f) {
  return MyObject(f(this.val));
}
``` 
如果對 object 定義了 map function，它就變成 functor null check的例子、Dynamic Safety： 
```js
map(plus1, Maybe(3)) //=> Maybe(4)

map(plus1, Maybe(null)) //=> Maybe(null)

Maybe = function(val) {
  this.val = val;
}

Maybe.prototype.map = function(f){
  return this.val ? Maybe(f(this.val)) : Maybe(null);
}
``` 
把 ES6 promise 變 functor 的例子 <pre style="background-color: rgba(0,100,100,0.1); padding: 10px;">
```js
map(populateTable, $.ajax.get('/posts');

Promise.prototype.map = function(f) {
  var promise = new Promise();
  this.then(function(response){
    promise.resolve(f(response));
  });
  return promise;
}
``` 
再來一個和 html 合作的例子：對有和沒有 user_login 的情況下，更新歡迎頁面。 <pre style="background-color: rgba(0,100,100,0.1); padding: 10px;">
```js
$div = $("#myDiv");

//dot 會把 user.name 拿出來
var getGreeting = compose(concat('Welcome '), dot('name'));

var updateGreetingHtml = compose($div.html, getGreeting);

map(updateGreetingHtml, Maybe(App.current_user));
``` 
underscore 不讓人 extend map  總結 functor 能: 
* 改變函數的行為卻不用變動 open/closed principle 
* 不光只有 map, 還有 reduce & compose *
直覺且非私人的 api 
* free formulas 
* 動態型別安全/檢查 
------------------------------------------------------------- <space><space>
總結：underscore 能變得更加 functional。希望有更 functional 的 library
