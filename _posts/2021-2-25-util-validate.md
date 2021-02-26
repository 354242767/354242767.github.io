---
title: 常用的表单验证
date: 2021-02-26 10:44:22
categories:
- 前端
tags:
- javaScript 
- Reg
- validate
description: 
- 项目utils中 validate.js常见的正则验证
---

### validate.js

``` javascript
// 身份证
export function identity(s) {
	return /^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/.test(s);
}

// 邮箱
export function email(s) {
	return /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(s);
}

// 手机号码
export function mobile(s) {
	return /^1[0-9]{10}$/.test(s);
}

//电话号码
export function phone(s) {
	return /^([0-9]{3,4}-)?[0-9]{7,8}$/.test(s);
}

// URL地址
export function url(s) {
	return /^http[s]?:\/\/.*/.test(s);
}

// IP地址
export function ip(s) {
	return /^(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])$/.test(s);
}

// 数字
export function number(s) {
	return /^-?\d*\.?\d+$/.test(s);
}

// 整数
export function integer(s) {
	return /^-?\d+$/.test(s);
}
```
