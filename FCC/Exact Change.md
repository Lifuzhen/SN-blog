Exact Change  
设计一个收银程序 checkCashRegister() ，其把购买价格(price)作为第一个参数 , 付款金额 (cash)作为第二个参数, 和收银机中零钱 (cid) 作为第三个参数.  

cid 是一个二维数组，存着当前可用的找零.  

当收银机中的钱不够找零时返回字符串 "Insufficient Funds". 如果正好则返回字符串 "Closed".  

否则, 返回应找回的零钱列表,且由大到小存在二维数组中.  

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。  

这是一些对你有帮助的资源:  

[Global Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)  

checkCashRegister(19.50, 20.00, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.10], ["QUARTER", 4.25], ["ONE", 90.00], ["FIVE", 55.00], ["TEN", 20.00], ["TWENTY", 60.00], ["ONE HUNDRED", 100.00]]) 应该返回一个数组.  
checkCashRegister(19.50, 20.00, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 应该返回一个字符串.  
checkCashRegister(19.50, 20.00, [["PENNY", 0.50], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 应该返回一个字符串.  
checkCashRegister(19.50, 20.00, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.10], ["QUARTER", 4.25], ["ONE", 90.00], ["FIVE", 55.00], ["TEN", 20.00], ["TWENTY", 60.00], ["ONE HUNDRED", 100.00]]) 应该返回 [["QUARTER", 0.50]].  
checkCashRegister(3.26, 100.00, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.10], ["QUARTER", 4.25], ["ONE", 90.00], ["FIVE", 55.00], ["TEN", 20.00], ["TWENTY", 60.00], ["ONE HUNDRED", 100.00]]) 应该返回 [["TWENTY", 60.00], ["TEN", 20.00], ["FIVE", 15], ["ONE", 1], ["QUARTER", 0.50], ["DIME", 0.20], ["PENNY", 0.04]].  
checkCashRegister(19.50, 20.00, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 应该返回 "Insufficient Funds".  
checkCashRegister(19.50, 20.00, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 1.00], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 应该返回 "Insufficient Funds".  
checkCashRegister(19.50, 20.00, [["PENNY", 0.50], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 应该返回 "Closed".    

```
    function checkCashRegister(price, cash, cid) {
      var change = cash - price;//找的钱
      var arr = [];
      var j=0;
      var array = [0.01,0.05,0.1,0.25,1,5,10,20,100];//对应cid[i][0]
      var total = 0;
      var money = change;                    
    
      for(var i=cid.length-1;i>=0;i--){
          total += cid[i][1];//总钱数
          //cid[i][0]:PENNY单位,cid[i][1]:1.01总数
          if(change > array[i] && cid[i][1]>0){//
              var c = parseInt(change/array[i]);//可以找多少张这个钱
    
    //如果change中可以找的这个钱的金额，比实际这个金额的钱大,说明可以将现有的钱找完，cid[i]应该放到数组中
    //如果小，则将change可以找的金额放进去
              if(c*array[i] > cid[i][1]){
                  change -= cid[i][1];
              }else{
                  change -= c*array[i];
                  cid[i][1] = c*array[i];
              }
              change = change.toFixed(2);//四舍五入，保留两位小数
    
              //arr.push(cid[i]);
              arr[j] = cid[i];
              j++;
          }
    
      }
    
      if(total == money){//总钱数等于要找的钱，closed
          return "Closed";
      }else if(total < money || change != 0){//总钱数小于要找的钱，或者不能找整
          return "Insufficient Funds";
      }
    
      return arr;
    }
    
    // Example cash-in-drawer array:
    // [["PENNY", 1.01],
    // ["NICKEL", 2.05],
    // ["DIME", 3.10],
    // ["QUARTER", 4.25],
    // ["ONE", 90.00],
    // ["FIVE", 55.00],
    // ["TEN", 20.00],
    // ["TWENTY", 60.00],
    // ["ONE HUNDRED", 100.00]]
    
    checkCashRegister(19.50, 20.00, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.10], ["QUARTER", 4.25], ["ONE", 90.00], ["FIVE", 55.00], ["TEN", 20.00], ["TWENTY", 60.00], ["ONE HUNDRED", 100.00]]);

```
