# generator异步编程

### 一，基本使用    

##### 定义generator函数    
 定义generator函数需要使用`fuction*`关键字，并且函数内可使用`yield`关键字来处理异步操作，感官上是相当于同步的。
```js
  function* fn(){
      const result = yield fetch('./post.json'); // 执行完后才会执行下一行代码，感官上相当于同步
      console.log(result);
  }
```  
在对象或class中定义可简写：  
```js
  // 在对象中定义  
  const obj = {
    username: "ben",
    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
    // 或
    *
  }  

  // 在class中定义  
  class App {  

    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
  }
```

##### generator原生用法  
调用generator对象有两个方法:    

一是不断地调用generator对象的next()方法  

二是直接用for ... of循环迭代generator对象
```js
 function* fn(){
    const result = yield fetch('./post.json');  // 同步执行
    console.log(result);
 }  
  
// 1，使用next调用generator函数
const g = fn();
const result = g.next();
result.value.then(function(data){
  return data.json();
}).then(function(data){
  g.next(data);
});    
  

// 2，使用`for of`调用generator函数
for (let v of fn()) {
  console.log(v);
}

```  

##### 使用co模块简化流程  
```js
co(function *(){
  try {
    const result = yield fetch('./post.json');  // 同步执行
    console.log(result);
  } 
  catch (err) {
    console.error(err);
 }
})
.catch(err=>{
    console.log(err);
});

```

