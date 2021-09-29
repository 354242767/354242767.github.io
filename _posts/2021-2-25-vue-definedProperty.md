---
title: vue数据双向绑定实现
date: 2021-02-26 10:44:22
categories:
- 前端
tags:
- vue 
description: 
- 手写vue数据双向绑定实现
---

### index.html
``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>vue响应话实现数据双向绑定</title>
</head>
<body>
  <div id="app">
    <p>{{name}}</p>
    <p>{{age}}</p>
    <p v-text="name"></p>
  </div>
  <script src="compile.js"></script>
  <script src="cvue.js"></script>
  <script>
    const app=new CVue({
      el:'#app',
      data:{
        name:'i am cxh',
        age:18,
        foo:'foo',
        bar:{
          mua:'mua'
        }
      },
      created(){
        console.log('改变数据')
        setTimeout(() => {
          this.name='我是测试'
          this.age=28
        }, 1000);
      }
    })
    // app.name="cxh";
    // app.age=20;
    // console.log(app.$data);


    //  const app=new CVue({
    //   el:'#app',
    //   data:{
    //     name:'cxh',
    //     age:18,
    //     foo:'foo',
    //     bar:{mua:'mua'}
    //   }
    // }) 
  </script>
</body>
</html>
```

### cvue.js(vue 对象，weatcher，dep对象)
``` javascript
class CVue{
  constructor(options){
    this.$options=options;
    this.$data=options.data;

    this.observe(this.$data);

    // console.log(this);
    // new Watcher(this,'foo');
    // this.foo;
    // this.foo='123';
    // new Watcher(this,'name');
    // this.name;
    // this.name='hhh';
    // new Watcher(this,'bar');
    // this.bar='null';

    new Compile(options.el,this);
    if(options.created){
      options.created.call(this)
    }
    
  }

  observe(data){
    if(!data||typeof data!='object'){
      return;
    }
    Object.keys(data).forEach(key=>{
      this.defineReactive(data,key,data[key]);
      this.proxyData(key)
    })
  }
  defineReactive(obj,key,value){
    this.observe(value);
    const dep=new Dep()
    Object.defineProperty(obj,key,{
      get(){
        //依赖收集
        Dep.target && dep.addDep(Dep.target)
        // console.log(Dep.target);
        // console.log(dep.watchers);
        return value;
      },
      set(newValue){
        if(newValue!=value){
          value=newValue;
          // console.log(key +'更新了');
          dep.notify();
        }
      }
    })
  }

  proxyData(key){
    Object.defineProperty(this,key,{
      get(){
        return this.$data[key];
      },
      set(newValue){
        this.$data[key]=newValue;
      }
   })
  }
}

class Dep{
  constructor(){
    this.watchers=[];
  }

  addDep(watcher){
    this.watchers.push(watcher);
  }
  notify(){
    this.watchers.forEach(watcher=>{
      watcher.update();
    })
  }
}

class Watcher{
  constructor(vm,key,cb){
    this.$vm=vm;
    this.$key=key;
    this.cb=cb;

    Dep.target=this;
    this.$vm[this.$key];
    Dep.target=null;

  }
  update(){
    this.cb.call(this.$vm,this.$vm[this.$key])
    console.log(this.$key+'更新了');
  }
}
```
### compile.js(编译)
``` javascript 

// 遍历dom，解析指令和插值表达式
class Compile{
  // el-编译模板，vm-KVue实列
  constructor(el,vm){
    this.$vm=vm;
    this.$el=document.querySelector(el)
    //将模板内容移到片段
    this.$fragment=this.node2fragment(this.$el);
    //执行编译
    this.compile(this.$fragment);
    //解析完放回$el中
    this.$el.appendChild(this.$fragment);
  }

  node2fragment(el){
    //创建文档片段
    const fragment=document.createDocumentFragment();
    let child;
    while(child = el.firstChild){
      fragment.appendChild(child)
    }
    return fragment;
  }

  compile(el){
    const childNodes=el.childNodes;
    Array.from(childNodes).forEach(node =>{
      if(node.nodeType==1){
        //
        console.log('编译元素'+node.nodeName);
      }else if(this.isInter(node)){
        //
        console.log('编译文本'+node.textContent);
        this.compileText(node)
      }
       //递归编译
      if(node.children&&node.childNodes.length>0){
        this.compile(node)
      }
    })
   
  }

  isInter(node){
    return node.nodeType==3 &&/\{\{(.*)\}\}/.test(node.textContent);
  }
  // 文本替换
  compileText(node){
    const exp=RegExp.$1;

    this.update(node,exp,'text')
    // node.textContent=this.$vm[RegExp.$1]
  }

  update(node,exp,dir){
    const updater =this[dir+'Updater'];
    updater&&updater(node,this.$vm[exp]);
    //创建watcher实列完成依赖收集
    new Watcher(this.$vm,exp,function(value){
      updater&& updater(node,value);
    })
  }
  textUpdater(node,value){
    node.textContent=value;
  }
}
```
