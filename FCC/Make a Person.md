Make a Person  
用下面给定的方法构造一个对象.  

方法有 getFirstName(), getLastName(), getFullName(), setFirstName(first), setLastName(last), and setFullName(firstAndLast).

所有有参数的方法只接受一个字符串参数.

所有的方法只与实体对象交互.

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。

这是一些对你有帮助的资源:

[Closures](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)  
[Details of the Object Model](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Details_of_the_Object_Model)  

Object.keys(bob).length 应该返回 6.  
bob instanceof Person 应该返回 true.  
bob.firstName 应该返回 undefined.  
bob.lastName 应该返回 undefined.  
bob.getFirstName() 应该返回 "Bob".  
bob.getLastName() 应该返回 "Ross".  
bob.getFullName() 应该返回 "Bob Ross".  
bob.getFullName() 应该返回 "Haskell Ross" after bob.setFirstName("Haskell").  
bob.getFullName() 应该返回 "Haskell Curry" after bob.setLastName("Curry"). 
bob.getFullName() 应该返回 "Haskell Curry" 在 bob.setFullName("Haskell Curry") 之后.  
bob.getFirstName() 应该返回 "Haskell" 在 bob.setFullName("Haskell Curry") 之后.  
bob.getLastName() 应该返回 "Curry" 在 bob.setFullName("Haskell Curry") 之后.  


```
var Person = function(firstAndLast) {
    this.getFirstName = function(){
      return firstAndLast.split(" ")[0];
    };
  this.getLastName = function(){
    return firstAndLast.split(" ")[1];
  };
  this.getFullName = function(){
    return firstAndLast;
  };
  this.setFirstName = function(first){
    firstAndLast = firstAndLast.replace(firstAndLast.split(" ")[0],first);
  };
  this.setLastName = function(last){
    firstAndLast = firstAndLast.replace(firstAndLast.split(" ")[1],last);
  };
  this.setFullName = function(fullName){
    firstAndLast = fullName;
  };
  return firstAndLast;
};

var bob = new Person('Bob Ross');
bob.getFullName();

```