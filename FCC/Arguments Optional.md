Arguments Optional

创建一个计算两个参数之和的 function。如果只有一个参数，则返回一个 function，该 function 请求一个参数然后返回求和的结果。

例如，add(2, 3) 应该返回 5，而 add(2) 应该返回一个 function。

调用这个有一个参数的返回的 function，返回求和的结果：

var sumTwoAnd = add(2);

sumTwoAnd(3) 返回 5。

如果两个参数都不是有效的数字，则返回 undefined。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Closures](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)

[Arguments object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)

add(2, 3) 应该返回 5。

add(2)(3) 应该返回 5。

add("http://bit.ly/IqT6zt") 应该返回 undefined。

add(2, "3") 应该返回 undefined。

add(2)([3]) 应该返回 undefined。


```
一：
如果两个参数中有一个不是Number类型则返回undefined
function add() {
  if(typeof arguments[0] !== "number" || (arguments.length>1 && typeof arguments[1] != "number")){
    return undefined;
  }
  if(arguments.length == 1){
    var arg = arguments[0];
    return function (num) {
      if(typeof num !=="number"){
        return undefined;
      }
      return arg+num;
    };
  }else{
    return arguments[0]+arguments[1];
  }
}

add(2,3);


二：
如果前两个参数都为数字则返回两数之和
function add() {
  if(typeof arguments[0] == "number" && typeof arguments[1] == "number"){
    return arguments[0] + arguments[1];
  }
  if(arguments.length == 1 && typeof arguments[0] == "number"){
    var arg = arguments[0];
    return function (num){
      if(typeof num =="number"){
        return arg+num;
      }
    };
  }
}

add(2,3);

```