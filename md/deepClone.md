## ðï¸åè¨

å¨ä¸ä¸ç¯æ°ç»å»éçæç« éï¼ä½¿ç¨å é¤åç´ å®ç°æ°ç»å»éæ¶ï¼ææå°è¿concat()è¿ä¸ªæ¹æ³ï¼å´å¹¶æ²¡æè¯´å®çå·ä½ä½ç¨ï¼è¿å°±åä»å¤©çæµæ·è´æå³äº

å¨è¿ä¹åï¼æä»¬æä¸ä¸ªåéå¼ç»å¦ä¸ä¸ªåéæ¶ä½¿ç¨çæ¯èµå¼æä½ï¼èµå¼ä¹åä¸¤ä¸ªåéå¶ä¸­ä¸ä¸ªçå¼æ´æ¹ä¹ä¸ä¼å½±åå°å¦ä¸ä¸ªåé

ä½æ¯ä¸ºä»ä¹æ°ç»èµå¼ä¹åï¼å¯¹æ°æ°ç»è¿è¡å»éï¼åæ¥çæ°ç»ä¹ä¼éçæ°æ°ç»ä¸åååå¢ï¼

### ð·ï¸èµå¼æä½

é¦åæä»¬è¦ç¥éèµå¼æä½èµçæ¯ä»ä¹å¼

åºæ¬æ°æ®ç±»åèµå¼ä¼ éçæ¯å­æ¾å¨æ åçæ°æ®ï¼èå¼ç¨ç±»åèµå¼ä¼ éçæ¯ä»ä»¬å­æ¾å¨æ åçå°åï¼å®ä»¬çæ°æ®å­æ¾å¨è¿ä¸ªå°åæåçå åå­é

æä»¥å¼ç¨ç±»åèµå¼ä¼ éçæ¯å­å¨æ åçå°åï¼å½å¯¹æ°å¯¹è±¡è¿è¡æ°æ®çä¿®æ¹æ¶ï¼æ¹åçæ¯è¿ä¸ªå°åæåçå åå­éçæ°æ®

å ä¸ºæ°æ§å¯¹è±¡ä½¿ç¨çæ¯ç¸åçå°åï¼å°åæåçæ°æ®æ¹åä¹åï¼æ§å¯¹è±¡çå¼ä¹å°±éä¹æ¹åäº

![èµå¼ (1).png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ea374bf80b074af886bc5f056611b9f9~tplv-k3u1fbpfcp-watermark.image?)

ä½æ¯æä»¬ä¸è¬æ¯ä¸æ³è®©åå¯¹è±¡çæ°æ®æ¹åçï¼é£è¦æä¹è§£å³è¿ä¸ªé®é¢å¢ï¼è¿æ¶åå°±ç¨å°äºæ·±æµæ·è´

## ðæµæ·è´

é£åæ¥è¯´æµæ·è´

æµæ·è´åå»ºä¸ä¸ªæ°çå¯¹è±¡ï¼åªæ·è´ä¸å±ï¼å³æ·è´å¯¹è±¡éç¬¬ä¸å±åºæ¬æ°æ®ç±»åçå¼åå¼ç¨ç±»åçå°å

![æµæ·è´.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58a46d1816504d12aff85b7d03e96b42~tplv-k3u1fbpfcp-watermark.image?)

ä½æ¯æ·±å±æ¬¡çæ°æ®è¿æ¯ä¼äºç¸å½±å

å¦æä¿®æ¹æ°å¯¹è±¡éç¬¬ä¸å±åºæ¬æ°æ®ç±»åçå¼ï¼ä¸ä¼å¯¹æ§å¯¹è±¡äº§çå½±åï¼ä½å¦æä¿®æ¹ç¬¬ä¸å±çå¼ç¨ç±»åçå¼ï¼ä»ä¼å¯¹æ§å¯¹è±¡äº§çå½±å

å ä¸ºæ°æ§å¯¹è±¡è½ç¶ä¸åä½¿ç¨åä¸å°åï¼ä½ç¬¬ä¸å±çå¼ç¨ç±»åçå°åä»æ¯ç¸åç

