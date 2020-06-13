+ 服务器软件：`apache`
+ 数据库软件：`mysql`
+ PHP 开发环境简称：`WAMH ---> window + apache + mysql + PHP`



# 一、软件架构

+ C/S ---> client/server ---> 客户端/服务端
+ B/S ---> broswer ---> server ---> 浏览器/服务器





# 二、网络基础

+ ip

  唯一性，没有规律，不容易记忆

  + `192.168` 局域网 ip
  + `127.0.0.1` 本地测试的 ip 地址

+ 域名(ip的名字)

  `ping jd.com` 可以获取京东的 ip

+ DNS

  用于记录 IP 和域名的对应关系

+ 端口

  可以精装定位具体的程序，是程序和外界通信的出入口

  常见 80 端口，3306 数据库

  本地机器会根据有需求的程序分配端口，随机从 <font color=red> 1024~65535 </font> 之间产生端口号。端口 0~1023 是分配给固定特殊的网络服务。比如：www选择80，FTPZ1。协议里面低于 1024 的端口都有确切的定义，他们对于着因特网上常见的一些服务

+ 特殊域名

  `localhost` 意为本地主机，保留域名，主要用于本地测试，对应的 ip 地址为 `127.0.0.1`

+ 本地 hosts 文件

  在本地存放了 ip 与域名的对应关系

  输入网址时，先找本地 hosts 文件，再找 DNS 进行域名转 ip





# 三、PHP

## 3.1 PHP 基础

```php
<?php
  header('content-type:text/html;charset=utf-8')
  // PHP 代码写在此标签内。必须在服务器中执行
?>
```

+ 注释

  + `//`
  + `/* ... */`

+ 输出(只能用于简单数据类型)

  固定写法：不是函数，将服务器的数据输出给浏览器展示

  `echo "..."`

+ 注意：每行都要加 `;`

+ 变量：

  + 定义：`$`
  + 规则：
    + 变量以 `$` 开头
    + 在 `$` 后跟变量名，规则通 JS
    + PHP 中变量不用声明，直接定义使用
    + PHP 中的变量先赋值后使用(无值会报错)
  + 变量操作：
    + `isset()` 判断变量是否赋值(变量有值，不为 null)，有值为true 无值为空
    + `empty()` 判断变量是否为空(值为 null，''，0，'0'，0.0，[]，false，未赋值)，会认为为空，虽然有值，但没有实际意义
    + `unset()` 删除变量



## 3.2 数据类型

+ 整数

+ 浮点数

+ 字符串

  + PHP 中的字符串拼接不能使用 `+` ，字符串拼接用 `.` (点)
  + PHP 字符串中的双引号会解析变量，如果 `""` 中有变量名，会转成变量对应的值
  + `''` 的性能更好，直接使用

+ Boolean 类型

  + `true` 输出 1
  + `false` 输出空字符串
  + 查看布尔类型：`var_dump()` 输出数据详细信息

+ 数组

  + 索引数组(类似 js 的数组)

    + 输出：复杂类型：`var_dump()` ---> 繁琐 `print_r()` ---> 用于数据复杂类型的输出
    + 取值/赋值：`arr[0]` (同 js)
    + 获取数组长度：`count($arr)`
    + 追加元素：`$arr[]` 中括号内不写值，相当于追加元素

  + 关联数组(类似 js 的对象)

    + 定义

      ```php
      $info = [
          'name' => 'zs',
          'age' => 18
      ]
      ```

    + 取值：`$info['name']`

    + 改值：`$info['name'] = 'lisi'`

  + 数组遍历

    ```php
    // 数组遍历
    for ($i=0; $i < count($arr); $i++) { 
        # code...
        $sum += $arr[$i];
    }
    // 遍历关联数组
    foreach ($variable as $key => $value) {
        # code...
    }
    ```

  + `array_splice(数组, index, 个数, 替换添加)`

    + 参1：要修改的数组
    + 参2：下标
    + 参3：个数，删除的个数
    + 参4：要添加的项



## 3.3 函数

+ 描述：PHP 的函数的语法与 js 的函数的语法基本一致

+ 不同点

  + 函数大小写不敏感
  + 函数的参数可以设置默认值

