---
title: 17.x - 小结与测试 - 继承
alias: 17.x - 小结与测试 - 继承
origin: /chapter-17-comprehensive-quiz/
origin_title: "17.x — Chapter 17 comprehensive quiz"
time: 2022-8-12
type: translation
tags:
- summary
---

## 复习

通过继承程序员可以在两个对象之间实现”is-a“（是一个）的关系。被继承的对象称为父类或者基类，或者超类。而继承得到的对象则称为子类、派生类。

当一个类从另一个类派生出来时，它会获得基类的全部成员。

当派生类被构造是，其属于基类的部分会首先被构建，然后派生类部分才会构建。更多具体信息如下：

1.  派生类的内存是另外分配的（足够存放基类部分的数据和派生类部分的数据）；
3.  调用派生类合适的构造函数；
4.  首先会使用合适的基类构造函数构造基类对象。如果基类对象没有被显式指定，则调用的是默认的构造函数；
5.  派生类使用初始化列表来初始化其成员变量；
6.  执行派生类构造函数的函数体；
7.  控制权交还给主调函数。

析构的顺序则正号相反，先析构派生类再析构基类。

C++ 支持3个访问控制说明符：public，private 和 protected。protected 关键字修饰的成员，允许该类、友类和派生类访问，但是不能被其他类访问。

Class也可以通过公开、私有或保护的方式继承。绝大多数情况下，类的继承都是公开的。

下表列举了不同访问说明符和继承类型的组合：


|基类中的访问说明符	|公开继承时的访问说明符|私有继承时的访问说明符|保护继承时的访问说明符|
|:----:|----:|----:|----:|
|公开|	公开	|私有	|保护|
|私有|	不可访问|	不可访问|	不可访问|
|保护|	保护|	私有|	保护|

派生类中可以添加新的函数，修改基类的函数，修改继承的成员的访问规则或者隐藏某些函数。

当派生类从多个父类进行基础时，称为[[多重继承]]。一般来说应该避免多重继承，除非它能够极大地降低设计复杂度。