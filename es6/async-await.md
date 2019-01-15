# async/await 异步终结者
ES2017(es8) 标准引入了 async 函数，使得异步操作变得更加方便。  

`async / await`对应的是generator的`function* / yield`,它是generator的语法糖，大大简化了generator的操作流程，体验更好。

另外async内置执行器，语义更加清晰，且返回promise。

### 一，基本使用    

##### 基本定义  

```js 
async function fn() {  
   const result = await promise ; // 处理异步时，await后面需接promise，比如fetch、axios等
}    

// 调用  
fn();
```    
##### 基本用法
```js
async function getPost() {  
  try {

    const userres = await fetch('./user.json'); // 先获取用户信息
    const user = await userres.json();
    console.log(user);  

    const postres = await fetch('./post.json',{ id: user.id }); // 再根据userId去获取用户的post
    const post = await postres.json();
    console.log(post);  

    // 其他工作
    ...
  }
  catch(err){
    // 异常捕获
    console.log(err);  
  }
}    

// 调用  
getPost();
```    

##### 简写版:  
```js
async function getPost() {  
  try {

    const use = await fetch('./user.json').then(res=>res.json()); // 先获取用户信息
    console.log(user);  

    const postres = await fetch('./post.json',{ id: user.id }).then(res=>res.json()); // 再根据userId去获取用户的post
    console.log(post);  

    // 其他工作
    ...
  }
  catch(err){
    // 异常捕获
    console.log(err);  
  }
}    

// 调用  
getPost();
```    

> await命令后面若是一个 Promise 对象，直接返回该promise对象的结果。如果不是 Promise 对象，就直接返回对应的值。

### 二，多种写法  

```js  

// 1，函数声明
async function fn(){
   // Todo
}


// 2，函数表达式
const foo = async function (){
    // Todo
};


// 3，对象的方法
let obj = { 
    name:"ben",
    age: 23,
    async fn() {
        // Todo
    } 
};  
obj.fn();


// 4，Class类的方法
class Post {

  async getPost(id) {
    const post = await fetch("/api/post",{ postId: id });
    // ...
  }
}
const Posts = new Post();
Posts.getPost('id').then(…);  


// 5，箭头函数
const fn = async () => {
    // ...
};
```

### 三，返回promise  
async函数返回一个 Promise 对象。

async函数内部return语句返回的值，会成为then方法回调函数的参数。    

如果await后面的异步操作出错，那么async函数返回的 Promise 对象就和被reject。

```js
async function getPost() {  
  try {

    const userres = await fetch('./user.json'); // 先获取用户信息
    console.log(user);  

    // 其他工作
  }
  catch(err){
    // 异常捕获
    console.log(err);  
  }
}    

// 调用  
getPost()
 .then(res=>{
    console.log(res);
    return res.json();
 })
 .catch(err=>{
    console.log(err);
 })
```    


### 四，匿名自执行async  
```js
(async () => {
    const response = await fetch('./post.json').then(res=>res.json());
    console.log(response);
})();
```