+ 语法：

  ```php
  function sayHello($name='周杰伦') {}
  ```



## 3.4 常量 constant

+ 定义：脚本执行周期内，值不会发生改变的量。常量不可以修改和删除。定义为常量可节省存储空间
+ 语法：`define(常量名, 常量值)`
+ 规范：
  + 常量区分大小写
  + 常量名一般全部大写
  + 常量不可以重复定义及修改数据
  + 常量值为标量数据类型(整形、浮点型、布尔型、字符串)



## 3.5 PHP 内置函数

+ 数学函数

  ```php
  // 1.返回一组数的最大值及最小值
  max();
  min();
  // 2.返回绝对值
  abs();
  // 3.向下取整
  floor();
  // 4.向上取整
  ceil();
  // 5.四舍五入
  round();
  // 6.返回随机数(可取两端值)
  rand();
  ```

+ 日期函数

  ```php
  // 返回当前时间戳(1970年~现在的秒数)
  time();
  // 格式化一个本地时间或日期
  date(format, time);
  // 获取时间戳
  $time = time();
  // 格式化时间戳,格式：Y(年)m(月)d(日) H(时)i(分)s(秒)
  date('Y-m-d H:i:s', $time);
  // 设置时区 PRC
  date_timezone_set
  ```

+ 字符串函数

  ```php
  // 字符串替换
  str_replace(查找的值, 替换的值, 执行替换操作的字符);
  // 去除字符串首尾的空白字符
  trim(字符串);
  // 用一个分隔符分隔一个字符串,返回数组
  explode(分隔符, 执行分隔的字符串);
  // 将一个一维数组的值拼接为字符串
  implode(连接符, 执行连接的数组);
  // 返回字符串的子串
  substr(字符串, 起始索引, 截取长度);
  // 从左-->右查找指定的字符,并返回该字符和后面全部字符
  strchr(字符串, 标识字符);
  // 从右-->左查找指定的字符,并返回该字符后全部字符(多用于截取后缀名)
  strrchr(字符串, 标识字符);
  ```

+ 数组

  ```php
  // 返回 true/false
  in_array(值, 数组);
  // 剪切,改变原数组
  array_splice(数组, 下标, 个数);
  ```

  

## 3.6 PHP 执行机制

+ 在服务器中执行 PHP 文件时，服务器只会执行 PHP 内部标签代码，PHP 标签外的代码不会报错，会被忽略
+ 执行完之后，会一起返回到浏览器，由浏览器解析



## 3.7 PHP 中引入 PHP 文件

```php
<?php include '....' ?>;
// include_once 只引入一次，防止重复引用
<?php include_once '....' ?>;
```



## 3.8 表单处理

+ 作用：收集用户信息，提交给后台服务器

+ 必须属性：

  + `action` 表单数据提交地址(默认)
  + `method` 表单提交数据的方式 get/post
  + `name` 每个表单标签必须有 name 属性

+ 获取提交的数据(get)

  + `$_GET` 后台 PHP 提供的一个超全局变量 `$_GET` (关联数组)

  + 作用：用于获取 get 方式提交的数据

  + 跳转：

    ```php
    header('location:http://www.baidu.com');
    // refresh：刷新 3:3秒后跳转
    header('refresh:3;url=01-form.html');
    ```

+ 获取提交的数据(post)

  + `$_POST` 后台 PHP 内部提供一个超全局变量

+ `$_REQUEST` 相当于 `$_GET` 和 `$_POST` 的集合

+ 其它提交数据的方式：`put` `delete` 不常用

+ `get` 和 `post`(不能获取文件) 的区别

  + get 请求方式会在 url 后面拼接数据，直接暴露数据不安全
  + get 请求传递数据量小，4kb 左右(无法上传大文件) 速度快
  + post 相对安全，不会在 url 后面拼接数据
  + post 对上传数据的大小没有限制



## 3.9 文件上传

+ 必须使用 `post` 方式

+ 除了 `action` `method` 外，必须写 `enctype="multipart/form-data"` 告诉后台多种格式的文件

+ 获取前端传递的文件，保存到服务器

  PHP 中提供了一个超全局变量 `$_FILES` 来获取前端传递的文件