**ä¸¾ä¸ªæ å­**ð°

```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
// Object.assign()æ¯ä¸ç§æµæ·è´çæ¹æ³
let obj_new = Object.assign({}, obj_old)
console.log(obj_old === obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ef28246a52c9440485ea9b4fb16d53f4~tplv-k3u1fbpfcp-watermark.image?)

è¿éçä¾å­æä»¬ä½¿ç¨äºæµæ·è´ï¼ç¶åæä»¬æ¥å¯¹æ¯æ°æ§å¯¹è±¡

> obj_old === obj_newæ¯falseï¼è¿è¯´ææ°æ§å¯¹è±¡çå°åå·²ç»ä¸ä¸æ ·äº

> obj_old.name === obj_new.nameæ¯trueï¼è¿ä¸ªæ¯åºæ¬æ°æ®ç±»åçå¼æ¯ç¸åçï¼æ²¡æé®é¢

> obj_old.favorite === obj_new.favoriteä¹æ¯trueï¼è¿éçfavoriteä¹æ¯å¯¹è±¡ï¼ä½æ¯ä»ä»¬æ¯è¾åºæ¥çç»æä¸æ¯falseèæ¯trueï¼è¯´æè¿ä¸ªå¯¹è±¡çå°åå·²ç»æ¯ç¸åçäºï¼å®ä»¬å±äº«åä¸ååå­ç©ºé´

åæ¥å¯¹æ°å¯¹è±¡éçæ°æ®è¿è¡ä¿®æ¹

ä¿®æ¹æ°å¯¹è±¡ç¬¬ä¸å±çåºæ¬æ°æ®ç±»åæ¶ï¼æ°æ§å¯¹è±¡äºä¸å½±å
```js
obj_new.name = 'Jerry'
console.log(obj_old)
console.log(obj_new)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9e4dbeb50fb45c793e946388b330f42~tplv-k3u1fbpfcp-watermark.image?)

ä¿®æ¹æ°å¯¹è±¡ç¬¬ä¸å±çå¼ç¨æ°æ®ç±»åæ¶ï¼ä¹å°±æ¯ä¿®æ¹obj_newç¬¬ä¸å±çfavoriteå¯¹è±¡éçå±æ§å¼æ¶ï¼obj_oldéçfavoriteç¸åºçå±æ§å¼ä¹éä¹æ¹åäºï¼æ°æ§å¯¹è±¡ç¸äºå½±å

