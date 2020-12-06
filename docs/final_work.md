![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_420fd467a46ce234121eaf7b8a412a77.PNG)


# 看板应用设计

- [看板应用设计](#看板应用设计)
  - [一、需求分析](#一需求分析)
    - [1. 问题陈述](#1-问题陈述)
    - [2. 用例模型](#2-用例模型)
      - [a. 用例图](#a-用例图)
      - [b. 用例规约](#b-用例规约)
    - [3. 补充规约](#3-补充规约)
    - [4. 术语表](#4-术语表)
  - [二、架构设计](#二架构设计)
    - [1. 系统架构描述](#1-系统架构描述)
      - [a. 信息浏览和编辑模块](#a-信息浏览和编辑模块)
      - [b. 其他模块](#b-其他模块)
    - [2. 系统架构图](#2-系统架构图)
    - [3. 系统关键类的析取](#3-系统关键类的析取)
  - [三、用例分析](#三用例分析)
    - [1. 补充用例规约](#1-补充用例规约)
    - [2. 用例中类的析取](#2-用例中类的析取)
      - [a. 登录用例类的析取：](#a-登录用例类的析取)
      - [b. 浏览统计报表用例类的析取：](#b-浏览统计报表用例类的析取)
      - [c. 修改个人信息用例类的析取：](#c-修改个人信息用例类的析取)
      - [d. 完成待办事项用例类的析取：](#d-完成待办事项用例类的析取)
      - [e. 创建代办事项用例类的析取：](#e-创建代办事项用例类的析取)
      - [f. 小组成员管理用例类的析取：](#f-小组成员管理用例类的析取)
    - [3. 分析机制](#3-分析机制)
    - [4. 合并分析类](#4-合并分析类)
  - [五、 子系统及其接口设计](#五-子系统及其接口设计)
  - [六、部件设计](#六部件设计)
    - [1. 分析并发需求](#1-分析并发需求)
    - [2. 解决方案](#2-解决方案)
    - [3. （进程）生命周期](#3-进程生命周期)
    - [4. 映射到现实系统](#4-映射到现实系统)

## 一、需求分析

### 1. 问题陈述

看板管理方法是在同一道工序或者前后工序之间进行物流或信息流的传递。本项目就是一个类似看板的管理工具，高效实现任务的发布和领取，避免重复劳动，提高沟通效率。

### 2. 用例模型

#### a. 用例图


![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_f674efc9c6cf7b938d30f0b7c1e47e03.png)


#### b. 用例规约



|用例名称：|登录|
|------|------|
|角色 | 所有用户|
|用例说明|用户必须先登录进入系统才能完成后续操作|
|前置条件|成功进入网站首页|
|基本事件流| ![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_065d88391e0cf14cb0fe3ea890aa8330.png) |
|异常事件流|用户名不存在，密码输入错误|
|后置事件|登陆成功，进入用户个人页面|

|用例名称：|浏览统计报表|
|------|------|
|角色 | 所有用户|
|用例说明|管理员可以浏览所有team的报表，其他类型的用户可以浏览自己小组的报表|
|前置事件|登录成功，进入报表页面|
|基本事件流|![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_0792f4fe31bbc101a1f0ef02e12dd1b8.png)|
|异常事件流|返回统计数据失败|
|后置事件|无|

|用例名称：|修改个人信息|
|------|------|
|角色 | 所有用户|
|用例说明|修改姓名，联系方式等信息|
|前置条件|登录成功并进入个人信息页面|
|基本事件流|![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_df73369f66f8b6cbe9637462b19a7f51.png)|
|异常事件流||
|后置事件|停留在个人信息页面|

|用例名称：|完成待办事项|
|------|------|
|角色 | 普通用户|
|用例说明|查看待办事项，同时可以修改其状态为已完成|
|前置条件|已登录，进入待办事项页面|
|基本事件流|![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_b46e89513278fc54e54ca8ac5e16719b.png)|
|异常事件流|输入的信息无效|
|后置事件|仍停留在待办事项页面|

|用例名称：|创建待办事项|
|------|------|
|角色 |管理用户|
|用例说明|创建一个待办事项给一个小组|
|前置条件||登录成功，进入待办事项管理页面|
|基本事件流|![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_515f7b38ec0bd0ba33d1751737fa715f.png)|
|异常事件流|当前用户无权限创建待办事项|
|后置事件|停留在当前页面|

|用例名称：|小组成员管理|
|------|------|
|角色 | 管理用户|
|用例说明|向小组增加/移除成员，小组不存在则创建，小组没有成员则删除小组|
|前置条件|登录成功，进入小组管理页面|
|基本事件流|![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_8ad82332d1f0b0741441efb9fe4af67e.png)|
|异常事件流|用户无权限，成员不存在|
|后置事件|停留在原页面|

### 3. 补充规约

有部分流程趋同或较简单的用例先省略，如注册、登出等等。

### 4. 术语表

|术语|解释|
|---|---|
|manager|管理用户、项目领导、leader等等均指同一个概念|
|member|普通用户、组员等均为同一个概念|

## 二、架构设计
### 1. 系统架构描述


#### a. 信息浏览和编辑模块
使用 MVC 模式，该模式由 Model、View 以及 Controller构成，是成熟、广泛使用，对本问题也足够适用的一种模式。
• View 层提供了系统与用户交互的界面，本系统运行在浏览器上，通过Vue.js来建立视图，其数据将由 Controller 提供。
• Controller 层是串联 Model 层与 View 层的层次，当用户发布或修改数据时，该层次将接受到通过 View 层传过来的用户交互的数据，并更新 Model 层的状态，对用户个人信息，待办任务等数据进行增删改查。同时在用户请求View层访问时将数据传到 View 层进行展示。
• Model 层是用户数据模型，保存用户的个人信息和任务。

#### b. 其他模块

消息处理模块
监听模式：由用户浏览器和服务器间异步的超文本数据传输实现

### 2. 系统架构图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_bc1e76303828cd15d4de9d49a91a8dd0.png)


### 3. 系统关键类的析取

Member：
每个员工隶属于一个部门，即关联一个经理。
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_4c2b1b4ea85e39ee6e399a46d018ef1e.png)

Manager：
关联一定量的员工。
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_31b49afa1582405428807b55b435f5df.png)



Task:
由经理发布任务在TodoList上，由一个或多个员工认领任务，并确认任务完成。故每个Task关联一个经理，关联一个或多个员工，附属于TodoList。
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_5b1198e4a62cbd47ca44e34fdcc17dfd.png)


TodoList：
经理在TodoList发布Task，员工在TodoList认领并确认任务完成。包含多个Task。
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_f0ff724f08649deecde09ef819422029.png)


Team：
由经理和员工组成。
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_9abb789e8aca08c058711e0f1198d0fb.png)



## 三、用例分析

### 1. 补充用例规约

暂无

### 2. 用例中类的析取

#### a. 登录用例类的析取：

实体类：User。User实体类表示用户实体，包含用户名、密码。
控制类：LoginValid。LoginValid控制类负责处理关于登录的相关操作，包括验证用户名是否存在、验证密码是否正确、登录成功页面跳转。
边界类：Login。Login边界类为登录页面。
用例析取图,时序图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_a5ab22a6fd1bf4ac85c0428383606d79.png)


#### b. 浏览统计报表用例类的析取：

实体类：ReportModel。ReportModel实体类表示报表实体，包含报表内容、报表所属小组。
控制类：ReportShow。ReportShow控制类负责处理关于报表显示的相关操作，包括验证用户类型、显示报表信息。
边界类：Report。Report为报表排布显示页面。
用例析取图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_9e98c1600d0610bf75c513da97d9b686.png)


#### c. 修改个人信息用例类的析取：

实体类：PersonalInfo。PersonalInfo实体类表示个人信息实体，包含昵称、性别、头像、用户类型、绑定邮箱、电话号码。
控制类：ChangeInfo。ChangeInfo控制类负责处理关于信息修改的相关操作，包括修改非法判断、更新个人信息、修改非法提醒。
边界类：Change。Change为个人信息修改页面。
用例析取图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_6cdcb2155b4f3c758103e046c61ec632.png)


#### d. 完成待办事项用例类的析取：
实体类：TodoModel。TodoModel实体类表示待办事项实体，包含todo标题、todo内容、todo截止时间和开始时间、todo的参与小组。
控制类：FinishTodo。FinishTodo控制类负责处理关于完成代办事项的相关操作：完成代办事项。
边界类：EndTodo。EndTodo为确认完成待办事项页面。
用例析取图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_5228f4e2db69478aa16dfadc5ebc6256.png)



#### e. 创建代办事项用例类的析取：
实体类：TodoModel。TodoModel实体类表示待办事项实体，包含todo标题、todo内容、todo截止时间和开始时间、todo的参与小组。
控制类：CreatTodo。CreatTodo控制类负责处理关于创建待办事项的相关操作，包括选择小组、输入todo的title、title长度检测及反馈、输入todo内容、todo内容长度检测及反馈、保存todo、看板上显示新建todo。
边界类：NewTodo。NewTodo为创建待办事项页面。
用例析取图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_8e9e943927a0159167f56f954ef87a7e.png)


#### f. 小组成员管理用例类的析取：
实体类：GroupModel。GroupModel实体类表示小组实体，包含小组成员、管理员、小组名称。
控制类：GroupManage。GroupManage控制类负责处理关于小组成员管理的相关操作，包括增加成员、删除成员、删除小组、创建小组。
边界类：Group。Group为小组成员管理页面。
用例析取图
![](https://codimd.s3.shivering-isles.com/demo/uploads/upload_40d74bbe56bf02cb6580bb97e23ddf93.png)

### 3. 分析机制

对于重要信息的要求比较一致，其他类没有特殊考虑

|分析类|分析机制|
|---|----|
|User|持久性、安全性|
|PersonalInfo|持久性、安全性|
|TodoModel|持久性、安全性|
|GroupModel|持久性、安全性|


### 4. 合并分析类

## 五、 子系统及其接口设计

系统简单则可能不需要，因为全部代码都是基于现有web前端、后端框架、web服务器软件、DBMS实现的。数据安全、持久性等等亦没有做特殊设计。同时考虑功能拓展，所有功能都有一个页面上的多个可切换标签页分别装载，前端拓展方式没有太大差异，而得益于MVC的结构，其他部分也容易在该架构下扩展。



## 六、部件设计

### 1. 分析并发需求
A：多个浏览器客户端的同时访问
B: 大量对数据库的并发访问

### 2. 解决方案
A、B: 利用现有DMBS、web服务器软件完成负载均衡

### 3. （进程）生命周期
web服务器、数据库服务器、客户端会话等等，待补充

### 4. 映射到现实系统
在编程中使用第三方框架，不考虑自己设计进程模型到现实的映射

