---
layout: mypost
title: 关于我
---

<script  type="text/javascript" language="javascript">
    
    function siteTime(){
        window.setTimeout("siteTime()", 1000);
        var seconds = 1000;
        var minutes = seconds * 60;
        var hours = minutes * 60;
        var days = hours * 24;
        var years = days * 365;
        var today = new Date();
        var todayYear = today.getFullYear();
        var todayMonth = today.getMonth()+1;
        var todayDate = today.getDate();
        var todayHour = today.getHours();
        var todayMinute = today.getMinutes();
        var todaySecond = today.getSeconds();
        /* Date.UTC() -- 返回date对象距世界标准时间(UTC)1970年1月1日午夜之间的毫秒数(时间戳)
        year - 作为date对象的年份，为4位年份值
        month - 0-11之间的整数，做为date对象的月份
        day - 1-31之间的整数，做为date对象的天数
        hours - 0(午夜24点)-23之间的整数，做为date对象的小时数
        minutes - 0-59之间的整数，做为date对象的分钟数
        seconds - 0-59之间的整数，做为date对象的秒数
        microseconds - 0-999之间的整数，做为date对象的毫秒数 */
        var t1 = Date.UTC(2021,12,05,00,00,00); //北京时间创建网站的时间
        var t2 = Date.UTC(todayYear,todayMonth,todayDate,todayHour,todayMinute,todaySecond);
        var diff = t2-t1;
        var diffYears = Math.floor(diff/years);
        var diffDays = Math.floor((diff/days)-diffYears*365);
        var diffHours = Math.floor((diff-(diffYears*365+diffDays)*days)/hours);
        var diffMinutes = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours)/minutes);
        var diffSeconds = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours-diffMinutes*minutes)/seconds);
        document.getElementById("show_time").innerHTML=diffDays+"天"+diffHours+"小时"+diffMinutes+"分钟"+diffSeconds+"秒***"; //+diffYears+"年"
    }
    siteTime();
</script>

> Hello 陌生人，欢迎访问 Gaoj Blog

该博客托管于 GitHub Page

## 关于我
1. 主业务java开发，当然其它语言也会涉javascript、html、vue、golang、c语言相关（本人近期在研究物联网相关的单片机，所有也有学习）,uniapp开发app以及上架安卓和ios各大应用市场。
2. 佛系开发🙂

## 联系我

- Email&nbsp;: [971004367@qq.com](mailto:971004367@qq.com)

- GitHub: [https://github.com/gaoj-git](https://github.com/gaoj-git)
  
> 网站已运行： <span id="show_time"></span>
