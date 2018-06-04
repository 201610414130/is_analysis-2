## 接口:getStudents [返回](../用例/学生列表用例.md)
----
用例:学会列表
* 权限:学生:不能看到成绩，只能看到成绩等级;老师:可以看到成绩
* 功能:返回学生列表
* API请求地址:项目地址/index/getStudents
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
            "student_id":"201510414325",
            "student_name":"张文",
            "class_name":"软件三班",
            "github_name":"Anntly",
            "update_time":"2018.06.02",
            "grade_p":"ABBBBA",
            "web_sum":"011111"
            },{
              ...其他学生
          }
      ]
  }
</pre>

* 返回参数说明:

|参数名称|说明|
|:-:|:-:|
|code|返回的状态码(200为正常)|
|msg|返回的信息|
|total|返回的学生总数|
|data|返回的学生列表|
|student_id|学号|
|student_name|返回的学生姓名|
|class_name|返回的学生班级|
|github_name|返回的github地址|
|update_time|更新时间|
|grade_p|返回的成绩等级|
|web_sum|返回的网址信息|
