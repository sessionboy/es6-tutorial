# 类修饰器Decorator
许多面向对象的语言都有修饰器（Decorator）函数，用来修改类的行为。目前，有一个[提案](https://github.com/tc39/proposal-decorators)将这项功能，引入了 ECMAScript。  

#### 基本使用  
```js
@annotation         // @annotation为修饰器，需要添加在类的顶部，后面不能有符合。
class MyClass { }
  

function annotation(target) {  
   target.annotated = true;  // 给MyClass类添加annotated属性
}    

// annotation为修饰器函数，它接受类为参数(target)，并修改类的行为。
```
> 修饰器函数将类作为参数，并修改类的行为。   

> 修饰器的使用需要[@babel/plugin-proposal-decorators](https://babeljs.io/docs/en/babel-plugin-proposal-decorators)插件的支持。

##### 经典案例——mobx(状态管理器)
```js
import React, { Component } from 'react';
import { inject, observer } from 'mobx-react';  

// inject表示调用缓存,observer表示当缓存数据生效时，刷新当前页面
@inject("store")
@observer
class SchoolComponent extends Component{  

    state={
        schoolname:this.props.store.school.name // store是通过修饰器注入进来的
    }  

    render(){
        return(
            <div>学校：{ this.state.schoolname }</div>
        )
    }
}
export default SchoolComponent;
```
