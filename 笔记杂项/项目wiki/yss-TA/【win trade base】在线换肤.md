## 【win trade base】在线换肤

Last edited by **曾华智** 6 months ago

[Page history](http://192.168.0.176:9000/dev_group/win-frond-component/win-micro-web/wikis/【win-trade-base】在线换肤/history)

**方案：通过iframe 直接操作dom的方式**

\##不存在iframe 跨域问题

\##步骤如下：

\##1 》交易平台通过webpack打包三套不同的主题样式，默认情况下前端基础框架通过iframe的onLoda方法加载默认的一套主题样式

\##2》当用户点击皮肤选择其中的一套样式的话，基础框架通过渲染dom的方式直接给iframe窗体下body标签添加一个样式类，达到全体换肤的效果

\##3》（win-trade-base 默认提供三套组件样式 最外层类名分别是：theme-blue-black（星空蓝）theme-blue-white（蓝白）theme-red-theme）（红白）

\##4》该四套样式不影响现在已经有的项目样式

\##5》项目中如果需要增加一套主题功能则需要在项目中收动开启换肤功能

开启如下：

```
export default {
  "tool": {
    "theme": {//显示主题
      isShow: true,
      themeList: []
    },
  }
}
theme:{
   isShow: true, //是否开启主题
   themeList: [{ "name": "星空蓝", "className": "darkBlue" }, { "name": "亮红", "className": "lightRed" }, { 
   "name": "亮蓝", "className": "lightBlue" }],
}

注意：themeList：采用项目上覆盖原win-trade-base 的方式样式覆盖

项目中组件样式规范

以时间组件为例：
最外层套一个需要根据换色的类  .lightRed 类
```

.lightRed{ .ant-picker-calendar { background-color: #F9DADC} .treeExpand{ span{ color: #222; } } }