+ 问题：

  + Q：上传的文件被自动删除？
  + A：这是服务器的保护机制，上传到服务器文件，在 PHP 程序执行结束后被删除，如果要使用文件，必须手动转移文件(在 PHP 程序结束之前)
  + 转移文件：`move_uploaded_file(临时文件地址, 新的文件地址)`



## 3.10 PHP页面动态渲染

+ PHP 支持与 HTML 混编，混编的格式为 PHP
+ 服务器解析时只会执行标签内部的代码，忽略 PHP 标签外的代码，最后将执行结果与非 PHP 代码一起返回给浏览器进行解析
  + 请求的是静态文件，服务器直接返回交给浏览器解析
  + 请求的是动态文件(PHP程序)在服务器中执行 PHP 代码，然后将执行结果和非 PHP 代码一起返给浏览器解析



## 3.11 表单标签与后台交互

+ 单选按钮：input:radio
  + 一组单选 name 属性相同
  + 标签必须要有对应的 value 属性
  + checked 默认选中
+ 复选按钮：input:checkbox
  + 一组复选框表单的 name 属性相同，在 name 后加 []，表示一组数据
  + 表单必须要有对应的 value 属性
  + checked 默认选中(可多)
+ 下拉列表：select>option
  + select 必须要有 name 属性
  + option 必须要有对应的 value 属性，表示每项的值
  + selected 默认选中



## 3.12 PHP 数据持久化(读写文件)

+ `file_put_contents(path, $str);`
  + 作用：向文件写入数据
  + 参数：
    + path：文件路径
    + $str：数据
  + 注意：复杂类型的数据不建议使用，格式丢失(下有解决方法)
+ `file_get_contents(path);`
  + 作用：向文件写出(读取)数据
  + 参数：
    + path：文件路径
+ 解决格式丢失
  + 说明：数据在存储之前，将数据转成带有格式的字符串。保留原有的格式，再存入文件中，方便后面读取。
  + `json_encode($info, JSON_UNESCAPED_UNICODE)`
    + 说明：将 `$info` 变量转化为 json 字符串再进行存储
    + `JSON_UNESCAPED_UNICODE` 不进行汉字编码
  + `json_decode($str, true);`
    + 说明：取得数据后再转化为数组
    + 参数：
      + `$str` 要转化的字符串
      + Boolean：true ---> 转为数组 false ---> 转为对象





# 四、HTTP 协议

+ 常见协议：
  + HTTP/HTTPS：超文本传输协议
  + FTP：文件传输协议
  + SMTP：简单邮件传输协议

+ 定义：

  + 由从客户端到服务器的请求(Request)和从服务器到客户端的相应(Response)进行的约束和规范
  + 即：HTTP 协议这就要由请求和响应构成
    + 常用的请求方法`Post` `Get` `Put` `Delete`
    + 请求(Request)：请求报文(请求行、请求头、请求主体)
    + 相应(Response)：相应报文(状态行、响应头、相应主体)

+ 特点：<font color=red> 无状态、无记忆、多次请求之间无任何关联 </font>，导致业务逻辑无法连续

+ post

  + post 请求报文

    + 请求行：请求方式/请求地址/请求协议

    + 请求头：记录大量浏览器自身的相关信息，方便服务器了解浏览器的情况，方便服务器响应。如果是 post 方式必须设置 `content-type` 为左侧取值

      `Content-type:application/x-www-form-urlencoded`

    + 请求主体：核心提交的数据

  + post 响应报文

    + 状态行：协议版本/状态码/状态主体

      403(无权访问) 404(页面未找到) 500(服务器错误) 200(成功) 302(页面重定向) 304(文档未修改)

    + 响应头：记录服务器的相关信息，让浏览器对其有所了解

    + 响应主体：服务器发给浏览器的核心数据

+ get

  + get 请求报文
    + 请求行
    + 请求头
    + 没有请求主体(原因：数据已然拼接在请求行后面)
    + 注意：get 请求不需要 `content-type` 属性，默认取值 `test/html`
    + 注意：拼接数据格式：`地址?key=value&key=value`
  + get 相应报文同 post





# 五、数据库(Mysql)

## 5.1 基本介绍

