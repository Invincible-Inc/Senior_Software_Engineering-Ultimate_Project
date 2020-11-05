# 项目管理软件-Ultimate Project 架构设计

> 架构设计又称概要设计，主要描述系统设计时所使用的基本架构，并对架构做简单介绍。

- [项目管理软件-Ultimate Project 架构设计](#项目管理软件-ultimate-project-架构设计)
  - [1. 架构描述](#1-架构描述)
  - [2. 架构图](#2-架构图)
  - [3. 关键抽象](#3-关键抽象)



## 1. 架构描述

本系统采用MVC（Model View Controller）三层架构。该架构的使用实现了应用程序的分层管理，简化了后续对程序的修改和扩展，并且使程序某一部分的重复利用成为可能。
- 模型（Model）：负责存储系统的中心数据。
- 视图（View）：将信息显示给用户（可以定义多个视图）。
- 控制器（Controller）：处理用户输入的信息。负责从视图读取数据，控制用户输入，并向模型发送数据，是应用程序中处理用户交互的部分。负责管理与用户交互交互控制。

其中视图和控制器共同构成了用户接口。且每个视图都有一个相关的控制器组件。控制器接受输入，通常作为将鼠标移动、鼠标按钮的活动或键盘输入编码的时间。时间被翻译成模型或试图的服务器请求。用户仅仅通过控制器与系统交互。


## 2. 架构图

![架构图](https://github.com/Invincible-Inc/Senior_Software_Engineering-Ultimate_Project/blob/main/docs/architecture_images/MVC.PNG)


## 3. 关键抽象

关键抽象即为找到系统实体类的过程。
实体类为系统中存储和改动的数据，可以从需求分析中的术语表中得到。经过分析，本系统有两个个实体类，分别为用户表和事件表，用户表存储了与用户相关的一切信息，包含用户名、密码、用户权限等，事件表包含了事件名称、事件ddl、事件具体任务等信息。
![关键抽象图](https://github.com/Invincible-Inc/Senior_Software_Engineering-Ultimate_Project/blob/main/docs/architecture_images/ab.PNG)
