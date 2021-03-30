## 【win trade base】app frame

Last edited by **曾华智** 6 months ago

[Page history](http://192.168.0.176:9000/dev_group/win-frond-component/win-micro-web/wikis/【win-trade-base】app-frame/history)

**一、模式**

```
基础框架分为“单页模式”和“多页模式”，通过参数isSingle控制
“单页模式”，通过更新主视图区来实现页面的切换
优势：页面轻巧
劣势：页面每次切换都是重新打开
“多页模式”，每个页面都由一个iframe包裹，各个页面相对独立。
优势：页面相对独立，页面切换不是重新打开
劣势：dom节点较多，对浏览器内存要求较高
```

**二、常用配置**

```
【isSingle】使用“单页模式”或“多页模式”
项目中在index 文件中根据项目的差异性配置不同的属性进行业务上的开发

/**
 * 应用入口
 * @author zhz
 */

import React from 'react';
import ReactDOM from 'react-dom';
import { service, appModel } from 'win-trade-base';
import { MainPort } from 'yss-biz';
import ChildRoutes from './router';
import project from './project.config';
import 'win-trade-base/static/css/main.css';
import 'yss-biz/index.css';
if (!window.singleSpaNavigate) {
  ReactDOM.render(<MainPort ChildRoutes={ChildRoutes} {...project} />, document.getElementById('root'));
}

// 提供基础服务
export const baseConfig = {
  service,
  appModel,
};

注意：project 的配置文件（注意：该配置文件不是必须的，只是方便与业务开发所提供的统一配置入口，业务开发也可以根据props进行传递的方式进行配置）
export default {
  "productName": "赢.投资",//头部产品名称
  "platformName": "中银基金一体化平台",//平台名称
  "platformNameEn": "Asset Management System",//平台英文名称
  // "productLogin": "zy",//登陆模板
  "productMenu": "sideMenu",//产品菜单模式sideMenu
  "isIframe": false,//是否开启iframe 模式
  "tool": {
    "isNew": true,//是否显示提示消息
    "theme": {//显示主题
      isShow: true,
      themeList: []
    },
    "isLockScreen": true//是否显示上锁
  }
}
```

**三、权限控制**

```javascript
<iframe
    width="100%"
    height="100%"
    frameBorder="0"
    scrolling="no"
    allowtransparency="yes"
    title={menuInfo.menuCode}
    key={menuInfo.menuCode}
    id={menuInfo.menuCode}
    src={menuInfo.menuAddress}
    onLoad={this.onLoad}
    ref={ref => this.$iframe = ref} 
/>
onLoad方法
onLoad = e => {
    const { contentDocument } = e.target;

    if (!contentDocument) {
        return;
    }

    contentDocument.onclick = e => {
        //触发父窗体点击事件
        top.window.document.body.click();
    };

    // 请求地址异常
    if (!contentDocument.title) {
        contentDocument.body.style.color = "red";
        return;
    }

    // 增加 menuCode ，ajax 请求头需带上菜单编号
    const { menuInfo } = this.props;
    this.$iframe.contentWindow.menuCode = menuInfo.menuCode;

    this.authController();
};
权限控制逻辑目前由ajax请求改变当前iframe的hash值，然后监听hash变化来渲染按钮权限
（可改造：通过this.$iframe.contentWindow添加方法，然后在每一次请求结束后去执行此方法）
authController = () => {
    const { authData } = this.state;

    this.$iframe.contentWindow.onhashchange = () => {
        if (!authData.menuCode) {
            return;
        }

        // 优先处理子页签按钮的权限，已处理过的打上标签 tabs-func-type
        authData.children.forEach(tabsItem => {
            this.pageAuthRender(tabsItem);
        });

        // 处理菜单级别的按钮权限
        this.pageAuthRender(authData);
    }
};

pageAuthRender = (auth) => {
    const selector = auth.tabFlag === "1" ? `#${auth.menuCode} [func-type]` : "[func-type]:not(.tabs-func-type)";

    this.$iframe.contentDocument.querySelectorAll(selector).forEach($item => {
        const hasAuth = (auth.children && auth.children.find(v => {
            return v.funcType === $item.getAttribute("func-type");
        })) || (auth.funcList && auth.funcList.find(v => {
            return v.funcType === $item.getAttribute("func-type");
        }));

        auth.tabFlag === "1" && $item.classList.add("tabs-func-type");

        if (!hasAuth) {
            $item.style.display = "none";
        }
    });
 };
```