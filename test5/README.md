# 实验5：图书管理系统数据库设计与界面设计

|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414325|软工三班|张文|![myself](../myself.jpg "myself")

## 1. 数据库表设计

### 1.1. 馆藏资源品种表（ItemsCategory）

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|name|varchar(32)||false|||资源分类|
|ISBN|varchar(32)|主键|false|||全球唯一编码|
|price|float||false|||价格|
|detail|varchar(512)||true|||资源介绍|
|number|bigint||false|0||馆藏数量|
|stock|bigint||false|0||库存|

### 1.2. 碟片品种(disk)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|name|varchar(32)||false|||碟片种类|
|id|int|主键|false|||主键id|
|number|bigint||false|0||数量|
|ISBN|varchar(32)|外键|false|||ISBN号|
|publisher|varchar(512)||true|||发行商|

### 1.3. 图书品种(book)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|name|varchar(32)||false|||图书种类|
|id|int|主键|false|||主键id|
|number|bigint||false|0||数量|
|ISBN|varchar(32)|外键|false|||ISBN号|
|publisher|varchar(512)||true|||出版社|
|publishDate|date||true|||发行时间|

### 1.4. 电子作品(e_book)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|name|varchar(32)||false|||电子作品种类|
|id|int|主键|false|||主键id|
|number|bigint||false|0||数量|
|publisher|varchar(512)||true|||发行商|
|status|int||false|0||更新状态(0：连载中 1：已完结)|

### 1.5. 资源项(resourceitem)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|flownumber|varchar(32)|主键|false|||流水号|
|status|int||false|0||流水号状态<br/>0:正常 1：异常|

### 1.6. 预定记录(reserve)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|id|varchar(32)|主键|false|||预定id|
|user_id|varchar(32)|外键|false|||用户id|
|book_id|varchar(32)|外键|false|||图书id|
|disk_id|varchar(32)|外键|false|||碟片id|
|e_book_id|varchar(32)|外键|false|||电子作品id|
|total|float||false|||总价|
|createtime|date||false|||创建时间|
|updatetime|date||false|||更新时间|
|ordertime|date||false|||预定时间|
|status|int||false|0||预定状态<br/>0:预定中 1：取消预订 2：预定结束|

### 1.7. 借书记录(orders)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|id|varchar(32)|主键|false|||预定id|
|user_id|varchar(32)|外键|false|||用户id|
|book_id|varchar(32)|外键|false|||图书id|
|disk_id|varchar(32)|外键|false|||碟片id|
|e_book_id|varchar(32)|外键|false|||电子作品id|
|total|float||false|||总价|
|createtime|date||false|||创建时间|
|updatetime|date||false|||更新时间|
|status|int||false|0||订单状态<br/>1：借出状态 2：归还 3：取消|

### 1.8. 用户(user)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|id|varchar(32)|主键|false|||用户id|
|nickname|varchar(32)||true|||用户昵称|
|birthday|date||true|||出生日期|
|role|int||false|0||用户角色<br/>0:普通用户 1:图书管理员 2:系统管理员|
|username|varchar(32)||false|||用户名|
|password|varchar(64)||false|||用户密码|
|phone|varchar(20)||true|||手机号|
|email|varchar(32)||true|||邮箱|
|createtime|date||false|||创建时间|
|updatetime|date||false|||更新时间|

### 1.9. 逾期记录(overdue)

|字段|类型|主键，外键|null|默认值|约束|说明|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|id|varchar(32)|主键|false|||逾期记录id|
|user_id|varchar(32)|外键|false|||用户id|
|fine|float||false|0||罚款|

## 2. 界面设计

### 2.1. 借书界面设计

![](借书界面.png '借书界面')

* 用例图参见: 借书用例
* 类图参见：借书类，读者类
* 顺序图参见： 借书顺序图
* API接口如下：

 1.获取全部分类API
   * 功能：用于获取全部分类
   * 请求地址 :http://Localhost:8080/bookmanager/book/list
   * 请求方法 Get
   * 请求参数

|参数名称|必填|说明|
|:-:|:-:|:-:|
|categoryId|是|商品分类ID|

   * 返回实例
   <pre>
   {
  "code": 200,
  "msg": "success",
  "data": [
    {
      "bookId": "161873371171128075",
      "bookName": "信息系统分析与设计",
      "stock": "20",
      "createTime": 1490171219,
      "updateTime": 1490171219,
    },
    {
      "bookId": "161873371171128075",
      "bookName": "信息系统分析与设计",
      "stock": "20",
      "createTime": 1490171219,
      "updateTime": 1490171219,
    }]
}
   </pre>

|参数名称|说明|
|:-:|:-:|
|code|返回的状态码|
|msg|返回的信息|
|data|返回的数据|

1.借阅图书API
  * 功能：提交订单
  * 请求地址 :http://Localhost:8080/bookmanager/book/order
  * 请求方法 Post
  * 请求参数

|参数名称|必填|说明|
|:-:|:-:|:-:|
|bookId|是|图书ID|
|bookName|是|图书名|
|number|是|数量|

  * 返回实例
  <pre>
  {
 "code": 200,
 "msg": "success",
 "data":null,
  </pre>

|参数名称|说明|
|:-:|:-:|
|code|返回的状态码|
|msg|返回的信息|
|data|返回的数据|
