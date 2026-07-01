# 浏览器工作流 + 每日自动收集

## 读取真实岗位（Claude in Chrome）
在候选人已登录的浏览器里操作。列表页可稳定读取(标题/公司/经验/链接)；详情页有反爬会卡死——不硬刷。投递/发送每条需本人确认，绝不自动群发、不代填账号密码。

## 每日自动收集（Chrome 定时任务）
把下面这段设成 Chrome 扩展的定时快捷任务(每早跑)。它只做"收集+预筛+输出列表"，不投递：

```
每天在 Boss 直聘依次打开这些搜索链接，提取每个岗位的[职位/公司/经验要求/链接]，汇总成一个表格：
https://www.zhipin.com/web/geek/job?query=投资者关系&city=101020100
https://www.zhipin.com/web/geek/job?query=IR&city=101020100
https://www.zhipin.com/web/geek/job?query=证券事务代表&city=101020100
https://www.zhipin.com/web/geek/job?query=董事会秘书&city=101020100
https://www.zhipin.com/web/geek/job?query=投后管理&city=101020100
https://www.zhipin.com/web/geek/job?query=募资&city=101020100
https://www.zhipin.com/web/geek/job?query=投融资&city=101020100
规则：剔除经验要求为"5-10年"或"10年以上"的岗位；剔除标题含"FA/PE/VC背景""美元基金""保荐代表人"的岗位；输出为表格并保存/展示。不要投递、不要发消息。
```

设置步骤见 README。收集结果由 Claude 打分入池(更新 web/jobs.js)，候选人本人投递。
