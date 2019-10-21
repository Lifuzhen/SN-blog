Smallest Common Multiple

[参考](https://github.com/FreeCodeCampChina/freecodecamp.cn/wiki/smallest-common-multiple)

找出能被两个给定参数和它们之间的连续数字整除的最小公倍数。

范围是两个数字构成的数组，两个数字不一定按数字顺序排序。

例如对 1 和 3 —— 找出能被 1 和 3 和它们之间所有数字整除的最小公倍数。

如果你被卡住了，记得开大招 Read-Search-Ask 。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[Smallest Common Multiple](https://www.mathsisfun.com/least-common-multiple.html)

smallestCommons([1, 5]) 应该返回一个数字。

smallestCommons([1, 5]) 应该返回 60。

smallestCommons([5, 1]) 应该返回 60。

smallestCommons([1, 13]) 应该返回 360360。

## 思路提示
1、 由于题目中要判断范围内多个数字的最小公倍数，最简单且暴力的方法就是两两地进行判断

2、 既然需要多次判断，那么我们首先需要封装一个判断函数，用于得出两个数字的最小公倍数。当然，写成递归也是没问题的。或者，用数组的 reduce 方法也行

3、 有一点需要注意。记"求最小公倍数"为 LCM。对于求三个数字 a、b 和 c 的最小公倍数 LCM(a, b, c)，则相当于 LCM(LCM(a, b), c)。由于 LCM 也存在结合律，因此也相当于 LCM(a, LCM(b, c))。所以，先求哪一组都是可以的

```
function smallestCommons(arr) {
   var smaller = Math.min(arr[0], arr[1]);
    var greater = Math.max(arr[0], arr[1]);
    var numArr = [];
    var result = smaller * (smaller + 1);
   
    for (var i = smaller; i <= greater; i++) {
        numArr.push(i);
    }
  function SCM(left, right){
    if(left === 0 || right === 0){
      return 0;
    }
    if(left === right){
      return left;
    }
    var scm = right;
    while(scm <= right*left){
      if(scm % left === 0){
        return scm;
      }
      scm += right;
    }
  }
    for (var j = 2; j < numArr.length; j++) {
        result = SCM(numArr[j], result);
    }
  return result;
  
}

smallestCommons([1,5]);

------------------------------------②🎈-------------------------------------------------------

function smallestCommons(arr) {
    var smaller = Math.min(arr[0], arr[1]);
    var greater = Math.max(arr[0], arr[1]);
    var numArr = [];
    
    for (var i = smaller; i <= greater; i++) {
        numArr.push(i);
    }
    
    function SCM(left, right) {
        // ...
    }
    
    // 初始值设为 1 就好，因为任何数与 1 的最小公倍数都是这个数本身
    return numArr.reduce(function(previous, next) {
        return SCM(previous, next)
    }, 1);
}

```

## 数学方法
·有一种计算最小公倍数的数学方法，但要先计算出最大公约数。详情可以参考最小公倍数的维基百科词条
 ·计算最大公约数，有一种比较快捷的方法叫辗转相除法
 ·简单举个例子，对于数字 a 和 b，若要求他们的最大公约数，则将较大数不断减去较小数，直到所得的差小于较小数。重复此步骤，直到差为 0，此时较小数即为最大公约数，伪代码如下：
```
while(b !== 0)
    temp = b
    b = a % b
    a = temp
return a
```
·有朋友可能觉得这里需要处理特殊值。但由于任何数都可以整除 0，因此 0 与任何数的最大公约数都为那个数本身。所以，不需要进行特殊处理
·根据维基百科，任何两个整数的最大公约数与最小公倍数存在如下关系：

```
LCM(a, b) = |a * b| / GCD(a, b)
```
·其中，LCM 为最小公倍数，GCD 为最大公约数。同样，这个可以推论到 n 个数的情况，即：
```
LCM(A1, A2, A3, ...) = ∏(An) / GCD(A1, A2, A3, ...)
```

#### 代码
```
function smallestCommons(arr) {
    if (arr.length !== 2) return;

    var smaller = Math.min.apply(null, arr);
    var greater = Math.max.apply(null, arr);
    var result = 1;
    
    function getGCD(a, b) {
        while (b !== 0) {
            var temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
    
    while (smaller <= greater) {
        result = smaller * result / getGCD(smaller, result);
        smaller++;
    }
    
    return result;
}
```