# Sorted Union
写一个 function，传入两个或两个以上的数组，返回一个以给定的原始数组排序的不包含重复值的新数组。

换句话说，所有数组中的所有值都应该以原始顺序被包含在内，但是在最终的数组中不包含重复值。

非重复的数字应该以它们原始的顺序排序，但最终的数组不应该以数字顺序排序。

请参照下面验证判断中的例子。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Arguments object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)

[Array.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

例子：

unite([1, 3, 2], [5, 2, 1, 4], [2, 1]) 应该返回 [1, 3, 2, 5, 4]。

unite([1, 3, 2], [1, [5]], [2, [4]]) 应该返回 [1, 3, 2, [5], [4]]。

unite([1, 2, 3], [5, 2, 1]) 应该返回 [1, 2, 3, 5]。

unite([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]) 应该返回 [1, 2, 3, 5, 4, 6, 7, 8]。



```
一：

function unite(arr1, arr2, arr3) {
  let arr = [];
  let newArr = Array.prototype.reduce.call(arguments,function(acc,cur){
    return Array.prototype.concat(acc,cur);
  });
  newArr.filter((x)=>{
    if(arr.indexOf(x) == -1){
      arr.push(x);
    }
  });
  return arr;
}

unite([1, 3, 2], [1, [5]], [2, [4]]);


二：

function unite(arr1, arr2, arr3) {

  return [].slice.call(arguments).reduce(function(prev,next){
      return prev.concat(next.filter(e => prev.indexOf(e) === -1));
    },[]);
  
}
//[].slice.call(arguments)将所有数组放入一个数组中。
unite([1, 3, 2], [1, [5]], [2, [4]]);
```