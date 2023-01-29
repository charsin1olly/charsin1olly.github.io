---
title: var、let、const的差別
date: 2022-11-16 11:47:36
tags: [學習筆記, JavaScript]
---

## 1.重複宣告
```
var a = 1
var a = 2
console.log(a) // 印出2
```
var可以重複宣告，並且後來宣告的a會覆蓋前面的a。

```
let a = 1
let a = 2
console.log(a) //錯誤
```
let不能重複宣告，這樣執行console.log(a)會跳出錯誤訊息：
**Identifier 'a' has already been declared**
告訴你a這個名字用過了。

```
const a = 1
const a = 2
console.log(a) //錯誤
```
const和let一樣不能重複宣告，執行會跳出和let一樣的錯誤訊息 ：**Identifier 'a' has already been declared**。

## 2.重新賦值
```
var a = 1
var a = 2
a=3
console.log(a) //印出 3
```
var除了可以重複宣告以外，也可以直接用全域變數直接重新賦值
這樣console.log(a)印出來的結果會是3。

```
let a = 1
a = 2
console.log(a) //印出2
```
上面提到過let不能重複宣告，但它可以使用全域變數直接賦值

```
const a = 1
a = 2
console.log(a) //錯誤
```
雖然const跟let一樣不能重複宣告，但const更加嚴格，全域變數也不能重值賦值，會跳出錯誤訊息**Assignment to constant variable.**

但是const也不是完全不能改變，假如const是一個陣列，我們可以藉由指定元素來變更內容 ：
```
const a=["a","b","c","d"]
a[0]="X"
console.log(a) //印出[ 'X', 'b', 'c', 'd' ]
```

## 3.作用的scope
var的作用範圍是function scope，也就是作用在function區域裡面都可以取用的變數，出了function就拿不到了
```
function hi(){
  var a=1
}
console.log(a) //印出  ReferenceError: a is not defined
```
如果不是放在function內的話還是可以在外部取用
```
age = 10
if(age>5){
    var a = "in block!";
}
console.log(a); //印出in block!
```

let的作用範圍都是block scope，在{}的範圍以外就無法取用了
```
age = 10
if(age>5){
    let a = "in block!";
}
console.log(a);  //印出 a is not defined
```
補充：迴圈也是{}應用的一種（這裡的 a is not defined是指console.log("out:"+a)的a），通常使用let。<br>
為什麼不用const呢？因為a++等同於 a=a+1，我們前面已經讓a是一個常數(const)了，不能明目張膽的改變它的內容，執行會顯示錯誤訊息**Assignment to constant variable.**
```
for(let a=0 ; a<5 ; a++){
    console.log(a)
}
console.log("out:"+a) //印出 a is not defined

```

const也是block scope，a無法在外部被取用。
```
age = 10
if(age>5){
    const a = "in block!";
}
console.log(a);  //印出 a is not defined
```

## 4.TDZ 暫時性死區
```
console.log(a) //印出 undefined
var a = 1
```
**var有變數提昇**的特性，如果就以執行順序來看的話，明明還沒宣告var a = 1 怎麼console.log會說a是undefined呢？<br>
JS執行順序為由上往下，步驟分成兩步，第一步先註冊名稱，第二步為賦值，變數提昇有點類似預告，在第一步的時候掃描到var a，告訴系統：「今天有一個a客人會來喔！」，進入第二步賦值由於還沒輪到把1賦予a就被印出來了，所以結果是undefined。

```
console.log(a)
let a = 1

console.log(a)
const a = 1

以上console.log(a)都會印出 ReferenceError: Cannot access 'a' before initialization
```
let、const則是有一個TDZ，類似一個防雷馬賽克，在第一步的時候TDZ就蓋在let（const）上面，系統就不知道有a客人，進行到第二步就會像a去客人去系統報到，系統卻說：「你沒有預約訂位喔」的樣子。

這樣的設計可以使流程更加嚴謹，使程式邏輯更加通順、增加可讀性。
（就像是：我的點的菜還沒炒好卻可以包空氣帶走？這不太對吧？）
## 5.污染window
在瀏覽器的主控台上宣告 var a=1 , let b =2 , const c =3
在window裡面只會有a會被建立出來，


![](https://i.imgur.com/rzkMLRO.png)


【結論】<br>
宣告的嚴謹程度 const > let > var<br>
盡量使用const，可以視情況適當改用let，非到萬不得已再使用var。 

