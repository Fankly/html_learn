### BOM

- ##### 浏览器对象模型

- ##### BOM为我们提供了一组对象,通过这组对象可以完成对浏览器的各种操作

- ##### BOM对象

  - Window 代表浏览器窗口(全局对象)
  - Location  (浏览器的地址栏信息)
  - Navigator 浏览器的对象(可以用来识别浏览器)
  - History (浏览器的历史记录,控制浏览器的前进后退)
  - Screen() 屏幕的信息

- ##### BOM对象都是window对象的属性保存的,所以可以直接在JS中访问这些对象

- ##### Navigator 浏览器的对象(可以用来识别浏览器)(了解)

  - userAgent 返回一个用来描述浏览器信息的字符串

- ##### Location  (浏览器的地址栏信息)

  - 可以直接将location的值修改为一个新的地址,这样会使得页面发生跳转
  - location.href 获取当前地址
  - 常用方法
    - location.assign() 赋值一个新的URL，并且跳转到该URL中
    - location.replace() 打开一个新的URL，并且跳转到该URL中（不同的是不会在浏览记录中留下之前的记录）
    - location.reload() 重新加载页面，可以传入一个true来强制清缓存刷新

- ##### History (浏览器的历史记录,控制浏览器的前进后退)

  - 属性	
    - history.length 会话中的记录条数
  - 方法
    - history.back() 返回上一页，等价于history.go(-1)
    - history.forward() 前进下一页，等价于history.go(1)
    - history.go() 加载历史中的某一页
      - 正数表示的前进
      - 负数表示的是后退

### 定时器

- ##### 通过定时器,可以使代码在指定时间后执行

  - ###### 设置定时器的方式有两种

    - setTimeout()
      - 参数
        - 回调函数(要执行的代码)
        - 间隔的时间(毫秒)
      - 关闭定时器
        - clearTimeout()
    - setInterval() (每间隔一段时间代码就会执行一次)
      - 参数
        - 回调函数(要执行的代码)
        - 间隔的时间(毫秒)
      - 关闭定时器
        - clearInterval()

### 调用栈

- ##### 事件循环(event loop)

  - 函数在每次执行时,都会产生一个执行环境
  - 执行环境负责存储函数执行时产生的一切数据
  - 问题:函数的执行环境要存储到哪里呢?
    - 函数的执行环境存储到了一个叫做调用栈的地方
    - 栈,是一种数据结构,特点 后进先出
    - 队列,是一种数据结构,特点 先进先出
  - 调用栈(call stack)
    - 调用栈负责存储函数的执行环境
    - 当一个函数被调用时,它的执行环境会作为一个栈帧
      - 插入到调用栈的栈顶,函数执行完毕其栈帧会自动从栈中弹出

### 消息队列

- 消息队列存储将要执行的函数
- 当我们触发了一个事件时,其响应函数并不是直接就添加到调用栈中的
  - 因为调用栈中有可能会存在一些还没执行完的代码
- 事件触发后,JS代码

### 定时器原理

- 定时器的本质,就是在指定时间后将函数添加到消息队列

- setInterval() 每间隔一段时间就将函数添加到消息队列中

  - 但是如果函数执行的速度比较慢,它是无法保证每次执行的间隔都是一样的

  - 希望可以确保函数每次函数执行都有相同间隔

    ```js
       setTimeout(function fn() {
                // console.log("函数执行了~")
                console.timeEnd("间隔")
                alert("函数执行了~")
                //在setTimeout的回调函数的最后,在调用一个setTimeout
                  console.time("间隔")
                setTimeout(fn, 3000);
               
            }, 3000);
    ```

    