---
layout: post
title:  "如何在vue上建立codemirror編輯器"
date:   2023-01-01 08:53:18 +0800
categories: javascript
---

### 什麼是codemirror
codemirror是一個可以應用在web頁面的程式碼編輯器。

### 如何使用？
前一陣子為了寫一個markdown編輯器尋尋覓覓的網路上搜尋資料，找到codemirror，後來在vue上實現它。
`codemirror` 目前最新版為 v6。
但目前使用的是v5
v5官方文件 [codemirror v5](https://codemirror.net/5/)


### 把editor放到web上
```
var myCodeMirror = CodeMirror(document.body, {
  value: "function myScript(){return 100;}\n",
  mode:  "javascript"
});
```
CodeMirror第一個參數，是要把editor掛的地方，在範例是選擇對body做掛載，而我是選擇用另一個方法，在html建立一個textarea，把editor建立在這上面。

[參考](https://codemirror.net/5/doc/manual.html#fromTextArea)
```
var myCodeMirror = CodeMirror.fromTextArea(myTextArea);
```
要怎麼使用myTextArea這個參數，可以 *document.getElementById('idName')* 的方式去對textarea與codemirror做連結，所以在textarea的tag中要記得先建立好相對應的id。

不管是body或是textarea，第二個參數都是configuration，他們是以json格式的方式儲存設定，裡面可以設定theme,mode,keyMap,extraKeys,configureMouse...等等的東西。[configuration](https://codemirror.net/5/doc/manual.html#config)

#### Event
[Event](https://codemirror.net/5/doc/manual.html#events)

在上面建立好codemirror後，就可以對編輯器的一些事件作設定，他可以有編輯器內文字變化(change),focus,scroll等等，詳細的可以網路上查更多資訊，[官方資料](https://codemirror.net/5/doc/manual.html#events)

使用方法：以上面建立好的codemirror物件(?)， ` myCodeMirror.on('change',()=>{}) `
這裡除了on之外還可以off，也就是可以把事件關閉。
在這裡帶的callback function的參數可以參考[event](https://codemirror.net/5/doc/manual.html#events)，依照每個不同的事件都有對應的參數，以change為例，他的第二個參數中有 `{from, to, text, removed, origin}` ，可以看到起始位置、最後位置、移除什麼字元、是移除還是新增。

#### 取editor裡面的text/set text *API constructor* [連結](https://codemirror.net/5/doc/manual.html#api_constructor)

`myCodeMirror.getValue()`
`myCodeMirror.setValue('字串')`

#### instance/ doc
在文件中config或是api中會看到cm(應該就是codemirror這個instance)與doc，我的理解是instance是指整個編輯器，而doc是指編輯器中這個文字document，所以以文件中寫的`doc.getValue()` ，照理說要這樣寫，`myCodeMirror.doc.getValue()`(實測也是沒問題的)。

不過在文件中有提到 *Methods prefixed with doc. can, unless otherwise specified, be called both on CodeMirror (editor) instances and CodeMirror.Doc instances. Methods prefixed with cm. are only available on CodeMirror instances.*
所以可以直接以 `CodeMirror instance 取代 CodeMirror.Doc instance，不過兩者都可以使用` 