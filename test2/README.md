|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414325|软工三班|张文|![myself](../myself.jpg "myself")

# 1.图书管理系统用例关系图

## 1.1 用例图PlantUml源码如下:

<pre>
@startuml
left to right direction
actor 读者
usecase 图书查询
usecase 个人信息查询
usecase 图书借阅
usecase 逾期处理
usecase 预订
读者-->图书查询
读者-->个人信息查询
读者-->图书借阅
读者-->预订
actor 图书管理员
usecase 还书
usecase 续借
usecase 维护读者信息
usecase 管理图书信息
逾期处理<--图书管理员
还书.>逾期处理:extend
续借<--图书管理员
读者-->还书
图书借阅.>续借:extend
维护读者信息<--图书管理员
管理图书信息<--图书管理员
usecase 新书校验
usecase 维护图书数据
usecase 增加图书记录
usecase 更新删除图书记录
usecase 订购图书
新书校验<.管理图书信息:include
维护图书数据<.管理图书信息:include
增加图书记录<.管理图书信息:include
增加图书记录<.管理图书信息:include
更新删除图书记录<.管理图书信息:include
订购图书<.管理图书信息:include
actor 系统管理员
usecase 系统维护
usecase 日志维护
usecase 权限维护
usecase 增删用户
usecase 后台数据维护
系统维护<--系统管理员
日志维护<.系统维护:include
权限维护<.系统维护:include
增删用户<.系统维护:include
后台数据维护<.系统维护:include
@enduml
</pre>
## 1.2. 用例图如下

参见图1.1

![](图书管理系统.png '用例图')

# 2.参与者说明:


## 2.1. 图书管理员

主要职责是: 图书的更新与维护，完成用户的数的借阅与归还，以及用户信息的更新与维护

## 2.2. 用户

主要职责: 图书的查询，借阅与归还

## 2.3. 系统管理员

主要职责：图书管理系统的维护

# 3.用例规约表


## 3.1 "借出图书"用例
参见表3.1

<table>
      <tr>
			   <th>用例名称</th>
			   <th>借出图书</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>图书管理员</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>用户发出借书请求</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>更新图书与用户信息</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 获取相应图书 <br/>
             5. 将相应图书交于用户<br/>
             6. 更新用户借阅信息<br/>
             7. 更新图书信息</th>
			   <th>2. 传递给管理员相应图书信息<br/>
             3. 显示图书借阅情况<br/>
             4. 确认图书库存<br/>
             8. 将图书信息更新<br/>
             9. 对图书归还计时</th>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">4a. 图书库存已为0<br/>
                1. 提示没有图书，结束用例<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1. 同一类型图书，有多本，应该有详细的信息记录<br/>
             2. 一次借阅最长时间为一周，逾期将会计算罚款<br/>
              </th>
      </tr>
</table>

### “借出图书”用例流程图源码如下:
<pre>
@startuml
start
:获取图书信息;
if ("库存充足") then (true)
    :借书成功;
    else (no)
    :借书失败，提示库存不足;
    endif
:更新图书信息;
:更新用户信息;
stop
@enduml
</pre>
### "借出图书"用例流程图如下:
![](借阅.png '借阅')

## 3.2 "归还图书"用例
参见表3.2

<table>
      <tr>
			   <th>用例名称</th>
			   <th>归还图书</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>图书管理员</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>用户发出还书请求</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>更新图书与用户信息</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 获取相应图书 <br/>
             5. 将相应图书归入入库<br/>
             6. 更新用户借阅信息<br/>
             7. 更新图书信息</th>
			   <th>2. 传递给管理员相应图书信息<br/>
             3. 显示图书借阅情况<br/>
             4. 确认图书库存<br/>
             8. 将图书信息更新<br/>
             9. 对图书借阅的时间进行核对</th>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">9a. 图书归还日期已经超过<br/>
                1. 提示超过归还日期，需要进行罚款措施<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1. 同一类型图书，有多本，应该有详细的信息记录<br/>
             2. 一次借阅最长时间为一周，逾期将会计算罚款<br/>
              </th>
      </tr>
</table>

### “归还图书”用例流程图源码如下:
<pre>
@startuml
start
:获取图书信息;
if ("归还为逾期") then (true)
    :还书成功;
    else (no)
    :还书失败，需要缴纳罚款;
    endif
:更新图书信息;
:更新用户信息;
stop
@enduml
</pre>
### "归还图书"用例流程图如下:
![](还书.png '还书')

## 3.3 "续借图书"用例
参见表3.3

<table>
      <tr>
			   <th>用例名称</th>
			   <th>续借图书</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>图书管理员</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>用户发出续借请求</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>更新图书与用户信息</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 获取相应图书 <br/>
             5. 将相应图书归入入库<br/>
             6. 更新用户借阅信息<br/>
             7. 更新图书信息</th>
			   <th>2. 传递给管理员相应图书信息<br/>
             3. 显示图书借阅情况<br/>
             4. 确认图书库存<br/>
             8. 将图书信息更新<br/>
             9. 对图书借阅的时间进行核对</th>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">9a. 图书归还日期已经超过<br/>
                1. 提示超过归还日期，需要进行罚款措施之后才能续借<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1. 同一类型图书，有多本，应该有详细的信息记录<br/>
             2. 一次借阅最长时间为一周，逾期将会计算罚款<br/>
              </th>
      </tr>
</table>

