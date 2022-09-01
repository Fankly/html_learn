### DOM(文档对象模型)

- #### 节点(Node)

  - ###### 介绍

    - node就是网页中所有节点的父类

  - ###### 常用节点

    - 文档节点
    - 元素节点
    - 文本节点
    - 属性节点

- #### 关系

  - 祖先 —— 包含后代元素的元素是祖先元素
  - 后代 —— 被祖先元素包含的元素是后代元素
  - 父 —— 直接包含子元素的元素是父元素
  - 子 —— 直接被父元素包含的元素是子元素
  - 兄弟 —— 拥有相同父元素的元素是兄弟元素

- #### 使用DOM

  - 要使用DOM来操作网页,我们需要浏览器至少得先给我一个对象才能完成各种操作

  - 所以浏览器已经为我们提供了docment对象,它是一个全局变量可以直接使用

    - document代表的是整个网页
    - window代表的是整个窗口

    ```js
     		//console.log(document)
    
            //获取btn对象
            const btn = document.getElementById("btn")
    
            //修改btn中的文字 innerText属性
            btn.innerText = "Click ME"
    
            console.log(btn)
    ```

- #### 文档节点

  - ##### document对象

    - ###### document对象表示的是整个网页

    - ###### doucment对象的原型链
    
      - HTMLDocument -> Document -> Node -> EventTarget -> Object.prototype -> null
    
    - ###### 凡是在原型链上存在的对象的属性和方法都可以通过Document去调用
    
    - ###### 部分属性
    
      - document.documentElement --> html根元素
      - document.head --> head元素
      - document.title --> title元素
      - document.body --> body元素
      - document.images --> 获取页面中所有的图片
      - doucment.links --> 获取页面中所有的超链接
  
- #### 元素节点

  - ##### 元素节点对象(element)

    - ###### 在网页中,每一个标签都是一个元素节点

    - ###### 如何获取元素节点对象?

      1. 通过document对象来获取元素节点
      2. 通过document对象创建元素节点

    - ###### 通过document来获取已有的元素节点

      - document.getElementById()
        - 根据id获取一个元素节点对象
      - document.getElementsByClassName()
        - 根据元素的class属性值获取一组元素节点对象
        - 返回的是一个类数组对象
        - 该方法返回的结果是一个实时更新的集合
          - 当网页中新添加元素时,集合也会实时的刷新
      - document.getElementsByTagName()
        - 根据标签名获取一组元素节点对象
        - 返回的结果时可以实时更新的集合
        - document.getElementsByTagName("*")
          - 获取页面中的所有元素
      - document.getElementsByName()
        - 根据name属性获取一组元素节点对象
        - 返回一个实时更新的集合
        - 主要用于表单项
      - document.querySelectorAll()
        - 根据选择器去页面中查询元素
        - 会返回一个类数组(不会实时更新)
      - document.querySelector()
        - 根据选择器去页面中查询第一个符合条件的元素

    - ##### 创建一个元素节点

      - document.createElement()
        - 根据标签名创建一个元素节点对象

    - ##### 元素的属性和方法

      ```js
      
              /* 
              div的原型链
                  HTMLDivElement -> HTMLElement -> Element -> Node -> EventTarget -> Object.prototype -> null
              */
              const box = document.getElementById('box1')
      
              console.log(box)
      ```

    - ##### 通过元素节点对象获取其他节点的方法

      - element.childNodes 获取当前元素的子节点
        - 会包含空白的子节点
      - element.children 获取当前元素的子元素
      - element.firstChild 获取当前元素的第一个子节点
      - element.firstElementChild 获取当前元素的第一个子元素
      - element.lastChild 获取当前元素的最后一个子节点
      - element.lastElementChild 获取当前元素的最后一个子元素
      - element.nextSibling 获取当前元素的下一个兄弟节点
      - element.nextElementSibling 获取当前元素的下一个兄弟元素
      - element.previousElementSibling 获取当前元素的前一个兄弟元素
      - element.previousSibling 获取当前元素的前一个兄弟节点
      - element.parentNode 获取当前元素的父节点
      - element.parentElement  获取当前元素的父元素
      - element.tagName 获取当前元素的标签名

- #### 文本节点

  - ##### 在DOM中,网页中所有的文本内容都是文本节点对象

    - ###### 可以通过元素来获取其中的文本节点对象,但是我们通常不会这么做

    - ###### 我们可以直接通过元素去修改其中的文本

      - 修改文本的三个属性

        - element.textContent 获取或修改元素中的文本内容

          - 获取的是标签中的内容,不会考虑css样式

        - element.innerText 获取或修改元素中文本内容

          - innerText获取内容时,会考虑css样式
          - 通过innerText去读取CSS样式,会触发网页的重排(计算CSS样式)
          - 当字符串中有标签时,会自动对标签进行转义

        - element.innerHTML 获取或修改元素中的html代码

          - 可以直接向元素中添加html代码

          - innerHTML插入内容,有被xss注入的风险

            ```js
               //  xss注入
                    element.innerHTML = "<script src='https://sss/sss.js'><\/script>"
            ```

