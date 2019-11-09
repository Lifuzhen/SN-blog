No repeats please  
把一个字符串中的字符重新排列生成新的字符串，返回新生成的字符串里没有连续重复字符的字符串个数.连续重复只以单个字符为准  
 
例如, aab 应该返回 2 因为它总共有6中排列 (aab, aab, aba, aba, baa, baa), 但是只有两个 (aba and aba)没有连续重复的字符 (在本例中是 a).  

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。  

这是一些对你有帮助的资源:  

[Permutations](https://www.mathsisfun.com/combinatorics/combinations-permutations.html)  
[RegExp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)  

permAlone("aab") 应该返回一个数字.  
permAlone("aab") 应该返回 2.  
permAlone("aaa") 应该返回 0.  
permAlone("aabb") 应该返回 8.  
permAlone("abcdefa") 应该返回 3600.  
permAlone("abfdefa") 应该返回 2640.  
permAlone("zzzzzzzz") 应该返回 0.  

```
function permAlone(str) {
 var arr=str.split("");
 var perarr=[];
 var begin=0;
 //创建正则，如果字符串全重复，则直接return 0
 var reg = /(.)\1+/g;
 if(str.match(reg)!==null&&str.match(reg)[0]===str){
  return 0;
 }
  //用于交换的函数
 function swap(idx1,idx2){
   var temp=arr[idx1];
   arr[idx1]=arr[idx2];
   arr[idx2]=temp;
 }
 //如果begin到了最后一个字符，可以将这个字符串加入到全排列数组中了
 function permall(arr,begin){
  if(begin==arr.length-1){
   perarr[perarr.length]=arr.join("");
   return;
  }
  for(var i=0;(i+begin)<arr.length;i++){
   swap(begin,begin+i);
   permall(arr,begin+1);
   swap(begin,begin+i);
  }
 }
 permall(arr,begin);
 //返回相邻不重复的数量
 return perarr.filter(function(val) {
   return !val.match(reg);
 }).length;
  
}

permAlone('aab');

```