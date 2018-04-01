|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414325|软工三班|张文|![myself](../myself.jpg "myself")
# PlantUml作业
flow1代码
===

<pre>
@startuml
|教务处|
startme
:安排考试;
:考试安排表]
|#AntiqueWhite|教师|
:出卷;
fork
    :A、B试卷]
fork again
    :打印审批表]
|#AntiqueWhite|系主任|
    :审批签字;
    :打印审批表;
end fork
|#AntiqueWhite|教务处|
:打印试卷;
:试卷]
|#AntiqueWhite|学生|
:参加考试;
:答卷]
|#AntiqueWhite|教师|
:阅读出成绩;
fork
    :成绩单]
|#AntiqueWhite|教务处|
if (有不及格) then (有)
    fork
    :安排补考;
    :补考安排表]
    detach
    end fork
endif
|#AntiqueWhite|教师|
fork again
    :答卷]
    :装订存档;
end fork
:期末流程结束;
stop
@enduml
</pre>

flow1图片
===

![](flow1.png 'flow1')

该流程图从考试安排开始，安排考试出卷后两个分支同时进行，分别为试卷的审批已打印审批表，之后打印试卷，再参加考试，之后答卷，出阅卷成绩，有不及格就安排补考，最终期末流程结束

flow2代码
===
<pre>
@startuml
|客户|
start
:申请服务;
|业务经理|
if(是新用户吗?) then (是)
:登记客户信息;
else (不是)
endif
:上门观察;
:制定方案;
|客户|
if(满意吗?) then (否)
end
else (是)
:签订服务合同;
|业务经理|
fork
:安排工人;
fork again
:安排材料;
end fork
fork
:填写派工单;
end fork
|工人|
:领取材料;
|客户|
:验收并填写反馈意见;
|业务经理|
:交回派工单;
|财务人员|
:结算;
end
@enduml
</pre>

flow2图片
===
![](flow2.png 'flow2')
该图是一个泳道图，有4个角色，客户，业务经理，工人与财务人员，首先客户申请服务，业务经理进行判断是否为新用户，之后上门观察，制定方案，用户对其满意程度进行反馈，之后业务经理安排工人与材料，填写派工单，工人领取材料，客户验收并反馈意见，业务经理交回派工单，最终财务人员结算
