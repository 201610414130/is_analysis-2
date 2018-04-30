# 实验4：图书管理系统顺序图绘制

|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414325|软工三班|张文|![myself](../myself.jpg "myself")

## 图书管理系统的顺序图
### 1.借书用例
1.1 借书用例PlantUML源码
<pre>
@startuml
actor 图书管理员
participant 读者
participant 资源项
participant 馆藏资源品种
participant 借书记录

图书管理员 -> 读者:验证读者
activate 读者
loop
图书管理员 -> 读者:读取读者限额
activate 读者
图书管理员 -> 资源项:获取资源项
activate 资源项
资源项 -> 馆藏资源品种:查找资源品种
activate 馆藏资源品种
图书管理员 ->借书记录:创建借书记录
activate 借书记录
图书管理员 ->资源项:借出资源
activate 资源项
资源项 ->馆藏资源品种:减少库存
activate 馆藏资源品种
图书管理员 ->读者:减少可用限额
activate 读者
end
图书管理员->借书记录:打印借书清单
activate 借书记录
@enduml
</pre>

1.2 借书用例顺序图

![借出图书](借出资源.png '借出图书')

1.3 借书用例顺序图说明
本用例由图书管理员操作，需要对读者的信息进行验证，才能执行图书借阅记录的创建等操作，并同时对图书表中的库存数进行更新，逾期记录表由系统进行创建，无需操作

### 2. 归还图书用例
2.1 归还用例PlantUML源码
<pre>
@startuml
actor 图书管理员
participant 资源项
participant 借书记录
participant 馆藏资源品种
participant 读者
participant 逾期记录

activate 图书管理员
图书管理员->资源项:读取资源信息
activate 资源项
资源项->借书记录:取借书记录
activate 借书记录
资源项->馆藏资源品种:取资源的品种
activate 馆藏资源品种
图书管理员 ->读者:取借阅信息
activate 读者
图书管理员->资源项:归还资源
资源项 ->馆藏资源品种:增加可借数量
图书管理员->借书记录:增加可借数量
opt [逾期]
图书管理员->逾期记录:登记逾期记录
end
@enduml
</pre>

2.2 归还用例顺序图
![归还图书](归还资源.png '归还图书')

2.3 归还图书用例说明

该用例actor为图书管理员，先获取资源信息，在对比读者的借阅信息，结合逾期记录进行归还的判断

### 3. 续借图书用例
3.1 续借图书用例PlantUML源码
<pre>
@startuml
actor 图书管理员
participant 资源项
participant 借书记录
participant 馆藏资源品种
participant 读者
participant 逾期记录
activate 图书管理员
图书管理员->资源项:读取资源信息
activate 资源项
资源项->借书记录:取借书记录
activate 借书记录
资源项->馆藏资源品种:取资源的品种
activate 馆藏资源品种
图书管理员->读者:取借阅信息
activate 读者
图书管理员->逾期记录:获取逾期记录
activate 逾期记录
图书管理员->读者:更新还书日期
图书管理员->逾期记录:更新逾期记录
@enduml
</pre>

3.2 续借图书用例顺序图
![](续借图书.png '续借图书')

3.3 续借图书用例顺序图说明
续借图书与借出图书大致相同，增加了对逾期记录的判断，续借图书后，更新逾期记录

### 4.预定图书用例顺序图
4.1 预定图书用例顺序图PlantUML源码
<pre>
@startuml
actor 读者
participant 读者信息
participant 资源项
participant 馆藏资源品种
participant 预定记录
读者->读者信息:获取读者信息
activate 读者信息
读者->读者信息:获取读者限额
读者->资源项:获取资源项
activate 资源项
资源项->馆藏资源品种:获取馆藏资源
activate 馆藏资源品种
读者->预定记录:创建预定记录
activate 预定记录
读者->馆藏资源品种:减少库存
读者->读者信息:减少限额
@enduml
</pre>

4.2 预定图书用例顺序图
![](预定图书.png '预定图书')

4.3 预定图书用例顺序图说明
预定图书的actor为读者，读者会使用相应账户进行登录，借阅的时候操作由系统完成

### 5.增删用户用例顺序图
5.1 增删用户用例图PlantUML源码
<pre>
@startuml
actor 系统管理员
participant 用户信息
participant 读者信息
系统管理员->用户信息:验证身份
activate 用户信息
系统管理员->读者信息:获取读者信息
activate 读者信息
系统管理员->读者:增/删操作
activate 读者
@enduml
</pre>

5.2 增删用户用例顺序图
![](增删用户.png '增删用户')

5.3 增删用户用例顺序图说明
本实例的actor为系统管理员，系统管理员对用户表进行增删操作

### 6.新书校验用例顺序图
6.1 新书校验用例图PlantUML源码
<pre>
@startuml
actor 图书管理员
participant 用户信息
participant 馆藏资源品种
图书管理员->用户信息:验证身份
activate 用户信息
图书管理员->馆藏资源品种:新书验证
activate 馆藏资源品种
图书管理员->馆藏资源品种:增加库存
@enduml
</pre>

6.2 新书校验用例顺序图

![](新书校验用例.png '新书校验')

6.3 新书校验用例顺序图说明
本实例的actor为图书管理员，图书管理员对官场资源进行增删操作
