---
title: Vue前后端交互必备知识
date: 2020-05-06 22:07:35
tags: 
    - Vuejs
categories: Vuejs
---

##  1.什么是前后端交互模式

### 1.1 接口调用方式

- **原生ajax** 

- **基于jQuery的ajax**

- **fetch** 

- **axios**

### 1.2 URL地址格式

​	**1.传统形式的 URL**

- 格式： schema://host:port/path?query#fragment
  - schema: 协议 例如: http、https、ftp等
  - host: 域名 或者 IP地址
  - port: 端口
  - path: 路径
  - query: 查询参数 例如： uname=lisi&age=18
  - fragment: 锚点

**2.Restful形式的 URL**

- HTTP请求方式
  - GET   查询
  - POST 添加
  - PUT  修改
  - DELETE 删除
- 符合规则的URL地址
  - **http://www.hello.com/books** GET
  - **http://www.hello.com/books** POST
  - **http://www.hello.com/books/123** PUT
  - **http://www.hello.com/books/123** DELETE

## 2.Promise 的相关概念和用法

### 2.1 异步编程

**JavaScript的执行环境是「单线程」** 

**所谓单线程**：是指JS引擎中负责解释和执行JavaScript代码的线程只有一个，也就是一次只能完成一项任务，这 个任务执行完后才能执行下一个，它会「阻塞」其他任务。这个任务可称为主线程 

**异步模式可以一起执行多个任务** 

**JS中常见的异步调用** 

- 定时任何

- ajax 

- 事件函数

----

### 2.2 Promise对象

- **主要解决异步深层嵌套的问题(回调地狱)** 

- **promise 提供了简洁的API 使得异步操作更加容易**

### 2.3 Promise 基本用法

- 实例化 Promise 对象，构造函数中传递函数，该函数用于处理异步任务
- `resolve`和`reject`两个参数用于处理`成功 `和 `失败`两种情况，并通过 `p.then` 获取处理结果 

```javascript
var p = new Promise(function(resolve,reject){
    // 成功时调用  指的是.then方法的第一个形参函数 
    resolve()
    // 失败时调用 指的是.then方法的第二个形参函数 
    reject()
})
p.then(function(ret){
    //  从 resolve 得到正常结果
}), function(ret){
    // 从 reject得到错误信息
})
```

### 2.4 基于 Promise 实现发送 Ajax 请求

```javascript
<script type="text/javascript">
    /*
      基于Promise发送Ajax请求
    */
    function queryData(url) {
     #   1.1 创建一个Promise实例
      var p = new Promise(function(resolve, reject){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
          if(xhr.readyState != 4) return;
          if(xhr.readyState == 4 && xhr.status == 200) {
            # 1.2 处理正常的情况
            resolve(xhr.responseText);
          }else{
            # 1.3 处理异常情况
            reject('服务器错误');
          }
        };
        xhr.open('get', url);
        xhr.send(null);
      });
      return p;
}
	# 注意：  这里需要开启一个服务 
    # 在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了
    # 需要发送多次 Ajax 请求就直接使用链式操作调用.then方法
    queryData('http://localhost:3000/data')
      .then(function(data){
        console.log(data)
        #  1.4 想要继续链式编程下去 需要 return  
        return queryData('http://localhost:3000/data1');
      })
      .then(function(data){
        console.log(data);
        return queryData('http://localhost:3000/data2');
      })
      .then(function(data){
        console.log(data)
      });
  </script>
```

### 2.5 then 参数中的函数返回值

**1.返回 Promise 实例对象**

- 返回的该实例对象会调用下一个 then

**2.返回的普通值**

- 返回的是普通值会直接传递给下一个 then，通过 then 参数中函数的参数接收该值

### 2.6 Promise 常用的API

#### 1.实例方法

- p.then() **调用异步任务的正确结果**
- p.catch() **获取异常信息**
  - 等同于 .then() 的第二个形参函数的作用
- p.finally() **成功与否都会执行(尚且不是正式标准)**

```javascript
foo()
    .then(function(data){
    console.log(data)
})
    .catch(function(data){
    console.log(data)
})
    .finally(function(){
    console.log('finished')
});
```

#### 2.对象方法（静态方法）

- Promise.all() 并发处理多个异步任务，所有任务都执行完成才能得到结果
- Promise.race() 并发处理多个异步任务，只要有一个任务完成就能得到结果

#####  .all(

- `Promise.all`方法接受一个数组作参数，数组中的对象（p1、p2、p3）均为promise实例（如果不是一个promise，该项会被用`Promise.resolve`转换为一个promise)。它的状态由这三个promise实例决定

