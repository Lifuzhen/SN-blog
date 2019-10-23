Finders Keepers

写一个 function，它遍历数组 arr，并返回数组中第一个满足 func 返回值的元素。举个例子，如果 arr 为 [1, 2, 3]，func 为 function(num) {return num === 2; }，那么 find 的返回值应为 2。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Array.filter()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

find([1, 3, 5, 8, 9, 10], function(num) { return num % 2 === 0; }) 应该返回 8。

find([1, 3, 5, 9], function(num) { return num % 2 === 0; }) 应该返回 undefined。

```
function find(arr, func) {
  var sum;
  for(var i=0;i<arr.length;i++){
    if(func(arr[i])){
      sum = arr[i];
      break;
    }
  }
  return sum;
}

find([1, 2, 3, 4], function(num){ return num % 2 === 0; });

```