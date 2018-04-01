|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414325|软工三班|张文| |![myself](https://github.com/Anntly/is_analysis/blob/master/myself.jpg "myself")
# PlantUml作业
flow1代码
===

<pre>
@startuml
:安排考试;
:考试安排表;
:出卷;
split
:A,B试卷<
:审批签字;
:打印审批表;
split again
:A,B试卷;
end split
:打印试卷;
:试卷<
:参加考试;
:答卷;
:阅卷出成绩;
fork
:答卷;
:装订成册;
fork again
:成绩单;
if(有不及格?) then (yes)
:安排补考;
:补考安排表;
endif
end fork
:期末流程结束;
@enduml
</pre>

flow1图片
===

![](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuR9wkgxpMT-a5mtDBzPFjUQoWZ2WWWjNM0CLjEzwshlTcgku82UpXClAKSS9g00eOWFIk_1PvyxdQ_SzNJiTgF9Pv-IdlHiWWa2zK2qAYUc9cNamZM2ZKlDI5C1oC3qm2Ik4qVrDJxiMm9trVEqKY8ANCrg13A2RddLCUBvxfJLNMdvHDfByYyMjBzOj0ae-RUk1ICBiXsXusWiqBZDDuzcSpYSxUf_sTprRiCTUKw4a8pLFGQCojLWJ7Y8Bbm9j1ve8OS131Epwp3Im7o1sFvip_zcSrS-sDZvVqVryz-HdS-TRSpa0fK712m00 'flow1')

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
![](http://www.plantuml.com/plantuml/png/PP7DJi9058NtynHTmYkq2taL4eiI4HF0tMmmXbH2RLKiF_wO4WMYiIMHy4CJV9cvTyfRU3kr2GcRPdBkFUSxDotK6yLQu_AymZW48xIMd2c5wRBx4uTBVBQXxHkCYzMG7Z9ofDlYh5pAOJz4RoQxKpA1splAQurJiwebUfxSWoWEPcca-FMn6HhChDHDBITMjbengyVb4jF5ghthJUF95OHl1jF1Ma0mH6-DlcLadL9UvEEriqy2TwnYqk0C_BsDoQHgWsk1spaeNxgedH4fkC7RUrX-YCt6K9fMF2cMgza4Nrpq1aO2q9JZt-P_GMk0yoqvmNxSc_CqYpDzDsg1usK1sH6aVtQmku3r8Wq1nzwDBJegdZGFIkfYymvFhtiW7iz7j408kElJWemUPD1J1LY1FibF_0C0 'flow2')
该图是一个泳道图，有4个角色，客户，业务经理，工人与财务人员，首先客户申请服务，业务经理进行判断是否为新用户，之后上门观察，制定方案，用户对其满意程度进行反馈，之后业务经理安排工人与材料，填写派工单，工人领取材料，客户验收并反馈意见，业务经理交回派工单，最终财务人员结算
