Steamroller

对嵌套的数组进行扁平化处理。你必须考虑到不同层级的嵌套。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Array.isArray()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)

steamroller([[["a"]], [["b"]]]) 应该返回 ["a", "b"]。

steamroller([1, [2], [3, [[4]]]]) 应该返回 [1, 2, 3, 4]。

steamroller([1, [], [3, [[4]]]]) 应该返回 [1, 3, 4]。

steamroller([1, {}, [3, [[4]]]]) 应该返回 [1, {}, 3, 4]。

```
我先是写了这么一个答案，但是不知道为什么竟然不对（我看输出的结果是对的啊）
var newArr = [];
function steamroller(arr) {
  
  // I'm a steamroller, baby
  for(var i=0;i<arr.length;i++){
    if(Array.isArray(arr[i])){
      steamroller(arr[i]);
    }else{
      newArr.push(arr[i]);
    }
  }
  return newArr;
  
}
steamroller([1, {}, [3, [[4]]]]);

不对就没有办法了，只能改啊~所以就改成了下面这个样子了
 function steamroller(arr) {
    // I'm a steamroller, baby
    var newArr=[];
   function flat(arr){
     for(var i=0;i<arr.length;i++){
       if(Array.isArray(arr[i])){
         flat(arr[i]);
       }else{
         newArr.push(arr[i]);
       }
     }
   }
   flat(arr);
   return newArr;
}
 
 steamroller([1, [], [3, [[4]]]]);
```
