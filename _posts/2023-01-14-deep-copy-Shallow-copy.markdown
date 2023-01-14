---
layout: post
title:  "在JS中複製object-深拷貝/淺拷貝"
date:   2023-01-14 20:01:00 +0800
categories: javascript
---
### 在JS複製object

在寫code有時候會需要使用某些變數或是object，但是又不希望直接對其做操作，因為可能在其他地方會繼續使用原始的object，
這時候就會宣告一個新的變數去把原先的object assign過去。
```
const source = {name:'Andy',coutry:'Taiwan',phone:'0911-111-111'}
//原始資料

const destination = source 
//新變數
destination.name = 'Rendy';

console.log(destination.name);  //結果: Rendy
console.log(source.name);       //結果: Rendy
```

這時候會發現，變更 `destination` 同時也變更 `source` 裡面的值。
這就要提到 call by value 以及 call by refence

### call by value / call by object

#### 什麼是call by value?
```
let x =1;
let y = x;

console.log(y); // 結果:1
y=10;
console.log(y); //結果:10
console.log(x); //結果:1
```
以一般變數assign來說，是以call by value，也就是說直接把 `x` 的值傳給 `y`

#### 什麼又是 call by reference?
在一開始的object assign方法就是 call by reference，意思就是說 `source` 這個變數在assign給 `destination` 時，他是以傳遞記憶體位址方式給`destination`，可以想像 `destination` 就是儲存一個記憶體位置，當程式要讀取資料時就會透過這個位置去存取這個記憶體位置實際儲存的值。

所以這樣就可以很明確的瞭解為什麼改變object的值的時候，`source` `destination` 裡面的值會被同步更動，因為兩者都是指到同一個記憶體位置。

#### 要怎麼做才能不更動 source 的值
這樣就要提到 淺拷貝跟深拷貝

#### 淺拷貝
字面意思就是比較淺，
這時候就會使用Object.assign [MDN介紹](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
舉例：

```
//Object.assign()
const source = {name:'Andy',coutry:'Taiwan',phone:'0911-111-111',detail:{age:10, job:'photographer'}}
//原始資料

const destination = {} 
Object.assign(destination,source);  //把objec assign 給 destination

destination.name='rendy';
console.log(destination.name,source.name) //結果 Rendy Andy 互不影響

destination.detail.age=100;
console.log(destination.detail.age,source.detail.age) //結果: 100 100
```
在這裡會發現修改 `name` 時資料互不影響，但在修改detail.age時又互相影響了，這是因為使用的是淺拷貝，這個copy只有單純複製第一層的資料，第二層以下的都還是以call by referenc，所以當你修改detail.age時兩邊同時都會被修改。
 
#### 以深拷貝來解決淺拷貝的問題
使用 JSON.parse(JSON.stringify())，用這個方法就可以把淺拷貝碰到裡面有多層的問題。
```
const destination = JSON.parse(JSON.stringify(source));

```

相關參考
[參考1](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
[參考2](https://jamie-life-coding.site/2021/10/javascript-copy-object/)