- #### 属性节点(Attr)

  - #####  在DOM也是一个对象,通常不需要获取对象而是直接通过元素即可完成对其的各种操作

  - 如何操作属性节点

    - 方式一
      - 读取
        - 元素.属性名
        - 注意事项
          - class属性需要使用className来读取
          - 读取一个布尔值(比如:disabled属性)时,会返回true或false
      - 修改
        - 元素.属性名 = 属性值
    - 方式二
      - 读取
        - 元素.getAttribute(属性名)
      - 修改
        - 元素.setAttribute(属性名,属性值)
      - 删除
        - 元素.removeAttribute(属性名)

- #### 事件(event)

  - 事件就是用户和页面之间发生的交互行为

    - 比如:点击按钮、鼠标移动、双击按钮、松开按键...

  - 可以通过为事件绑定响应函数(回调函数),来完成和用户之间的交互

  - 绑定响应函数的方式

    1. 可以直接在元素的属性中设置

    2. 可以通过为元素的指定属性设置回调函数的形式来绑定事件(一个事件只能绑定一个响应函数)

    3. 可以通过元素addEventListener()方法来绑定事件

       ```js
        		const btn = document.getElementById("btn")
              /*  btn.onclick = function () {
                   alert("点击")
               } */
       
               btn.addEventListener("click",function(){
                  alert("点击1")
               })
       
       		
               btn.addEventListener("click",function(){
                  alert("点击2")
               })
       
       		
               btn.addEventListener("click",function(){
                  alert("点击3")
               })
       ```

- #### 文档的加载

  - 网页是自上而下加载的,如果将js代码编写到网页的上边

    - js代码在执行时,网页还没有加载完毕,这时会出现无法获取到DOM对象的情况

    - window.onload 事件会在窗口中的内容加载完毕之后才触发

    - 如何解决这个问题

      1. 将script标签编写到body的最后(\*\*\*\*\*)

      2. 将代码编写到window.onload的回调函数中

      3. 将代码编写到document对象的DOMContentLoaded的回调函数中(执行时机更早)

      4. 将代码编写到外部的js文件中,然后以defer的形式进行引入(执行时机更早,早于DOMContentLoaded)(\*\*\*\*\*)

         ```js
         <!DOCTYPE html>
         <html lang="en">
         
         <head>
             <meta charset="UTF-8">
             <meta http-equiv="X-UA-Compatible" content="IE=edge">
             <meta name="viewport" content="width=device-width, initial-scale=1.0">
             <title>Document</title>
             /*<script>
                 window.addEventListener("load", function () {
                     const btn = document.getElementById('btn')
                     console.log(btn)
                 })*/
               /*   document.addEventListener("DOMContentLoaded", function () {
                     const btn = document.getElementById('btn')
                     console.log(btn)
                 });
             </script> */
          <script defer src="./script.js"></script>
         </head>
         
         <body>
             <button id="btn">点我一下</button>
             <iframe src="http://www.lilichao.com" frameborder="0"></iframe>
         
         </body>
         
         </html>
         ```

- #### 练习

  - 图片的切换
  
  - 多选按钮的全选和反选
  
    - ###### 知识点
  
      - 在事件的响应函数中,响应函数绑定给谁,this就是谁(箭头函数除外)
  
- #### 元素的修改

  - appendChild() 用于给一个节点添加子节点
  - insertAdjacentElement() 可以向元素的任意位置添加元素
    - 两个参数
      1. 要添加的位置
         - beforeend 标签的最后(父子元素)
         - afterbegin 标签的开始(父子元素)
         - beforebegin 在元素的前面插入元素(兄弟元素)
         - afterbegin 在元素的后面插入元素(兄弟元素)
      2. 要添加的元素

  - insertAdjacentHTML() 方法将指定的文本解析为element元素，并将结果节点插入到 DOM 树中的指定位置
  - replaceWith()  使用一个元素替换当前元素
  - remove() 删除当前元素

  ```js
  /* 
              点击按钮后,向ul中添加一个唐僧
          */
  
          const btn01 = document.getElementById("btn01")
          const list = document.getElementById("list")
          btn01.onclick = function () {
              const li = document.createElement("li")
              li.textContent = "唐僧"
              li.id = "ts"
              // console.log(li)
              list.appendChild(li)
          }
  ```

