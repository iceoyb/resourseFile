###	TA-项目业务使用常量维护&&使用
####	1.functionRolue--功能权限(src/yss-biz-utils-util/constant.js)

​	配置如下：(形如	功能:"function"	功能为业务代码中按钮的name，funciton为后端指定的权限值)

```javascript
export const functionRolue = {
  查询: 'QUERY', //查询
  新增: 'ADD', //新增
  修改: 'UPDATE', //修改
  删除: 'DELETE', // 删除
  审核: 'CHECK', //审核
  反审核: 'UNCHECK', //反审核
  打印: 'PRINT', //打印
  导入: 'IMPORT', //导入
  导出: 'EXPORT', //导出
  审批通过: 'APPROVED', //审批通过
  审批拒绝: 'APPROVED_REJECT', //  审批拒绝
  其他操作: 'OTHER_OPERATION', //其他操作
  添加: 'ADD', //新增
  详情: 'DETAIL',
  批量通过: 'APPROVED',
  批量驳回: 'APPROVED_REJECT',
  复核:'APPROVED',
  通过: 'APPROVED',
  驳回: 'APPROVED_REJECT',
  复制新增: 'COPY_ADD',
  复制: 'COPY_ADD',
  提交: 'SUBMIT',
  批量删除: 'BATCH_DELETE',
  标记为已读: 'MARK_READ',
  数据比对:'DATA_COMPARE',
  查询条件设置:'CONDITION_SETTING',
  输出列设置:'FIELD_OUTPUT'
};
```

​	用法：

```javascript
/**操作栏按钮组**/
const ActionButtonType = [
  {
    name: "详情",/**此处为functionRolue中定义的功能(中文)**/
    ...,
  },
];
/**展示列--表格**/
let columns = [
  {
    ...,
    render: (row) => withRoleTableBotton([...ActionButtonType])(row),//调用withRoleTableBotton
  },
];
```

