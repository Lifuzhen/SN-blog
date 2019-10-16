给一个正整数num，返回小于或等于num的斐波纳契奇数之和。

斐波纳契数列中的前几个数字是 1、1、2、3、5 和 8，随后的每一个数字都是前两个数字之和。

例如，sumFibs(4)应该返回 5，因为斐波纳契数列中所有小于4的奇数是 1、1、3。

提示：此题不能用递归来实现斐波纳契数列。因为当num较大时，内存会溢出，推荐用数组来实现。

参考文档：[博客园](https://www.cnblogs.com/meteoric_cry/archive/2010/11/29/1891241.html)，[Issue](https://github.com/FreeCodeCampChina/freecodecamp.cn/issues/19)

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Remainder](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Remainder_(.25))


sumFibs(1) 应该返回一个数字。

sumFibs(1000) 应该返回 1785。

sumFibs(4000000) 应该返回 4613732。

sumFibs(4) 应该返回 5。

sumFibs(75024) 应该返回 60696。

sumFibs(75025) 应该返回 135721。

```
function sumFibs(num) {
  var arr =[1,1];
  var sum = 2;
  if(num >= arr.length){
    for(var i=arr.length;i<num;i++){
     arr[i] = arr[i - 2] + arr[i - 1];
     var tmp = arr[i] % 2 != 0 && arr[i]<=num ? arr[i] : 0;
     sum+= tmp;
    }
  }else{
    sum = 1;
  }
  console.log(sum);
  return sum;
}

sumFibs(4);
```