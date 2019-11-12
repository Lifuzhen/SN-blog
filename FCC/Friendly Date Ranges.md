Friendly Date Ranges

让日期区间更友好！  

把常见的日期格式如：YYYY-MM-DD 转换成一种更易读的格式。  

易读格式应该是用月份名称代替月份数字，用序数词代替数字来表示天 (1st 代替 1).   

记住不要显示那些可以被推测出来的信息: 如果一个日期区间里结束日期与开始日期相差小于一年，则结束日期就不用写年份了；在这种情况下，如果月份开始和结束日期如果在同一个月，则结束日期月份也不用写了。  

另外, 如果开始日期年份是当前年份，且结束日期与开始日期小于一年，则开始日期的年份也不用写。  

例如:  

包含当前年份和相同月份的时候，makeFriendlyDates(["2017-01-02", "2017-01-05"]) 应该返回 ["January 2nd","5th"]  

不包含当前年份，makeFriendlyDates(["2003-08-15", "2009-09-21"]) 应该返回 ["August 15th, 2003", "September 21st, 2009"]。 

请考虑清楚所有可能出现的情况，包括传入的日期区间是否合理。对于不合理的日期区间，直接返回 undefined 即可  

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。  

这是一些对你有帮助的资源:            
 
[String.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)  
[String.substr()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substr)  
[parseInt()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)  

makeFriendlyDates(["2017-01-02", "2017-01-05"]) 应该返回 ["January 2nd","5th"].  
makeFriendlyDates(["2017-02-01", "2017-03-03"]) 应该返回 ["February 1st","March 3rd"].  
makeFriendlyDates(["2016-05-11", "2017-04-04"]) 应该返回 ["May 11th, 2016","April 4th"].  
makeFriendlyDates(["2017-07-12", "2018-06-13"]) 应该返回 ["July 12th","June 13th"]  
makeFriendlyDates(["2003-08-15", "2009-09-21"]) 应该返回 ["August 15th, 2003", "September 21st, 2009"].  
makeFriendlyDates(["2010-10-23", "2011-10-22"]) 应该返回 ["October 23rd, 2010","October 22nd"].  
makeFriendlyDates(["2008-10-31", "2009-10-31"]) 应该返回 ["October 31st, 2008","October 31st, 2009"].  
makeFriendlyDates(["2004-11-17", "2005-12-25"]) 应该返回 ["November 17th, 2004","December 25th, 2005"].  
makeFriendlyDates(["2001-12-20", "2001-12-20"]) 应该返回 ["December 20th, 2001"].  
makeFriendlyDates(["2002-12-20", "2001-12-20"]) 不应该返回数组  


