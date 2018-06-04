## 接口:getWorks [返回](../用例/查看实验用例.md)
----
用例:参看实验
* 权限:学生，老师均能查看
* 功能:返回实验信息
* API请求地址:项目地址/work/getWorks
* 请求方式:GET
* 求情参数说明:无
* 返回实例:
<pre>
{
      "code": 200,
      "msg": null,
      "total": 30,
      "data": [
          {
            "test_id":"1",
            "test_name":"实验1:业务流程建模",
            "test_content":"实验要求",
            "end_time":"截止日期",
            },{
              ...其他实验
          }
      ]
  }
</pre>

* 返回参数说明:

|参数名称|说明|
|:-:|:-:|
|code|返回的状态码(200为正常)|
|msg|返回的信息|
|total|返回的实验总数|
|data|返回的实验列表|
|testt_id|实验ID|
|test_name|返回的实验名称|
|test_content|返回的实验要求|
|end_time|返回的实验截止日期|
