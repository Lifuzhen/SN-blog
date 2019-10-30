Symmetric Difference  
创建一个函数，接受两个或多个数组，返回所给数组的 对等差分(symmetric difference) (△ or ⊕)数组.

给出两个集合 (如集合 A = {1, 2, 3} 和集合 B = {2, 3, 4}), 而数学术语 "对等差分" 的集合就是指由所有只在两个集合其中之一的元素组成的集合(A △ B = C = {1, 4}). 对于传入的额外集合 (如 D = {2, 3}), 你应该安装前面原则求前两个集合的结果与新集合的对等差分集合 (C △ D = {1, 4} △ {2, 3} = {1, 2, 3, 4}).  

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。  

这是一些对你有帮助的资源:  

[Array.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)  
[Symmetric Difference](https://www.youtube.com/watch?v=PxffSUQRkG4)  

sym([1, 2, 3], [5, 2, 1, 4]) 应该返回 [3, 4, 5].  
sym([1, 2, 3], [5, 2, 1, 4]) 应该只包含三个元素.  
sym([1, 2, 5], [2, 3, 5], [3, 4, 5]) 应该返回 [1, 4, 5]  
sym([1, 2, 5], [2, 3, 5], [3, 4, 5]) 应该只包含三个元素.  
sym([1, 1, 2, 5], [2, 2, 3, 5], [3, 4, 5, 5]) 应该返回 [1, 4, 5].  
sym([1, 1, 2, 5], [2, 2, 3, 5], [3, 4, 5, 5]) 应该只包含三个元素.  
sym([3, 3, 3, 2, 5], [2, 1, 5, 7], [3, 4, 6, 6], [1, 2, 3]) 应该返回 [2, 3, 4, 6, 7].  
sym([3, 3, 3, 2, 5], [2, 1, 5, 7], [3, 4, 6, 6], [1, 2, 3]) 应该只包含五个元素.  
sym([3, 3, 3, 2, 5], [2, 1, 5, 7], [3, 4, 6, 6], [1, 2, 3], [5, 3, 9, 8], [1]) 应该返回 [1, 2, 4, 5, 6, 7, 8, 9].  
sym([3, 3, 3, 2, 5], [2, 1, 5, 7], [3, 4, 6, 6], [1, 2, 3], [5, 3, 9, 8], [1]) 应该只包含八个元素. 

```
    function sym(args) {
      var newArr = [];
      // 1.用数组接收所有参数
      for(var i=0;i<arguments.length;i++){
        newArr.push(arguments[i]);
      }
        // 2.为每个参数数组去除重复项                                                                                                                    
      for(var j=0;j<newArr.length;j++){
        newArr[j] = newArr[j].filter((item,index)=>{
          return newArr[j].indexOf(item) == index;
        });
      }
       // 3.归并所有参数数组到最后一个参数 
      newArr.reduce((pre,cur)=>{
        pre.forEach((z)=>{
          if(cur.indexOf(z) == -1){
            cur.push(z);
          }else{
            cur.splice(cur.indexOf(z),1);
          }
        });
        return cur;
      });
      // 4.返回最后一个参数       
      return newArr[newArr.length-1];
    }
    
    sym([1, 2, 3], [5, 2, 1, 4]);
    
    2、传入n个数组，先将每个数组去重,然后将数组1与数组2去重，得到的结果再与数组3去重
    function sym(args) {
      var arr = []; //存放传入的参数
      for(var i = 0; i < arguments.length; i++){
        arr.push(arguments[i]);
    
        //数组中的每一项分别去重
        arr[i] = arr[i].filter(function(item,index,array){
          return array.indexOf(item,index+1) === -1; //若该元素之后再查不到该元素的位置，表示该元素之后没有与之相同的元素
        });
      }
      var result = arr[0];
      for(var i = 1; i < arr.length; i++){
        result = result.concat(arr[i]);
    
        result = result.filter(function(item,index,array){
          return array.indexOf(item) === array.lastIndexOf(item);
        }); 
    
      }
    
      return result;
    }
   
```