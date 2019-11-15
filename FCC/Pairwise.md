Pairwise  
到你的另一半

都说优秀的程序员擅长面向对象编程，但却经常找不到另一半，这是为什么呢？因为你总是把自己局限成为一个程序员，没有打开自己的思维。

这是一个社群的时代啊，在这里你应该找到与你有相同价值观但又互补的另一半。

譬如：你编程能力强，估值11分，如果以20分为最佳情侣来计算，你应该找一个设计能力强，估值为9分的女生。

那么当你遇到一个设计能力为9分的女生，千万别犹豫，大胆去表白。千万别以为后面的瓜比前面的甜哦。

举个例子：有一个能力数组[7,9,11,13,15]，按照最佳组合值为20来计算，只有7+13和9+11两种组合。而7在数组的索引为0，13在数组的索引为3，9在数组的索引为1，11在数组的索引为2。

所以我们说函数：pairwise([7,9,11,13,15],20) 的返回值应该是0+3+1+2的和，即6。

我们可以通过表格来更直观地查看数组中索引和值的关系：

Index	0	1	2	3	4  
Value	7	9	11	13	15  
任务：帮右边的pairwise函数实现上面的功能。              

当你遇到困难的时候，记得开大招'Read-Search-Ask'。  

这是一些对你有帮助的资源:  

[Array.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)  
我还用到了  
[Array.splice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

pairwise([1, 4, 2, 3, 0, 5], 7) 应该返回 11.  
pairwise([1, 3, 2, 4], 4) 应该返回 1.  
pairwise([1, 1, 1], 2) 应该返回 1.  
pairwise([0, 0, 0, 0, 1, 1], 1) 应该返回 10.  
pairwise([], 100) 应该返回 0.  

```
function pairwise(arr, arg) {
  if(arr.length == 0) return 0;
  var indexArr = [];
  out:
  for(var i=0;i<arr.length;i++){
    for(var j=i+1;j<arr.length;j++){
      if(arr[i]+arr[j] == arg){
        indexArr.push(i);
        indexArr.push(j);
        arr.splice(i,1,undefined);
        arr.splice(j,1,undefined);
        continue out;
      }
    }
  }
  console.log(indexArr.reduce((a,b)=>a+b));
  return indexArr.reduce((a,b)=>a+b);
}

pairwise([1, 1, 1], 2);

```