---
title: JavaScript 排序 - sort
date: 2023-02-08 14:23:26
tags: [學習筆記, JavaScript]
---
在JavaScript 30挑戰的路上遇到sort，以往只用來排序數字大小，當我寫到第四天（實際上超過4天）遇到它，還是寫篇筆記吧...

## 根據字串的 Unicode 編碼排序
像下面這個例子，一般來說順序應該是[1, 4, 21, 30, 100000]但因為數字會被轉換成字串，再轉成Unicode編碼，所以100000會在4前面。
```
const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);

結果： Array [1, 100000, 21, 30, 4]
```
## sort排序會變更原陣列
如上面演示的，當我們使用完sort，再去印出原本的陣列，會發現資料順序是排序過的。

## compareFunction可以使sort使用回傳值比較排序
為了解決上面提到的Unicode排序很亂的問題，我們可以使用compareFunction去定義排序規則。

先來個基本款：```arr.sort((a, b) => {return a - b})```

原理（越大放越後面）：
a - b < 0，會把 a 排在 b 前面。
a - b = 0，不會進行排序，但會和其他全部的元素比較來排序。
a - b > 0，會把 b 排在 a 前面。

升冪及降冪可以這樣寫
```
arr.sort([compareFunction])

#升冪排列
function compareNumbers(a, b) {
  return a - b;
}

#降冪排列
function compareNumbers(a, b) {
  return b - a;
}
```
### 可套用在物件的排序
假設有一個陣列，裡面的元素都是物件，我們也可以用sort針對物件的屬性進行排序。
```
const inventors = [
        { first: "Albert", last: "Einstein", year: 1879, passed: 1955 },
        { first: "Isaac", last: "Newton", year: 1643, passed: 1727 },
        { first: "Galileo", last: "Galilei", year: 1564, passed: 1642 },
        { first: "Marie", last: "Curie", year: 1867, passed: 1934 },
        { first: "Johannes", last: "Kepler", year: 1571, passed: 1630 },
        { first: "Nicolaus", last: "Copernicus", year: 1473, passed: 1543 },
        { first: "Max", last: "Planck", year: 1858, passed: 1947 },
        { first: "Katherine", last: "Blodgett", year: 1898, passed: 1979 },
        { first: "Ada", last: "Lovelace", year: 1815, passed: 1852 },
        { first: "Sarah E.", last: "Goode", year: 1855, passed: 1905 },
        { first: "Lise", last: "Meitner", year: 1878, passed: 1968 },
        { first: "Hanna", last: "Hammarström", year: 1829, passed: 1909 },
      ];
```
#### (1)以年齡排序（比較數字）
就如同一般比較數值大小
```
const question3 = inventors.sort(function (a, b) {
        return a.year - b.year;
      });
console.table(question3);
```
![](https://i.imgur.com/T5x61J9.png)

#### (2)以姓名做排序（比較字串）
如果用inventorA - inventorB 會沒有效果，而其中的1或-1我很好奇的試一下，發現要一正一負才能排序（1:2、-1:-2都不會排序），如果把-1：1倒過來則會變成相反的排序。另外這種比較方法也同樣可以比較數值大小。
```
const question3 = inventors.sort((inventorA, inventorB) => { 
        return inventorA.first > inventorB.first ? 1 : -1;
            })
```
![](https://i.imgur.com/Fcr6ZnP.png)

參考資料：[MDN-sort](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
