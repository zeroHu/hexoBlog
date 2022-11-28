---
title: table2excel table 转为excel js处理
date: 2017-07-31 18:05:45
tags: javascript
---
### table转为excel表格
> 需要借助jQuery

```html
<!DOCTYPE HTML>
<html>

<head>
  <script src="http://cdn.bootcss.com/jquery/2.2.1/jquery.min.js"></script>
</head>

<body>
  <table id="targetTable">
    <tbody>
      <tr align="center">
        <th>标识</th>
        <th>内容</th>
        <th>创建时间</th>
      </tr>
      <tr align="center">
        <td>1</td>
        <td>excel导出01</td>
        <td>2015-07-22</td>
      </tr>
      <tr align="center">
        <td>2</td>
        <td>excel导出02</td>
        <td>2015-07-22</td>
      </tr>
    </tbody>
  </table>
  <a id="exportExcel" href="javascript:;">导出Excel</a>
</body>

</html>
```

```javascript
<script>
/**
*   将html的table转成Excel的data协议类型数据，不支持ie
*   table 是HTML DOM Document 对象
×   name 是sheet的名称
*/
var tableToExcel = (function() {
  var uri = 'data:application/vnd.ms-excel;base64,',
    template = '<html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:x="urn:schemas-microsoft-com:office:excel" xmlns="http://www.w3.org/TR/REC-html40">' +
    '<head><meta http-equiv="Content-type" content="text/html;charset=UTF-8" /><!--[if gte mso 9]><xml><x:ExcelWorkbook><x:ExcelWorksheets><x:ExcelWorksheet><x:Name>{worksheet}</x:Name><x:WorksheetOptions><x:DisplayGridlines/>' +
    '</x:WorksheetOptions></x:ExcelWorksheet></x:ExcelWorksheets></x:ExcelWorkbook></xml><![endif]--></head><body><table>{table}</table></body></html>',
    base64 = function(s) {
      return window.btoa(unescape(encodeURIComponent(s)))
    },
    format = function(s, c) {
      return s.replace(/{(\w+)}/g, function(m, p) {
        return c[p];
      })
    };
  return function(table, name) {
    var ctx = {
      worksheet: name || 'Worksheet',
      table: table.innerHTML
    }
    return uri + base64(format(template, ctx));
  }
})();

$(function() {
  $('#exportExcel').on('click', function() {
    var $this = $(this);
    //设定下载的文件名及后缀
    $this.attr('download', 'myfileexcel.xls');
    //设定下载内容
    $this.attr('href', tableToExcel($('#targetTable')[0], '财务统计'));
  });
});
</script>
```
