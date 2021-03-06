---
layout:     post
title:      "Python技术小结一"
subtitle:   "python小知识 "
date:       2018-08-20 19:45:00
author:     "Makes.Z"
header-img: "img/post-think-try-write.jpg"
tags:
    - Python
---

## python小知识。

1.在一个对象中，当我们对它其中的一个属性进行赋值时，这个被重新赋值的属性
会遮住类级别的变量，若该变量为类的公共变量，所有对象都可访问，其他对象访
问该变量时访问的是类级别的变量，而赋值后访问的是对象级别的变量。具体可参
考下列代码：
      ```
        init（）：
            member += 1
      ```

        ```
        $ m1.init()
        >member = 1
        $m2.init()
        >member = 2
        $m1.member = "two"
        >member = "two"
        $m2.member
        >2
        ```

2.Pythong的"归一化"原理，即为接口，接口继承实质上是要求“做出一个良好的抽象”，
外部调用者无需关心内部实现。这里实际上用到一个设计模式，名为“依赖倒置”：高层
不依赖底层，二者相互依赖抽象。


3.Python多个超类的方法解析顺序
如下图的继承关系所示：

![image](https://img-blog.csdn.net/20180821090834383?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzODcxMTQ3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

    在Python有至少3种不同的MRO解析方法
    1.经典方法：采用了一种很简单的 MRO 方法：从左至右的深度优先遍历其查找顺序为
[D, B, A, C, A]，出现重复的时候保留第一个。
    存在的问题，当我们想使用X.show()时，没有使用C.show(),而是A.show()
    2.Python 2.2 的新式类 MRO:在经典方法的基础上修改，当再次出现同样的时候，保
留最后一个，最后结果为 [D, B, C, A]。
    3.Python 2.3以后采用C3的方法：判断MRO要先确定一个线性序列，然后查找路径由由序
列中类的顺序决定。所以C3算法就是生成一个线性序列。如果继承至一个基类:  class B(A)。
这时B的MRO序列为[B,A]。
    merge操作就是C3算法的核心。遍历执行merge操作的序列，如果一个序列的第一个元素，
是其他序列中的第一素，或不在其他序列出现，则从所有执行merge操作序列中删除这个元素，
合并到当前的MRO中。merge操作后的序列，继续执行merge操作，直到merge操作的序列为空。
如果merge操作的序列无法为空，则说明不合法。
---
    总的来说，这和超类排列顺序有关，位于前面的类的方法将会覆盖位于后面的类的方法。
---
