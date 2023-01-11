---
layout: post
title:  "在vue中一次watch多個變數"
date:   2023-01-10 18:00:50 +0800
categories: javascript
---

#### 在Vue3 & Composition下，想一次watch多個變數的實現方法
```
setup(){
    const message = ref('');
    const name = ref('');
    watch([message,name],([newValueMessage,newValueName],[oldValueMessage,oldValueName])=>{
        //do something
    })
}

```
#### watch vuex裡面的state或是其他reactive裡的某個值

```
//假設vuex state中影一個名為msg的值
setup(){
    const message= reactive({user1:''})
    watch([()=>message.user1,()=>store.state.msg],()=>{
        //do something

    })
}

```
使用 `()=> arrow` function去return reactive的值才能watch