```
function makeFriendlyDates(arr) {
 //获得目前的年份
 var yearnow= 2017;
 //把传入的参数放入字符串数组，创建Date类型也可以
 var date1=arr[0].split("-");
 var date2=arr[1].split("-");
 //月份的英文表示
 var months=["January","February","March","April","May","June","July","August","September","October","November","December"];
 //初始化几个后面用到的数组
 var date1str="";
 var date2str="";
 var datearr=[];
 //给日期加后缀的函数
 function friendlydate(str){
  var str2num=Number(str);
   console.log(str);
   if(str2num == 1 || str2num == 21 || str2num == 31){
     return str2num+="st";
   }else if(str2num == 2 || str2num == 22){
     return str2num+='nd';
   }else if(str2num == 3 || str2num ==23){
     return str2num+="rd";
   }else{
     return str2num+='th';
   }
 }
 //date1的字符串表示大部分情况下都是需要年月日的。date2的如果不是在同年同月，大部分情况下都是需要月日的
 date1str=months[date1[1]-1]+" "+friendlydate(date1[2])+", "+date1[0];
 if(date1[1]===date2[1]&&date1[0]===date2[0]){
  date2str=friendlydate(date2[2]);
 }else{
  date2str=months[date2[1]-1]+" "+friendlydate(date2[2]);
 }
 //如果大于一年，date2加上年份；如果小于一年，而且date1的日期是今年，那么去掉date1的年份。
 if((date2[0]-date1[0]>1)||((date2[0]-date1[0]===1)&&(date2[1]-date1[1]>0))||((date2[0]-date1[0]===1)&&(date2[1]-date1[1]===0)&&date2[2]-date1[2]>=0)){
  date2str+=", "+date2[0];
 }else if(date1[0]==yearnow){
  date1str=date1str.slice(0,-6);
 }
 //把两个日期放在同一个数组里输出（如果是同年同月同日，代码里的date2str无用，所以代码是可以改善的）。
 datearr[datearr.length]=date1str;
 if(date1.toString()!==date2.toString()){
  datearr[datearr.length]=date2str;
 }
  
  //如果第二个数组的年份小于第一个数组的年份返回null
  if(date1[0]>date2[0]){
    datearr = null;
  }
 return datearr;
}

makeFriendlyDates(['2016-05-11', '2017-04-04']);

———————————————————————————分割线—————————————————————————————————

function makeFriendlyDates(arr) {
  var months = {     //这里先弄个月份对象
    "01":"January",
    "02":"February",
    "03":"March",
    "04":"April",
    "05":"May",
    "06":"June",
    "07":"July",
    "08":"August",
    "09":"September",
    "10":"October",
    "11":"November",
    "12":"December"
  };
  var date=[],dateArr=[];
  var dateString = "";
  //把arr分割成二维数组
  for(var i=0;i<arr.length;i++){
    date[i] = arr[i];
    date[i] = date[i].split("-");  
  }
 
  //去除不正确日期
  if(date[0][0]>date[1][0])return undefined;
  if(date[0][0]==date[1][0]&&date[0][1]>date[1][1])return undefined;
  if(date[0][0]==date[1][0]&&date[0][1]==date[1][1]&&date[0][2]>date[1][2]) return undefined;
 
 
  var minus = date[1][0] - date[0][0] ;
  //如果年月日都相等
  if(date[0][0]==date[1][0]&&date[0][1]==date[1][1]&&date[0][2]==date[1][2]){
    dateString = months[date[0][1]]+" "+tailOfDay(date[0][2])+", "+date[0][0];
    dateArr.push(dateString) ;   
    return dateArr;
  }
  //如果年月相等
  else if(date[0][0]==date[1][0]&&date[0][1]==date[1][1]){
    dateString = months[date[0][1]]+" "+tailOfDay(date[0][2]);
    dateArr.push(dateString,tailOfDay(date[1][2]));
    return dateArr;
  }
  //如果只有年相等
  else if(date[0][0]==date[1][0]){
    dateString = months[date[0][1]]+" "+tailOfDay(date[0][2]);
    dateArr.push(dateString);
    dateString = months[date[1][1]]+" "+tailOfDay(date[1][2]);
    dateArr.push(dateString);  
    return dateArr;
  }
  else{
    //如果不是当前年份且时间间隔小于一年
    if((date[0][0]!=2017&&date[0][1]>date[1][1])||(date[0][1]==date[1][1]&&date[0][2]>date[1][2])&&minus<=1){
      dateString = months[date[0][1]]+" "+tailOfDay(date[0][2])+", "+date[0][0];
      dateArr.push(dateString) ;     
      dateString = months[date[1][1]]+" "+tailOfDay(date[1][2]);
      dateArr.push(dateString);  
      return dateArr;
    }
    //如果是当前年份且时间间隔小于一年
    else if(date[0][0]==2017 && date[0][1]>date[1][1] && date[1][0]==2018){
      dateString = months[date[0][1]]+" "+tailOfDay(date[0][2]);
      dateArr.push(dateString);
      dateString = months[date[1][1]]+" "+tailOfDay(date[1][2]);
      dateArr.push(dateString);  
      return dateArr;
    }
    //其他
    else{
      dateString = months[date[0][1]]+" "+tailOfDay(date[0][2])+", "+date[0][0];
      dateArr.push(dateString) ;     
      dateString = months[date[1][1]]+" "+tailOfDay(date[1][2])+", "+date[1][0];
      dateArr.push(dateString);  
      return dateArr;
    }
  }
}  
//把日期转换成对应的简便字符串
function tailOfDay(day){
  day = parseInt(day);
  if(day==1||day==21||day==31){
    day = day.toString() + "st";
    return day;
  }
  else if(day==2||day==22){
    day = day.toString() + "nd";
    return day;
  }
  else if(day==3||day==23){
    day = day.toString() + "rd";
    return day;
  }
  else{
    day = day.toString() + "th";
    return day;
  }
}

makeFriendlyDates(['2017-07-12', '2018-06-13']);


```