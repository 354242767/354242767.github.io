---
title: 从输入URL到页面加载的过程？如何由一道题完善自己的前端知识体系！
date: 2018-03-27 23:33:26
category:
- 前端
tags:
- JavaScript
- HTML
- CSS
- 优化
- 浏览器模型
- 渲染原理
- http
- web 安全
description: 
- 这道题的覆盖面可以非常广，很适合作为一道承载知识体系的题目。
- 每一个前端人员，如果要往更高阶发展，必然会将自己的知识体系梳理一遍，没有牢固的知识体系，无法往更高处走！
---

## 大纲
- **对知识体系进行一次预评级**

- **为什么说知识体系如此重要？**

- **梳理主干流程**

- **从浏览器接收url到开启网络请求线程**

    - 多进程的浏览器

    - 多线程的浏览器内核

    - 解析URL

    - 网络请求都是单独的线程

    - 更多

- 开启网络线程到发出一个完整的http请求

    - DNS查询得到IP

    - tcp/ip请求

    - 五层因特网协议栈

- 从服务器接收到请求到对应后台接收到请求

    - 负载均衡

    - 后台的处理

- 后台和前台的http交互

    - http报文结构

    - cookie以及优化

    - gzip压缩

    - 长连接与短连接

    - http 2.0

    - https

- 单独拎出来的缓存问题，http的缓存

    - 强缓存与弱缓存

    - 缓存头部简述

    - 头部的区别

- 解析页面流程

    - 流程简述

    - HTML解析，构建DOM

    - 生成CSS规则

    - 构建渲染树

    - 渲染

    - 简单层与复合层

    - Chrome中的调试

    - 资源外链的下载

    - loaded和domcontentloaded

- CSS的可视化格式模型

    - 包含块（Containing Block）

    - 控制框（Controlling Box）

    - BFC（Block Formatting Context）

    - IFC（Inline Formatting Context）

    - 其它

- JS引擎解析过程

    - JS的解释阶段

    - JS的预处理阶段

    - JS的执行阶段

    - 回收机制

- 其它

- 总结