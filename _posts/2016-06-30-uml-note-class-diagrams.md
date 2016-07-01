---
layout: post
title: "UML Note: Class diagrams"
description: ""
date: 2016-06-30
time: 17:27:50
author: Lambert Bao
header_img: img/bg-1.jpg
category: 
tags: []

---

### UML类图示例

在UML中，类图包含类名、属性和操作，一个完整的类用带有分割线的长方形表示。如定义一个Employee类，如下：

![class_employee](/img/in_post/class_employee.jpg)

其对应的java片段如下：

    public class Employee {
	    private String name;
        private int age;
		private String email;
		
		public void modifyInfo() {
			...
		}
	}

其中：

- 第一部分对应的是类名。
- 第二部分是类的属性(Attributes)，其表示方法为：`可见性 名称:类型 [ = 缺省值 ]`。
- 第三部分是类的操作(Operations)，其表示方法为：`可见性 名称(参数列表) [ : 返回类型 ]`。

属性及操作的可见性可以用符号代替，对应关系如下：

- public: `+`
- protected: `#`
- private: `-`


### 类间关系

UML类图中常见的几种关系包括：

- 泛化(Generalization)
- 实现(Realization)
- 关联(Association)
- 聚合(Aggregation)
- 组合(Composition)
- 依赖(Dependency)

#### 泛化

泛化是一种继承关系，指定子类如何特化父类的所有特征和行为。
一般用带三角箭头的实线表示，箭头指向父类：

![generalization](/img/in_post/generalization.png)

#### 实现

实现是一种类与接口的关系，标示类是接口所有特征和行为的实现。
一般用带三角箭头的虚线表示，箭头指向接口：

![realization](/img/in_post/realization.png)

#### 关联

关联是一种拥有的关系，它使一个类知道另一个类的属性和方法。
一般用带普通箭头的实线标示，箭头指向被拥有者：

![association](/img/in_post/association.png)

*注：双向关联可以没有箭头，单向关联有一个箭头*

一个自身关联的例子如下：

![self_association](/img/in_post/self_association.png)

#### 聚合

聚合是关联关系的一种，表示整体与部分，是强关联关系。
聚合与关联在语法上无法区分，必须考察具体的逻辑关系。
一般用带空心菱形的实线表示，菱形指向整体：

![aggregation](/img/in_post/aggregation.png)

#### 组合

组合也是整体与部分的关系，是一种比聚合关系更强的关联关系，它要求代表整体的对象负责代表部分的对象的生命周期：

![composition](/img/in_post/composition.png)

#### 依赖

依赖是一种表示使用的关系，尽量不要使用双向的互相依赖。
一般用带普通箭头的虚线表示，箭头指向被使用者：

![dependency](/img/in_post/dependency.png)

上述各种关系之间的强弱顺序为：

    泛化=实现>组合>聚合>关联>依赖

一个各种关系交织的示例如下：

![class_diagram_allinone_example](/img/in_post/class_diagram_allinone_example.png)