### “续借图书”用例流程图源码如下:
<pre>
@startuml
start
:获取图书信息;
if ("归还为逾期") then (true)
    :可以进行续借;
    :图书借阅时间延长;
    else (no)
    :续借失败，需要缴纳罚款;
    if("不缴纳罚款") then (true)
      :续借失败，结束用例;
      else(no)
      :续借成功;
      endif;
    endif
:更新图书信息;
:更新用户信息;
stop
@enduml
</pre>
### "归还图书"用例流程图如下:
![](续借.png '续借')

## 3.4 "预定图书"用例
参见表3.4

<table>
      <tr>
			   <th>用例名称</th>
			   <th>预定图书</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>用户</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>图书管理系统有预定功能</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>图书充足</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 登录查询图书 <br/>
             5. 订阅相应图书<br/>
             6. 向管理员发出请求<br/>
             8. 等待并获取图书</th>
			   <th>2. 反馈相应图书信息<br/>
             3. 显示图书借阅情况<br/>
             4. 返回图书库存<br/>
             7. 管理员进行进行预定操作<br/>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">
                1a. 用户为非法用户<br/>
                1. 提示其进行注册<br/>
                4a. 图书库存不足<br/>
                1. 提示图书数量不足<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1. 同一类型图书，有多本，应该有详细的信息记录<br/>
             2. 一次借阅最长时间为一周，逾期将会计算罚款<br/>
              </th>
      </tr>
</table>

### “预定图书”用例流程图源码如下:
<pre>
@startuml
start
:登录;
if (用户不合法) then (true)
      :提示注册，或者申请解封;
    else (no)
    :登录成功;
    endif;
:查询图书;
:预定图书;
if(图书不存在或者没有库存) then (true)
    :提示现在无法进行预定;
    else (no)
    :提示预订成功;
    endif
stop
@enduml
</pre>
### "预定图书"用例流程图如下:
![](预定.png '预定')

## 3.5 "增删用户"用例
参见表3.5

<table>
      <tr>
			   <th>用例名称</th>
			   <th>增删用户</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>系统管理员</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>图书管理系统数据正常</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>更新图书管理系统</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 系统管理员身份登录 <br/>
             3. 进入用户管理界面<br/>
             4. 执行用户增删操作<br/>
			   <th>2. 进入系统管理员界面<br/>
             5. 对用户执行相应操作<br/>
             6. 返回执行结果<br/>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">
                1a. 用户不是系统管理员<br/>
                1. 提示其重新登录<br/>
                5a. 删除用户不存在<br/>
                1. 提示删除用户不存在<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1.每个操作都有相应提示<br/>
             2. 每次操作系统都有相应备份<br/>
              </th>
      </tr>
</table>

### “增删用户”用例流程图源码如下:
<pre>
@startuml
start
:登录;
if (非系统管理员) then (true)
      :提示重新输入账号密码;
    else (no)
    :登录成功;
    endif;
:增加用户;
if(用户名不合法) then (true)
    :提示用户名不合法;
    else (no)
    :提示增加成功;
    endif
:删除用户;
if(用户名不存在) then (true)
    :提示用户名不存在;
    else (no)
    :提示删除成功;
    endif
stop
@enduml
</pre>
### "增删用户"用例流程图如下:
![](用户操作.png '用户操作')

## 3.6 "新书校验"用例
参见表3.6

<table>
      <tr>
			   <th>用例名称</th>
			   <th>新书校验</th>
      </tr>
      <tr>
			   <th>参与者</th>
			   <th>图书管理员</th>
      </tr>
      <tr>
			   <th>前置条件</th>
			   <th>图书管理系统数据正常</th>
      </tr>
      <tr>
			   <th>后置条件</th>
			   <th>更新图书管理系统图书数据</th>
      </tr>
      <tr>
			   <th colspan="2">主事件流</th>
      </tr>
      <tr>
			   <th>参与者动作</th>
			   <th>系统行为</th>
      </tr>
      <tr>
			   <th>1. 图书管理员身份登录 <br/>
             3. 进入图书管理界面<br/>
             4. 执行新书校验操作<br/>
			   <th>2. 进入图书管理员界面<br/>
             5. 对用户执行相应操作<br/>
             6. 返回执行结果<br/>
      </tr>
      <tr>
			   <th colspan="2">备选时间流</th>
      </tr>
      <tr>
         <th colspan="2">
                1a. 用户不是图书管理员<br/>
                1. 提示其重新登录<br/>
                5a. 新书信息有误<br/>
                1. 提示重新录入书籍<br/>
              </th>
      </tr>
      <tr>
         <th colspan="2">业务规则</th>
      </tr>
      <tr>
         <th colspan="2">1.每个操作都有相应提示<br/>
             2. 每次操作系统都有相应备份<br/>
              </th>
      </tr>
</table>

### “增删用户”用例流程图源码如下:
<pre>
@startuml
start
:登录;
if (非图书管理员) then (true)
      :提示重新输入账号密码;
    else (no)
    :登录成功;
    endif;
:新书校验;
if(新书信息不合法) then (true)
    :提示新书信息不合法;
    else (no)
    :提示校验成功;
    endif
stop
@enduml
</pre>
### "增删用户"用例流程图如下:
![](新书校验.png '新书校验')

由于本次写的用例图里面的用例写的有点多，我还有其他事情要做，
就写了其中比较常见的用例的规约表与流程图
