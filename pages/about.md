---
layout: mypost
title: 关于我
---

> Hello 陌生人，欢迎访问 Gaoj Blog

该博客托管于 GitHub Page

## 关于我
1. 主业务java开发，当然其它语言也会涉javascript、html、vue、golang、c语言相关（本人近期在研究物联网相关的单片机，所有也有学习）,uniapp开发app以及上架安卓和ios各大应用市场。
2. 佛系开发🙂

## 联系我

- Email&nbsp;: [971004367@qq.com](mailto:971004367@qq.com)

- GitHub: [https://github.com/gaoj-git](https://github.com/gaoj-git)
  
> 网站已运行： <span id="show_time"></span>


<script>
		function secondToDate(second) {
				if (!second) {
					return 0;
				}
				var time = new Array(0, 0, 0, 0, 0);
				if (second >= 365 * 24 * 3600) {//计算年
					time[0] = parseInt(second / (365 * 24 * 3600));
					second %= 365 * 24 * 3600;
				}
				if (second >= 24 * 3600) {//计算天
					time[1] = parseInt(second / (24 * 3600));
					second %= 24 * 3600;
				}
				if (second >= 3600) {//计算时
					time[2] = parseInt(second / 3600);
					second %= 3600;
				}
				if (second >= 60) {//计算分
					time[3] = parseInt(second / 60);
					second %= 60;
				}
				if (second > 0) {//计算秒
					time[4] = second;
				}
				return time;
			}
			function setTime() {
				var create_time = Math.round(new Date(Date.UTC(2022, 5, 1, 0, 0, 0)).getTime() / 1000);//设置起始时间为2017年1月1日0点整，注意月份取值是0-11。
				var timestamp = Math.round((new Date().getTime() + 8 * 60 * 60 * 1000) / 1000);
				currentTime = secondToDate((timestamp - create_time));
				currentTimeHtml = currentTime[0] + '年' + currentTime[1] + '天' + currentTime[2] + '时' + currentTime[3] + '分' + currentTime[4] + '秒';
				document.getElementById("show_time").innerHTML = currentTimeHtml;
			}
			setInterval(setTime, 1000);
	</script>