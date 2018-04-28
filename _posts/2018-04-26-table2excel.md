---
title: 前端-表格导出Excel
date: 2018-04-26 13:07:08
categories:
- 前端
tags:
- JavaScript
- 实用技巧
description: 
- 最近项目中需要用到把页面中的表格导出成Excel，于是就总结了基于JavaScript的表格导出Excel的技巧
- 兼容目前主流浏览器，好了直接上代码。
---

``` html
<!DOCTYPE html>  
<html>  
<head lang="en">  
    <meta charset="UTF-8">  
    <title>表格导出Excel</title>  
    <script language="JavaScript" type="text/javascript">  
        
        var idTmr;  
        function  getExplorer() {  
            var explorer = window.navigator.userAgent ;  
            //ie  
            if (explorer.indexOf("MSIE") >= 0) {  
                return 'ie';  
            }  
            //firefox  
            else if (explorer.indexOf("Firefox") >= 0) {  
                return 'Firefox';  
            }  
            //Chrome  
            else if(explorer.indexOf("Chrome") >= 0){  
                return 'Chrome';  
            }  
            //Opera  
            else if(explorer.indexOf("Opera") >= 0){  
                return 'Opera';  
            }  
            //Safari  
            else if(explorer.indexOf("Safari") >= 0){  
                return 'Safari';  
            }  
        }  
        function method(tableid) {  
            if(getExplorer()=='ie')  
            {  
                var curTbl = document.getElementById(tableid);  
                var oXL = new ActiveXObject("Excel.Application");  
                var oWB = oXL.Workbooks.Add();  
                var xlsheet = oWB.Worksheets(1);  
                var sel = document.body.createTextRange();  
                sel.moveToElementText(curTbl);  
                sel.select();  
                sel.execCommand("Copy");  
                xlsheet.Paste();  
                oXL.Visible = true;  
  
                try {  
                    var fname = oXL.Application.GetSaveAsFilename("Excel.xls", "Excel Spreadsheets (*.xls), *.xls");  
                } catch (e) {  
                    print("Nested catch caught " + e);  
                } finally {  
                    oWB.SaveAs(fname);  
                    oWB.Close(savechanges = false);  
                    oXL.Quit();  
                    oXL = null;  
                    idTmr = window.setInterval("Cleanup();", 1);  
                }  
  
            }  
            else  
            {  
                tableToExcel(tableid)  
            }  
        }  
        function Cleanup() {  
            window.clearInterval(idTmr);  
            CollectGarbage();  
        }  
        var tableToExcel = (function() {  
            var uri = 'data:application/vnd.ms-excel;base64,',  
                    template = '<html><head><meta charset="UTF-8"></head><body><table>{table}</table></body></html>',  
                    base64 = function(s) { return window.btoa(unescape(encodeURIComponent(s))) },  
                    format = function(s, c) {  
                        return s.replace(/{(\w+)}/g,  
                                function(m, p) { return c[p]; }) }  
            return function(table, name) {  
                if (!table.nodeType) table = document.getElementById(table)  
                var ctx = {worksheet: name || 'Worksheet', table: table.innerHTML}  
                window.location.href = uri + base64(format(template, ctx))  
            }  
        })()  
  
    </script>  
</head>  
<body>  
  
<div >  
    <button type="button" onclick="method('tableExcel')">导出Excel</button>  
</div>  
<div id="myDiv">  
<table id="tableExcel" width="100%" border="1" cellspacing="0" cellpadding="0">  
    <tr>  
        <td colspan="5" align="center">表格导出到Excel</td>  
    </tr>  
    <tr>  
        <td>标题1</td>  
        <td>标题2</td>  
        <td>标题3</td>  
        <td>标题4</td>  
        <td>标题5</td>  
    </tr>  
    <tr>  
        <td>前端技术</td>  
        <td>html</td>  
        <td>css</td>  
        <td>js</td>  
        <td>node</td>  
    </tr>  
    <tr>  
        <td>后端语言</td> 
        <td>java</td>  
        <td>php</td>  
        <td>python</td>  
        <td>c++</td>  
    </tr>  
    <tr>  
        <td>数据库</td>  
        <td>mysql</td>  
        <td>oracle</td>  
        <td>mongodb</td>  
        <td>DB2</td>  
    </tr>  
</table>  
</div>  
</body>  
</html>  
```
[在线演示](https://354242767.github.io/examples/projects/Effects/)

如果想要更为丰富的效果可考虑jq的插件或者是`js-xlsx`
[github：https://github.com/tealeg/xlsx](https://github.com/tealeg/xlsx)

不熟悉的同学可参考[这篇文章：https://segmentfault.com/a/1190000011057149](https://segmentfault.com/a/1190000011057149),有具体demo