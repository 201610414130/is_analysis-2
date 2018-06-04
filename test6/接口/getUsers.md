## 接口:getUsers [返回](../用例/用户列表用例.md)
----
用例:用户列表
* 权限:管理员
* 功能:返回用户信息
* API请求地址:项目地址/User/getUsers
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
            "user_id":"1",
            "user_name":"AAA",
            "user_status":"用户状态",
            "role":"用户角色",
            },{
              ...其他用户
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
|user_id|用户Id|
|user_name|用户名|
|user_status|用户状态|
|role|角色|