```js
obj_new.favorite.food = 'cheese'
console.log(obj_old)
console.log(obj_new)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2f6eaaed29d74785a3fb2a8e8541f75b~tplv-k3u1fbpfcp-watermark.image?)

### ð·ï¸æµæ·è´çæ¹æ³

äºè§£è¿æµæ·è´æ¯ä»ä¹ä¹åï¼è¿éå°±æ¥ç½åå ä¸ªæµæ·è´çæ¹æ³

#### 1. *Object.assign()*

> è¯­æ³ï¼Object.assign(target, ...sources)
>
> target
> ç®æ å¯¹è±¡ï¼æ¥æ¶æºå¯¹è±¡å±æ§çå¯¹è±¡ï¼ä¹æ¯ä¿®æ¹åçè¿åå¼ã
> sources
> æºå¯¹è±¡ï¼åå«å°è¢«åå¹¶çå±æ§ã

ä»£ç å±ç¤º
```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
let obj_new = {...obj_old}
console.log(obj_old === obj_new)  // false
console.log(obj_old.name === obj_new.name)  // true
console.log(obj_old.favorite === obj_new.favorite)  // true
```

#### 2. *å±å¼è¿ç®ç¬¦ Spread ...*

> è¯­æ³ï¼{...sources}
>
> sources
> æºå¯¹è±¡ï¼åå«å°è¢«åå¹¶çå±æ§ã

ä»£ç å±ç¤º
```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
let obj_new = Object.assign({}, obj_old)
console.log(obj_old === obj_new)  // false
console.log(obj_old.name === obj_new.name)  // true
console.log(obj_old.favorite === obj_new.favorite)  // true
```

#### 3. *Array.prototype.concat()*

> è¯­æ³ï¼arr.concat(value0, /* â¦ ,*/ valueN) 
>
> æ³¨ï¼å¦æçç¥äºææ `valueN` åæ°ï¼å `concat` ä¼è¿åè°ç¨æ­¤æ¹æ³çç°å­æ°ç»çä¸ä¸ªæµæ·è´ã

ä»£ç å±ç¤º
```js
let arr_old = [1, 2, {name: 'Tom'}]
let arr_new = arr_old.concat()
console.log(arr_old === arr_new)  // false
console.log(arr_old.name === arr_new.name)  // true
```

#### 4. *Array.prototype.slice()*

> è¯­æ³ï¼arr.slice(begin, end) 
>
> æ³¨ï¼å¦æçç¥äº `begin`, `end` åæ°ï¼å `slice` ä¼è¿åè°ç¨æ­¤æ¹æ³çç°å­æ°ç»çä¸ä¸ªæµæ·è´ã

ä»£ç å±ç¤º
```js
let arr_old = [1, 2, {name: 'Tom'}]
let arr_new = arr_old.slice()
console.log(arr_old === arr_new)  // false
console.log(arr_old.name === arr_new.name)  // true
```

## ðæ·±æ·è´

æ¥ä¸æ¥è¯´æ·±æ·è´

æ·±æ·è´å°±æ¯å¨å åå­ä¸­å¼è¾ä¸ä¸ªæ°çç©ºé´å­æ¾æ°å¯¹è±¡ï¼æ·è´åå¯¹è±¡çææå±æ§ï¼æ·è´ååä¸¤ä¸ªå¯¹è±¡äºä¸å½±å

æ·±æ·è´çæ°æ§å¯¹è±¡ä¸å±äº«åå­

![æ·±æ·è´ (1).png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31a3a9b3bd1440fd9545a821ba43c3ea~tplv-k3u1fbpfcp-watermark.image?)

è¿æ¶æä»¬å»ä¿®æ¹æ°å¯¹è±¡ä¸­çä»»æå±çº§çä»»æå±æ§å¼ï¼é½ä¸ä¼å¯¹åå¯¹è±¡äº§çå½±åï¼åå¯¹è±¡ä¾ç¶ä¿æä¸å

**ä¸¾ä¸ªæ å­**ð°

```js
let obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
let obj_new = _.cloneDeep(obj_old)
console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```

è¿éæä»¬ä½¿ç¨äº`lodash`å·¥å·åºæä¾ç`_.cloneDeep`æ·±æ·è´æ¹æ³,æ¥çä¸ä¸æ°æ§å¯¹è±¡çå¯¹æ¯

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb3842905a6a4bf1b42a76d95ae0cf4c~tplv-k3u1fbpfcp-watermark.image?)

å¯ä»¥çè§æ°æ§å¯¹è±¡ææå±æ§åå±æ§å¼å®å¨ç¸å

é£åæ¥ç»èå¯¹æ¯ä¸ä¸ï¼ççæ·è´åå¯¹è±¡çå°åæ¯å¦ç¸å

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/16392a4effab427c988ed7fdcfc37f30~tplv-k3u1fbpfcp-watermark.image?)

> obj_old.name === obj_new.nameä¸ºtrueï¼è¿ä¸ªæ¯åºæ¬æ°æ®ç±»åï¼å®å¨ç¸åï¼æ²¡æé®é¢

> obj_old.favorite === obj_new.favoriteï¼è¿éä¸ºfalseï¼å°è¿éå°±åæµæ·è´ä¸åäºï¼æµæ·è´å°è¿ä¸å±çæ¶åï¼å¯¹è±¡å±æ§çå°åæ¯ç¸åçï¼èæ·±æ·è´æ¯å®å¨æ·è´åºä¸ä¸ªæ°çå¯¹è±¡ï¼æä»¥ä¸ç®¡æ¯åªä¸å±ï¼å¯¹è±¡å±æ§çå°åé½æ¯ä¸åç

> obj_old.favorite.drink === obj_new.favorite.drinkä¸ºfalseï¼åå¾æ·±ä¸å±ä»ç¶æ¯falseï¼å³å°åä¸ç¸å

é£åæ¥ä¿®æ¹ä¸ä¸å±æ§å¼ï¼ççååå¯¹æ¯

```js
obj_new.name = 'Jerry'
obj_new.hobby[0] = 'sing'
obj_new.favorite.food = 'cheese'
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bf27bd505e0746f597269d99c3bb92fa~tplv-k3u1fbpfcp-watermark.image?)

