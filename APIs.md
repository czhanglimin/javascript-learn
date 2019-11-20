# javaScript DOM BOM
## API
应用程序编程接口，通俗地讲就是一个个的接口，用于帮助我们实现某种功能，会使用即可，不必纠结内部如何实现。
## Web API
任何语言都有自己的API，Web API就是浏览器提供的一套操作浏览器功能和页面元素的API。
# DOM简介
处理可扩展标记语言（HTML或者XML）的**编程接口**。

可用于改变网页的内容、结构、样式。
## DOM树
文档：一个页面就是一个文档，DOM中使用document标示。

元素：页面中所有的标签都是元素，DOM中使用element表示。

节点：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM中使用node表示。

DOM把以上内容都看作是对象。
# DOM获取元素
## getElementById()
注意点:

* 参数：id是字符串，大小写敏感。
* 返回值：是一个**Element对象**，当前文档没有特定ID元素时返回null。
* 先有标签，再getElementById。

console.dir()可打印元素对象，更好地查看里面的属性和方法

```html
<!DOCTYPE html>
<html>
  <head></head>
  <body>
    <h1 class="text-xxl" id="time">Hello world!</h1>
    <script>
      const time = document.getElementById('time');
      // <h1 class="text-xxl" id="time">Hello world!</h1>
      console.log(time)
      // h1#time
      console.dir(time)
    </script>
  </body>
</html>
```
## getElementsByTagName()

注意点：

* 参数：标签名。
* 返回值：带有指定标签名的**对象的集合**，以伪数组的形式存储，没有时返回空的伪数组HTMLCollections[]。
```
<!DOCTYPE html>
<html>
  <head></head>
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
      const lis = document.getElementsByTagName('li');
      // HTMLCollections(5)
      console.log(lis);
    </script>
  </body>
</html>
```
## getElementsByClassName()

注意点：

* 参数：类名。
* 返回值：带有指定标签名的**对象的集合**，以伪数组的形式存储，没有时返回空的**伪数组**HTMLCollections[]。
* H5新增

## querySelector()

注意点：

* 参数：任何选择器
* 返回值：返回指定选择器的**第一个对象**。
* H5新增

## querySelectorAll()

注意点：

* 返回指定选择器的所有元素对象的集合。
* H5新增。

```
<html>
  <head></head>
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
      const lis = document.getElementsByTagName('li');
      const querylis = document.querySelectorAll('li')
      // HTMLCollection(3) [li, li, li]
      console.log(lis);
      // NodeList(3) [li, li, li]
      console.log(querylis)
    </script>
  </body>
</html>
```
## 获取body
document.body
## 获取html
document.documentElement
# 事件基础
JS使我们有能力创建动态页面，事件是可以被JS侦测到的行为。

简单理解：触发--响应机制。
## 事件组成
1. 事件源：事件被触发的对象。
2. 事件类型：点击、经过。。。
3. 事件处理程序
```
    <button id="btn">提交</button>
    <script>
      const btn = document.getElementById('btn');
      btn.onclick = function() {
        alert('点击事件')
      }
    </script>
```