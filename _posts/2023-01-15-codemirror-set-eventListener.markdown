---
layout: post
title:  "codemirror 設定(註冊)事件觸發Codemirror.on"
date:   2023-01-16 18:01:00 +0800
categories: vue,js
---

### codemirror
什麼是codemirror，它是一款可以實現在前端網頁上的編輯器。
如同現在網路上看到的文字編輯器一樣，但你可以去設定當使用者做哪些操作時codemirror做哪些對應的行為。
[CodeMirror v5](https://codemirror.net/5/)

### 如何在codemirror編輯器設定事件觸發
[Event列表](https://codemirror.net/5/doc/manual.html#events)

使用 const editor = CodeMirror.fromTextArea()建立編輯器instance後
在透過這個instance去呼叫 `on` 這個function
```
editor.on("change",(cm,changeObj)=>{                  
    //這個意思是當editor文字有改變時就執行callback function
    
    //do something，這裡也可以加入其他CodeMirror的function執行
})
```
要怎麼使用on呢？ [官方介紹](https://codemirror.net/5/doc/manual.html#on)
```
cm.on(type: string, func: (...args))
```

舉例：
```
//建議以下function可以在頁面建立一併執行(如果是馬上要用到)，on的功能可以看成註冊的概念，把這個功能註冊給editor，條件有達到就會執行
editor.on("change",(cm,changeObj)=>{                  
    console.log(changeObj.ch);
    console.log(changeObj.line); 
    //在change中會有ch(第幾個位元) line第幾行
})
```
這裡的cm是指codemirror，在官方頁面中有提到，不管是看到codemirror(簡寫cm)或是doc，在使用上都可以用前面建立好的editor instance(端看使用者怎麼命名)

on裡面第一的參數 `type` 也就是 cursorActivity  或者 change 之類的事件，後面callback function裡面的參數，在每個event中都會清楚告訴你有什麼參數可以用。
在`change`中可以使用cm instance以及獲取改變的文字及其相關資訊。