#####  .race()

- `Promise.race`方法同样接受一个数组作参数。当p1, p2, p3中有一个实例的状态发生改变（变为`fulfilled`或`rejected`），p的状态就跟着改变。并把第一个改变状态的promise的返回值，传给p的回调函数

```javascript
<script type="text/javascript">
    /*
      Promise常用API-对象方法
    */
    // console.dir(Promise)
    function queryData(url) {
    return new Promise(function(resolve, reject){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
            if(xhr.readyState != 4) return;
            if(xhr.readyState == 4 && xhr.status == 200) {
                // 处理正常的情况
                resolve(xhr.responseText);
            }else{
                // 处理异常情况
                reject('服务器错误');
            }
        };
        xhr.open('get', url);
        xhr.send(null);
    });
}

var p1 = queryData('http://localhost:3000/a1');
var p2 = queryData('http://localhost:3000/a2');
var p3 = queryData('http://localhost:3000/a3');
Promise.all([p1,p2,p3]).then(function(result){
    //   all 中的参数  [p1,p2,p3]   和 返回的结果一 一对应["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
    console.log(result) //["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
})
Promise.race([p1,p2,p3]).then(function(result){
    // 由于p1执行较快，Promise的then()将获得结果'P1'。p2,p3仍在继续执行，但执行结果将被丢弃。
    console.log(result) // "HELLO TOM"
})
</script>
```

## 3.使用 fetch 进行接口调用

