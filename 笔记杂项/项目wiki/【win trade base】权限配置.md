## 【win trade base】权限配置

Last edited by **曾华智** 6 months ago

[Page history](http://192.168.0.176:9000/dev_group/win-frond-component/win-micro-web/wikis/【win-trade-base】权限配置/history)

**一、菜单按钮权限配置**

```
1、子页签需要配置菜单编号作为 “id”（系统菜单添加菜单时自动产生），元素坐标（Tabs.TabPane）
<Tabs.TabPane
    tab={menuItem.title}
    key={menuItem.keys}
    id={menuItem.keys}
>
    {<menuItem.component {...this.props} />}
</Tabs.TabPane>
2、新增、修改、删除按钮配置属性 “func-type={constant.ADD}”，constant 常量从 win-trade-base 中读取
import { constant } from "win-trade-base";

<Button func-type={constant.ADD} >新增</Button>
```

**二、菜单接口请求配置**

```
1、新增、修改、删除接口请求配置增加 headers 增加功能类型入参，字段暂未确定
getCapitalAcctInfo(params) {
    return service.httpService({
        baseURL: service.dfbpBaseManage,
        url: '/capitalAccount/list',
        method: 'post',
        data: params,
        headers: {
            // 功能类型
        }
     });
};
```

**二、菜单接口请求配置**

```
    在项目开发中，开发人员无需对按钮组件进行权限的控制，我们将会在yss-trade-base组件包中暴露withRoleTableBotton
，withRoleBotton这两个组件。该组件会根据当前的用户判断是否有该按钮权限。（本方法是采用dom二次渲染的机制重新对按钮进行一个现实和隐藏的效果
该实现的方案弊端是1.对dom元素进行二次的渲染重绘2.根据请求的延时性可能出现按钮演示隐藏不及时的弊端
项目中使用方式：

通过项目中的 functionRolue 暴露出的属性与按钮进行匹配

 /***按钮组***/
import {functionRolue } from yss-biz

声明：

    const ButtonType = [
      {
        name: '新增',
        roule: functionRolue.ADD
      },
      {
        name: '导入',
        // roule: functionRolue.EXPORT,
      },
      {
        name: '导出',
        // roule: functionRolue.EXPORT,
      }
    ];


 /***表格行按钮组***/
    const ButtonTableType = [
      {
        name: '编辑',
        roule: functionRolue.edit
      }
    ];

使用：

withRoleBotton(ButtonType, "primary")
如果：项目中为采用withRoleTableBotton，withRoleBotton这两个组件，需要开发人员自己在按钮配置一下
如下图：
<Button func-type={constant.ADD} >新增</Button>
```