- #### 练习-删除员工

  - 只要点击超链接就会触发页面的跳转,事件中可以通过取消默认行为来阻止超链接的跳转
  - 使用return false来取消默认行为,只在xxx.xxx = function(){}这种形式绑定的事件中才适用
  - 修改超链接的href="javascript:;"也可以取消超链接默认行为

  ```html
  <!DOCTYPE html>
  <html lang="zh">
  
  <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <style>
          .outer {
              width: 400px;
              margin: 100px auto;
              text-align: center;
          }
  
          table {
              width: 400px;
              border-collapse: collapse;
              margin-bottom: 20px;
          }
  
          td,
          th {
              border: 1px black solid;
              padding: 10px 0;
          }
  
          form div {
              margin: 10px 0;
          }
      </style>
  
      <script>
          window.addEventListener("DOMContentLoaded", function () {
  
              function delElementHandler() {
                  const tr = this.parentNode.parentNode
                  //this.parentElement.parentElement.remove()
                  if (confirm(`你确定要删除[${tr.firstElementChild.textContent}]吗`)) {
                      tr.remove()
                      alert("删除成功")
                  }
              }
              const links = document.links
  
              const tbody = document.querySelector("tbody")
  
              for (let i = 0; i < links.length; i++) {
                  links[i].onclick = delElementHandler
              }
  
              const btn = document.getElementById("btn")
              btn.onclick = function () {
                  const name = document.getElementById("name").value
                  const email = document.getElementById("email").value
                  const salary = document.getElementById("salary").value
                  // 这种写法,容易被xss的攻击
                  /*  tbody.insertAdjacentHTML("beforeend", ` <tr>
                       <td>${name}</td>
                       <td>${email}</td>
                       <td>${salary}</td>
                       <td><a href="javascript:;">删除</a></td>
                   </tr>`) */
                  //创建tr元素
                  const tr = document.createElement("tr")
  
                  //创建td元素
                  const nameTd = document.createElement("td")
                  const emailTd = document.createElement("td")
                  const salaryTd = document.createElement("td")
                  //添加文本
                  nameTd.textContent = name
                  emailTd.textContent = email
                  salaryTd.textContent = salary
  
                  //将三个td添加到tr中
                  tr.appendChild(nameTd)
                  tr.appendChild(emailTd)
                  tr.appendChild(salaryTd)
                  tr.insertAdjacentHTML("beforeend", "<td><a href='javascript:;'>删除</a></td>")
  
                  tbody.appendChild(tr)
                  // 用于上边超链接是新添加的,所以它的上边并没有绑定单击响应函数,所以新添加的员工无法删除
                  // 解决方式,为新添加的超链接单独绑定响应函数
                  links[links.length - 1].onclick = delElementHandler
                  return false
              }
          })
      </script>
  </head>
  
  <body>
      <div class="outer">
          <table>
              <tbody>
                  <tr>
                      <th>姓名</th>
                      <th>邮件</th>
                      <th>薪资</th>
                      <th>操作</th>
                  </tr>
                  <tr>
                      <td>孙悟空</td>
                      <td>swk@hgs.com</td>
                      <td>10000</td>
                      <td><a href="javascript:;">删除</a></td>
                  </tr>
                  <tr>
                      <td>猪八戒</td>
                      <td>zbj@glz.com</td>
                      <td>8000</td>
                      <td><a href="javascript:;">删除</a></td>
                  </tr>
                  <tr>
                      <td>沙和尚</td>
                      <td>shs@lsh.com</td>
                      <td>6000</td>
                      <td><a href="javascript:;">删除</a></td>
                  </tr>
              </tbody>
          </table>
  
          <form action="#">
              <div>
                  <label for="name">姓名</label>
                  <input type="text" id="name" />
              </div>
              <div>
                  <label for="email">邮件</label>
                  <input type="email" id="email" />
              </div>
              <div>
                  <label for="salary">薪资</label>
                  <input type="number" id="salary" />
              </div>
              <button id="btn">添加</button>
          </form>
      </div>
  </body>
  
  </html>
  ```

