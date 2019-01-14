# class 类
> es6中的class(类)是es5原型写法的一个语法糖，拥有很好的开发体验

### 一，基本使用
```js
// es5写法
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};
var p = new Point(1, 2);
    

// es6写法
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
const a = new Point(1, 2);
```
> constructor是class的构造函数，当使用new生成实例时，constructor方法会自动调用  

如果constructor没有定义，则默认为空函数。
```js
class Point {
}

// 等同于
class Point {
  constructor() {}
}
```

### 二，在class内定义函数  
```js
class Point {  
    getname(){
        return 1;
    }
}  

// 访问
const P = new Point();
P.getname();
// => 1
```