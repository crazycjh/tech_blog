---
layout: post
title:  "在vue中把變數傳進css"
date:   2023-01-14 20:01:00 +0800
categories: vue
---

某些時候會希望動態改變css的樣式高度、寬度、顏色...等等的
在vue中可以宣告一個ref變數(composition API)，然後把搭丟到vue檔案中的 <style></style>中，又或者透過inline的方式直接插入到html tag中，舉例如下：

```
setup(){
    const mdSize = ref("100px");

}
```
### 傳到<style>

```
<div class="md-size"></div> //在這裏class不需要v-bind
<style>
.md-size{
    height:v-bind(mdSize);
}
</style>    
```

### 以傳值的方式丟到inline

搭配v-bind 也就是縮寫 ":"
把mdSize放進去style

```
<button :style="{ height: mdSize }" > 按鈕名稱 </button>
```
