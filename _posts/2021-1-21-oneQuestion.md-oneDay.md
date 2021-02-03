---
title: 每日一题
date: 2021-09-06 18:44:22
categories:
- 前端
tags:
- javaScript
description: 
- 从基础到进阶的JavaScript问题列表
---

### 1.输出什么？

```javaScript
function sayHi() {
  console.log(name)
  console.log(age)
  var name = 'Lydia'
  let age = 21
}

sayHi()

```
- A: Lydia 和 undefined
- B: Lydia 和 ReferenceError
- C: ReferenceError 和 21
- D: undefined 和 ReferenceError

### 2.输出什么？

```javaScript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1)
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1)
}

```
- A: 0 1 2 和 0 1 2
- B: 0 1 2 和 3 3 3
- C: 3 3 3 和 0 1 2

### 3.输出什么？

```javaScript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2
  },
  perimeter: () => 2 * Math.PI * this.radius
}

shape.diameter()
shape.perimeter()

```
- A: 20 and 62.83185307179586
- B: 20 and NaN
- C: 20 and 63
- D: NaN and 63

### 4.输出什么？

```javaScript
+true;
!"Lydia";
```

A: 1 and false
B: false and NaN
C: false and false

### 答案
1.D 2.C 3.B 4.A