ä¿®æ¹å±æ§å¼ä¹åï¼æ°æ§å¯¹è±¡æ¯äºä¸å½±åç

### ð·ï¸æ·±æ·è´çæ¹æ³

é£ä¹ç°å¨å°±æ¥ç½åå ä¸ªæ·±æ·è´çæ¹æ³

#### 1. *éå½å®ç°*

ä½¿ç¨éå½å®ç°åå¯¹è±¡æ¯ä¸å±çæ·è´ï¼å½éå°åºæ¬æ°æ®ç±»åæ¶ï¼ç´æ¥æ·è´ï¼éå°å¼ç¨æ°æ®ç±»åæ¶ï¼éå½æ·è´å®çæ¯ä¸ªå±æ§

ä»£ç å±ç¤º
```js
const obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
const obj_new = {}

function deepClone(newObj, oldObj){
  for (const key in oldObj) {
    if (oldObj[key] instanceof Object) {
      newObj[key] = {}
      deepClone(newObj[key], oldObj[key])
    } else if (oldObj[key] instanceof Array) {
      newObj[key] = []
      deepClone(newObj[key], oldObj[key])
    } else {
      newObj[key] = oldObj[key]
    }
  }
}

deepClone(obj_new, obj_old)

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
æµè¯ç»æ

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

#### 2. *lodashå·¥å·å*

[ç¹è¿éå»lodashçä¸­æææ¡£](https://www.lodashjs.com/)

å¼å¥æååï¼æä»¬ç´æ¥ä½¿ç¨lodashæä¾ç»æä»¬çå½æ°_.cloneDeepå°±è¡

ä»£ç å±ç¤º

```js
let obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
let obj_new = _.cloneDeep(obj_old)

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
æµè¯ç»æ

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

#### 2. *JSON.parse(JSON.stringify(obj))*

`JSON.stringify()` å°JSONæ ¼å¼çå¯¹è±¡è½¬ä¸ºå­ç¬¦ä¸²

`JSON.parse()` å°JSONæ ¼å¼çå­ç¬¦ä¸²è½¬ä¸ºå¯¹è±¡

ä»£ç å±ç¤º

```js
const obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
const obj_new = JSON.parse(JSON.stringify(obj_old))

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
æµè¯ç»æ

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

â£ï¸è½ç¶è¿ä¸ªæ¹æ³æç®åï¼ä»£ç è¡æ°æå°ï¼ä½æ¯å®ä¹æä¸å®çç¼ºé·ï¼

1. æ·è´å¯¹è±¡çå¼ä¸­å¦ææâå½æ°âï¼âundefinedâï¼âsymbolâ
JSON.stringify()åºåååï¼é®å¼å¯¹ä¸¢å¤±

2. æ·è´RegExpä¼åæç©ºå¯¹è±¡{}

3. å¯¹è±¡ä¸­å«æâNaNâï¼âInfinityâä¼åænull

4. æ·è´Dateä¼åæå­ç¬¦ä¸²

## ðï¸ç»è¯­

è¿æ¬¡çæ·±æ·è´æµæ·è´çæ»ç»å°±å°è¿éå¦ï¼åç»­åç°ä¸è¶³çè¯ä¼ç»§ç»­è¡¥åç