# 八、BOM

## 8.1 window 对象

BOM 的核心是 window，它表示浏览器的一个实例。



### 8.1.1 全局作用域

+ 所有在全局作用域中声明的变量、函数都会变成 window 对象的属性和方法(let 和 const 除外)

+ 全局变量不能通过 delete 操作符删除，而直接在 window 对象上定义的属性可以。

  var 语句添加的 window 属性不可以通过 delete 操作符删除。

  ```js
  var gae = 29
  window.color = 'red'
  // return true
  delete window.ccolor
  // return false
  delete window.age
  
  // 删除数组
  var arr = [1, 2, 3]
  // arr --> [empty, 2, 3]
  delete arr[0]
  ```

+ 尝试访问未声明的变量会抛出错误，但是通过查询 window 对象，可以知道某个可能未声明的变量是否存在



### 8.1.2 窗口关系及框架