- 更加简单的数据获取方式，功能更加强大、更灵活、可以看作是原生 ajax 的升级版
- 基于 `Promise` 实现
- 语法格式：fetch(url, options).then(）

### 基本语法：

```javascript
fetch('url').then(data => {
    // text()方法属于fetch API一部分 它返回一个Promise实例对象，用于获取后台返回的数据 再通过后面的.then获得数据
    return data.text();
}).then(data => {
    // 注意这里才可以得到最终获取的数据
    console.log(data);
})
```

### fetch请求参数 options

**常用配置选项**

- method(字符串):   http请求方法 默认为 GET（POST PUT DELETE）

- body(字符串): http的请求参数

- headers(对象): http请求头，默认为{}

- ```javascript
  fetch('url', {
      method: 'post',
      body: JSON.stringify({
          uname: '张三',
          pwd: '456'
      }),
      headers: {
          'Content-Type': 'application/json'
      }
  })
      .then(function(data) {
      return data.text();
  }).then(function(data) {
      console.log(data)
  });
  ```

###  fetchAPI 中 响应格式

- 用fetch来获取数据，如果响应正常返回，我们首先看到的是一个response对象，其中包括返回的一堆原始字节，这些字节需要在收到后，需要我们通过调用方法将其转换为相应格式的数据，比如`JSON`，`BLOB`或者`TEXT`等等

- text()  接收的是字符串类型的数据

- json()  接收的是 JSON格式的数据 等同于 `JSON.parse()` 

- ```javascript
  /*
    Fetch响应结果的数据格式
  */
  fetch('http://localhost:3000/json').then(function(data){
      // return data.json();   //  将获取到的数据使用 json 转换对象
      return data.text(); //  //  将获取到的数据 转换成字符串 
  }).then(function(data){
      // console.log(data.uname)
      // console.log(typeof data)
      var obj = JSON.parse(data);
      console.log(obj.uname,obj.age,obj.gender)
  })
  ```

----

## 4.使用 axios 进行接口调用

### 基本特性

- 基于promise用于浏览器和node.js的http客户端
- 支持浏览器和node.js
- 支持promise
- 能拦截请求和响应（拦截器）
- 自动转换JSON数据
- 能转换请求和响应数据

### 安装

- 可以通过npm安装    `npm install axios`
- 安装后引入 **相关的文件**

### 基本用法

```javascript
axios.get('url').then(ret => {
    // data属性名称是固定的，用于获取后台响应的数据
    console.log(ret.data)
})
```

### 请求参数

- get和 delete请求传递参数

  - 通过传统的url  以 ? 的形式传递参数
  - restful 形式传递参数 
  - 通过params  形式传递参数 

- post  和 put  请求传递参数

  - 通过选项传递参数
  - 通过 URLSearchParams  传递参数 

- ```javascript
  # 1. 发送get 请求 
  axios.get('http://localhost:3000/adata').then(function(ret){ 
      #  拿到 ret 是一个对象      所有的对象都存在 ret 的data 属性里面
      // 注意data属性是固定的用法，用于获取后台的实际数据
      // console.log(ret.data)
      console.log(ret)
  })
  # 2.  get 请求传递参数
  # 2.1  通过传统的url  以 ? 的形式传递参数
  axios.get('http://localhost:3000/axios?id=123').then(function(ret){
      console.log(ret.data)
  })
  # 2.2  restful 形式传递参数 
  axios.get('http://localhost:3000/axios/123').then(function(ret){
      console.log(ret.data)
  })
  # 2.3  通过params  形式传递参数 
  axios.get('http://localhost:3000/axios', {
      params: {
          id: 789
      }
  }).then(function(ret){
      console.log(ret.data)
  })
  #3 axios delete 请求传参     传参的形式和 get 请求一样
  axios.delete('http://localhost:3000/axios', {
      params: {
          id: 111
      }
  }).then(function(ret){
      console.log(ret.data)
  })
  
  # 4  axios 的 post 请求
  # 4.1  通过选项传递参数
  axios.post('http://localhost:3000/axios', {
      uname: 'lisi',
      pwd: 123
  }).then(function(ret){
      console.log(ret.data)
  })
  # 4.2  通过 URLSearchParams  传递参数 
  var params = new URLSearchParams();
  params.append('uname', 'zhangsan');
  params.append('pwd', '111');
  axios.post('http://localhost:3000/axios', params).then(function(ret){
      console.log(ret.data)
  })
  
  #5  axios put 请求传参   和 post 请求一样 
  axios.put('http://localhost:3000/axios/123', {
      uname: 'lisi',
      pwd: 123
  }).then(function(ret){
      console.log(ret.data)
  })
  ```

### axios 全局配置

```javascript
#  配置默认地址 
axios.defaults.baseURL = 'https://api.example.com';
#  配置 超时时间
axios.defaults.timeout = 2500;
#  配置公共的请求头
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
# 配置公共的 post 的 Content-Type
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

### 拦截器

- 请求拦截器

  - 请求拦截器的作用是在请求发送前进行一些操作
    - 例如在每个请求体里加上token，统一做了处理如果以后要改也非常容易

- 响应拦截器

  - 响应拦截器的作用是在接收到响应后进行一些操作
    - 例如在服务器返回登录状态失效，需要重新登录的时候，跳转到登录页

- ```javascript
  # 1. 请求拦截器 
  axios.interceptors.request.use(function(config) {
      console.log(config.url)
      # 1.1  任何请求都会经过这一步   在发送请求之前做些什么   
      config.headers.mytoken = 'nihao';
      # 1.2  这里一定要return   否则配置不成功  
      return config;
  }, function(err){
      #1.3 对请求错误做点什么    
      console.log(err)
  })
  #2. 响应拦截器 
  axios.interceptors.response.use(function(res) {
      #2.1  在接收响应做些什么  
      var data = res.data;
      return data;
  }, function(err){
      #2.2 对响应错误做点什么  
      console.log(err)
  })
  ```

---

## 5.使用 async/await语法

- async/await 是 `ES7` 引入的新语法，可以更加方便的`进行异步操作`
- async(异步) 关键字用于函数上 (async函数返回值是Promise实例对象)
- await(等待) 关键字用于 async 函数中 (await可以得到异步结果)

---

- async作为一个关键字放到函数前面

- 任何一个`async`函数都会隐式返回一个`promise`

- `await`关键字只能在使用`async`定义的函数中使用
  - ​    await后面可以直接跟一个 Promise实例对象
  - ​     await函数不能单独使用
- **async/await 让异步代码看起来、表现起来更像同步代码**

```javascript
# 1.  async 基础用法
# 1.1 async作为一个关键字放到函数前面
async function queryData() {
    # 1.2 await关键字只能在使用async定义的函数中使用      await后面可以直接跟一个 Promise实例对象
    var ret = await new Promise(function(resolve, reject){
        setTimeout(function(){
            resolve('nihao')
        },1000);
    })
    // console.log(ret.data)
    return ret;
}
# 1.3 任何一个async函数都会隐式返回一个promise   我们可以使用then 进行链式编程
queryData().then(function(data){
    console.log(data)
})

#2.  async    函数处理多个异步函数
axios.defaults.baseURL = 'http://localhost:3000';

async function queryData() {
    # 2.1  添加await之后 当前的await 返回结果之后才会执行后面的代码   

    var info = await axios.get('async1');
    #2.2  让异步代码看起来、表现起来更像同步代码
    var ret = await axios.get('async2?info=' + info.data);
    return ret.data;
}

queryData().then(function(data){
    console.log(data)
})
```

## 6.能够基于后台接口实现案例