+ 数据库的分类
  + 关系型数据库：以表格的形式存储数据，将数据存储在硬盘中
  + 非关系型数据库：以键值的形式存储数据，将数据存储在内存中
+ 数据库的结构
  + 可创建多个数据库
  + 每个数据库可以有多个表
  + 表中能存储多个数据
+ 行(记录) 列(字段)
+ 数据库中常见的数据类型
  + `int` 整形
  + `float` 小数(精度缺失问题)
  + `decimal` 金钱类型(精度高的小数)
  + 字符串类型
    + `varchar(num)` 用于存储长度可变的字符串
    + `char(num)` 用于存储长度固定的字符串
    + `text` 用于存储大量的字符文章
  + `datetime` 日期时间型
+ 字段约束(列的限制条件)
  + `not null` 不为空
  + `default` 默认值
  + `Primary Key` 主键(数据唯一标识，不能为空，不能重复)
  + `auto_increment` 自动增长(一般用于主键)
  + `unique key` 不能重复



## 5.2 sql 语句

+ SQL：结构化查询语言

+ 概念：关系型数据库所使用的通用语言，为一个 ISO 标准

+ SQL语句：相当于客户端发送的命令

+ sql 操作

  + 插入数据

    `insert into 表名(字段列表) values(值列表)`

  + 查询数据(*表示全部字段)

    `select * from 表名` 全部数据查询

    `select 字段列表 from 表名 where 条件` ---> `select name, age from stu`

  + 删除数据

    `delete from 表名` 删除全表

    `delete from 表名 where 删除条件` ---> `delete from stu where id = 11`

  + 修改数据

    `update 表名 set k=v, k=v where 删除条件`

    `update 表名 set k=v, k=v` 全表更新

    `update 表名 set name="张翠花", age=18, sex="f" where id = 13 order by id` 升序

    `update 表名 set name="张翠花", age=18, sex="f" where id = 13 order by desc` 降序

+ 操作符

  + `and` 与
  + `or` 或
  + `!` 非



## 5.3 sql高级

+ `like` ---> 模糊匹配  `%` ---> 通配符

  `select * from stu where name like '张%'`

+ `in` 语法：一次查询多个符合条件的数据

  `select * from stu where id in(1,7,13,12)`

+ `count()` 获取返回数据的总条数(统计结果集行数)

  `select count(*) from stu` 查询一共有多少行

  `select count(*) as "total" from stu`  as 给 count() 取别名

+ 对结果集进行截取

  `limit 子句` 返回查找结果的前 n 行

  `select * from stu limit 0, 5` 0(索引值) 5(个数)

+ 连接查询(多个表联合查询)

  + 主键：唯一标识
  + 外键：当前表存储了别的表的主键，通过它可以关联到别的表的数据

  `select * from 表A join 表B on 表A.外键 = 表B.主键`

  `select * from teacher join class on teacher.classid=class.id;where teacher.id=4`

+ 将结果集通过字段排序

  + `order by 字段` 升序

    `select * from stu order by id`

  + `order by 字段 desc` 降序

    `select * from stu order by id desc`



# 六、PHP操作数据库

+ 链接数据库

  ```php
  // 返回值：true ---> 成功,返回数据库的连接对象  false ---> 失败
  $link = mysqli_connet(IP, 用户名, 密码, 数据库名);
  // 如果连接失败,程序到此结束
  if ($link) {
      die('....');
  }
  ```

+ 准备 sql 语句

  ```php
  $sql = "delete from stu where id = 17";
  ```

+ 将 sql 语句传递给数据库执行

  ```php
  // 成功返回ture 失败返回false
  mysqli_query($link, $sql);
  ```

+ 分析执行结果

+ 关闭数据库链接

  ```php
  // 成功返回ture 失败返回false
  mysqli_close($link);
  ```

+ 查询语句(sql 执行完成后，会产生查询结果集，需保存处理)

  + `mysqli_query` 返回true / false (非查询语句)

  + `mysqli_query` 返回结果集 / false (查询语句)

  + 返回结果集处理：

    + 获取结果集数据的方法

      ```php
      // 以关联数据的形式返回数据
      // 缺点：一次只能取一行(一条，记录),如果取完还取,返回null
      // 解决: while() {}
      // 说明：fetch(取,拿) assoc(联合) $res(结果集)
      mysqli_fetch_assoc($res);
      ```

      