- #### 节点的复制

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
      <script>
          window.addEventListener("DOMContentLoaded", function () {
              const list2 = document.getElementById("list2")
              const l1 = document.getElementById("l1")
              const btn01 = document.getElementById("btn01")
  
              btn01.onclick = function () {
                  // 用来对节点进行复制
                  const newL1 = l1.cloneNode(true)
  
                  /* 
                      使用cloneNode()方法对节点进行复制时,它会复制节点的所有特点包括各种属性
                      这个方法默认只会复制当前节点,而不会复制节点的子节点
                      可以传递一个true作为参数,这样改方法也会将元素的子节点一起复制
                  */
                  newL1.id = "newL1"
                  console.log(newL1)
                  list2.appendChild(newL1)
              }
          })
      </script>
  </head>
  
  <body>
      <button id="btn01">点我一下</button>
      <ul id="list1">
          <li id="l1">孙悟空</li>
          <li id="l2">猪八戒</li>
          <li id="l3">沙和尚</li>
      </ul>
  
      <ul id="list2">
          <li>蜘蛛精</li>
      </ul>
  </body>
  </html>
  ```

- #### 修改样式

  - ##### 修改样式的方式(行内样式)

    - 元素.style.样式名 = 样式值
    - 如果样式名中含有-,则需要将样式表修改为驼峰命名法

- #### 读取样式

  - ##### 读取的方式(内敛样式(行内样式))

    - 元素.style.样式名

  - ##### getComputedStyle(element) 

    - 参数
      1. 要获取样式的对象
      2. 要获取的伪元素

    - 返回值
      - 返回一个对象,这个对象中包含了当前元素所有生效的样式

    - 注意事项
      - 样式对象中返回的样式值,不一定能来拿来直接计算
        - 所以使用时,一定要确保值是可以计算的才去计算

    - 获取伪元素 getComputedStyle(element,"::before") 
    - 获取的样式都是有单位的

- #### 通过属性读取样式

  - 元素.clientWidth
  - 元素.clientHeight
    - 获取元素内部的宽度和高度(包括内容区和内边距)
  - 元素.offsetWidth
  - 元素.offsetHeight
    - 获取元素的可见框的大小(包括内容区、内边距和边框)

  - 元素.scrollWidth
  - 元素.scrollHeight
    - 获取元素滚动区域的大小

  - 元素.offsetParent
    - 获取元素的定位父元素
    - 定位父元素,离当前元素最近的开启了定位的祖先元素,如果所有的元素都没有开启定位则返回body

  - 元素.offsetTop
  - 元素.offsetLeft
    - 获取元素相对于其定位父元素的偏移量

  - 元素.scrollTop
  - 元素.scrollLeft
    - 获取或设置元素滚动条的偏移量

- #### 操作Class

  ```js
    /* 
                  点击按钮后，修改box1的宽度
              */
  
              const btn = document.getElementById("btn")
              const box1 = document.querySelector(".box1")
  
              btn.onclick = function () {
  
                  // 除了直接修改样式外，也可以通过修改class属性来间接的修改样式
                  /* 
                      通过class修改样式的好处：
                          1. 可以一次性修改多个样式
                          2. 对JS和CSS进行解耦
                  */
                  // box1.className += " box2"
  
                  // 元素.classList 是一个对象，对象中提供了对当前元素的类的各种操作方法
                  /* 
                      元素.classList.add() 向元素中添加一个或多个class
                      元素.classList.remove() 移除元素中的一个或多个class
                      元素.classList.toggle() 切换元素中的class
                      元素.classList.replace() 替换class
                      元素.classList.contains() 检查class
                  */
                  // box1.classList.add("box2", "box3", "box4")
                  // box1.classList.add("box1")
  
                  // box1.classList.remove("box2")
                  // box1.classList.toggle("box2")
                  // box1.classList.replace("box1", "box2")
  
                  let result = box1.classList.contains("box3")
                  console.log(result)
              }
  ```

- #### 事件对象

  - ##### event事件

    - ###### 事件对象

      - 事件对象是由浏览器触发时所创建的对象
        - 这个对象中封装了事件相关的各种信息

      - 通过事件对象可以获取到事件的详细信息
        - 比如:鼠标的坐标、键盘的按键...

      - 浏览器在创建事件对象后,会将事件对象作为响应函数的参数传递,所以我们在事件的回调函数中定义一个形参来接受事件对象
      
    - ###### 在DOM中存在着多种不同类型的事件对象
    
      - 多种事件对象有一个共同的祖先Event
        - event.target 触发事件的对象
        - event.stopPropagation() 取消事件的传递
        - event.currentTarget 绑定事件的对象(同this)
        - event.preventDefault() 取消默认行为
      - 事件的冒泡(bubble)
        - 事件的冒泡就是指事件的向上传导
        - 当元素上的某个事件被触发后,其祖先元素上的相同事件也会同时被触发
        - 冒泡的存在大大的简化代码的编写,但是在一些场景下我们并不希望冒泡存在
          - 不希望事件冒泡时,可以通过事件对象来取消冒泡
    
    - ###### 在事件中的响应函数中
    
      - event.target 表示的是触发事件的对象
      - this 绑定事件的对象
    
    - ###### 事件的冒泡
    
      - 
