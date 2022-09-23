## 小程序搜索高亮组件

#### highlight  ---适合分词高亮，后端给出高亮结果，前端正则解析高亮

例如搜索：`“半导体时代”`,后端分词给出两个拆分的高亮，后端返回结果和展示结果如下：

```javascript
title: "现在是<span style=color:red>半导体</span>的黄金<span style=color:red>时代</span>"
```
![Snipaste_2022-09-23_16-53-03.png](https://s2.loli.net/2022/09/23/I1Fi5OHYS4XwjNJ.png)


#### highlight-slice ---根据关键词全局匹配字符串高亮

例如搜索：字母`“H”`,后端正常给出，前端根据正则自行匹配高亮，如图

![Snipaste_2022-09-23_16-50-39.png](https://s2.loli.net/2022/09/23/6PaDNQLqrnuk1gA.png)