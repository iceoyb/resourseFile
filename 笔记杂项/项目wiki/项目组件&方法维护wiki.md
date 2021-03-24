---

### 1、toTableColumns--表格展示转换方法(自定义列)

-  将后端返回数据处理成表格可使用的columns的公共方法

```javascript
// 公共请求部分代码
import {  getColumns } from "../services";
import {  toTableColumns } from "ta-biz";
export default {  
  /**主界面表头 */
  async httpGetFundColumns(state, params, { getState, mutations }) {
    let sendData = { ...params };
    if (sendData.hasOwnProperty("bool")) {
      delete sendData.bool;
    }
    let result = await getColumns(sendData);
    if (result.code === "200") {
      // 拿到数据后做处理
      let visibleColumns =
        result.data.filter((item) => item.visible === "1") || [];
        /*调用toTableColumns将后端返回数据处理成表格可使用的columns*/ 
      let fundColumns = toTableColumns(handleEditCols(visibleColumns));
      let columnsList = handleEditCols(result.data);
      if (params.bool) {
        let addParams = {};
        mutations.asyncHttpGetFundPage({
          ...addParams,
          menuCode: params.menuCode,
        }); //获取当前翻页数据
        mutations.asyncHttpGetFundAllColumns({ menuCode: params.menuCode });
      }
      state = getState();
      return state.merge({
        fundColumns,
        columnsList,
      });
    }
  },
  // ...
};

```

- toTableColumns参数说明

| 参数名 | 功能说明                   | 类型              | 默认值         |
| ------ | -------------------------- | ----------------- | -------------- |
| cols   | 后端接口返回的自定义列数据 | Array（数组对象） | [{},{},...,{}] |
- cols数组对象参数说明

| 参数名     | 功能说明                                                     | 类型   | 备注                                                         |
| ---------- | ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| fieldName  | 展示字段中文名--对应表格列的title属性                        | string | 无                                                           |
| field      | 展示字段英文名--对应表格列的dataIndex属性                    | string | 无                                                           |
| dataSize   | 展示字段宽度--对应表格列的dataIndex属性                      | number | 无                                                           |
| dataType   | 展示字段数据类型--根据不同类型决定如何渲染，如何进行排序，字段的居左居中居右等 | string | "n"--数值型，"d"--日期型，"dic"--字典（状态）型，"m"--金额型，"r"--利率型  其他数据暂不支持 |
| dataPrec   | 展示字段精确位                                               | number | 只有dataType为"n","m","r"该字段才生效                        |
| dateFormat | 用于展示日期的格式化                                         | string | 常规值："YYYY-MM-DD","HH:mm:ss","YYYY-MM-DD HH:mm:ss"等      |

---