# 七、会话技术(用户登录状态保存)

## 7.1 cookie

浏览器端持久化数据的容器

+ 介绍

  + cookie 中的数据可以被同一个服务器的多个页面共享
  + 默认情况下浏览器关闭，cookie 数据被销毁
  + 容量仅有 4kb 左右
  + 每次发送请求，浏览器自动把 cookie 添加到请求报文中，发送给服务器
  + 服务器设置的响应报文浏览器解析，根据响应报文内容自动设置 cookie

+ 操作 cookie

  + js 操作 cookie (频繁)

    ```js
    // 设置
    document.cookie = 'name=zs';
    document.cookie = "age=18";
    // 获取
    // 返回一个字符串 -> str.split(';') -> arr[1].split('=')
    document.cookie;
    ```

  + `jquery.cookie.js` 操作

    ```js
    // 设置
    $.cookie(k, v)
    // 获取
    $.cookie(k)
    // 设置cookie的生命周期:1天后过期
    $.cookie(k, v, { expires: 1 })
    // 删除cookie(本身没有方法删除，将数据的有效期设置为当前时间即可)
    $.cookie('name', '', { expires: -1})
    ```

  + php 操作 cookie

    ```php
    // 设置 setcookie(k, v, 有效期)
    setcookie('xh', 'zs', time() + 1*24*60*60);
    // 获取 cookie 使用超全局变量,只能用于获取,是一个只读属性
    $_COOKIE;
    ```

    Q：后台为什么可以操作 cookie (设置同理)

    A：因为浏览器请求服务器指定页面时，会在请求报文中自动携带 cookie 数据到服务器。所以服务器中可以获取 cookie，后台无法直接设置 cookie。服务器将设置信息放在响应报文中，浏览器根据响应报文设置 cookie 的数据



## 7.2 session

在服务器中存储数据的容器(可被同一服务器多个页面共享)

+ session 在使用之前，必须先开启 `session_start()`

+ session 容器是一个数据的形式，通过超全局变量 `$_SESSION` 进行取值和设置

+ 步骤

  ```php
  // 开启session机制
  session_start();
  // 设置
  $_SESSION['username'] = 'zs';
  // 获取
  $r = $_SESSION['username'];
  // 删除
  unset($_SESSION['age']);
  // 清空
  $_SESSION = [];
  ```

+ `session_start()` 的作用

  + 随机生成 `sessionID` 通过 `session_id()` 查看
  + 创建一个 session 文件用于存储数据，文件名以 `sess + sessionID`
  + 通过 `setcookie()` 将上次 `sessionID` 传递给浏览器从而设置 cookie 存储 `sessionID`





# 八、XML 文件格式

前后端常见数据传输格式

+ 介绍

  + 定义：可拓展的标记语言
  + HTML：超文本标记语言
  + 共同点：都是标记语言(都要使用标签进行标记)
  + 不同点：
    + 作用不同
      + XML：存储和传递数据
      + HTML：展示数据
    + HTML 标签定义好，标签有语义。XML 标签可拓展，可自定义

+ 语法规范

  + 第一行必须是版本信息

    `<? xml version="1.0" encoding="utf-8" ?>`

  + 只能有一个根标签

  + 属性使用双引号

  + 特殊符号使用转义

  + 其它标准同 HTML 一致

+ JS 解析 XML

  + 获取服务器返回的 xml 数据，需要使用 `xhr.responseXML` 是一个 dom 对象

    ```js
    var data = xhr.responseXML;
    ```

  + 获取所有

    ```js
    // 实例获取标签文字，用innerHTML,因为无innerText属性
    var students = data.querySelectorAll('student')
    ```

+ php 获取 xml 文件内容

  + 如需要返回 xml 数据，需要把 `content-type` 改为 `text/xml` 不然浏览器会以 `text/html` 进行解析

    ```php
    header('content-type:text/xml;charset:utf-8');
    ```

  + 获取文件内容

    ```php
    // 参数:xml的文件路径
    $result = file_get_contents('data.xml');
    ```

+ XML 缺点：解析过于复杂，体积过大，用的少

