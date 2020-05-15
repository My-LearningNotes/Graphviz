DOT用法
=======

原文地址: https://itopic.org/graphviz.html

基本用法
--------

DOT中使用图(``digraph``/``graph``/``subgraph``), 节点(``node``)和边(``edge``)来描述关系图/流程图, 再配合一些属性的设置完成绘图.

Example:

.. code-block:: text

    #@startdot

    digraph demo {
    	label="示例"
    	bgcolor="beige"

    	node[color="grey"]

    	father[label="爸爸", shape="box"]
    	mother[label="妈妈", shape="box"]
    	brother[label="哥哥", shape="circle"]
    	sister[label="姐姐", shape="circle"]
    	node[color="#FF6347"]
    	strangers[label="路人"]

    	edge[color="#FF6347"]

    	father->mother[label="夫妻", dir="both"]
    	father->brother[label="父子"]
    	father->sister[label="父子"]
    	father->我[label="父子"]

    	mother->{brother,sister,我}[label="母子"]

    	{rank=same; father, mother}
    	{rank=same; brother,sister,我}
	}

    #@enddot

* ``graph``\ 用来定义无向图, 关系使用\ ``--``\ 来描述, 
  ``digraph``\ 用来描述有向图, 关系使用\ ``->``\ 来描述;
* ``demo``\ 为定义的图的名称, ``label``\ 和\ ``bgcolor``\ 为定义的图的属性;
* ``father``, ``mother``, ``brother``, ``sister``, ``我``, ``strangers``\ 为节点.
* 描述节点与节点的关系理解为\ ``边``\ .
  ``边``\ 有有向(``->``)和无向(``--``)两种.
* 上面有两个特殊的节点, ``node``\ 和\ ``edge``;
  ``node``\ 用来定义节点的默认属性; ``edge``\ 用来定义边的默认属性.
  作用域从本次定义到下一次定义为止.
  特定节点/边设置的属性会覆盖默认值.
* ``[]``\ 内定义属性, 属性可以针对图, 节点, 边来设置.
* ``father``\ 与子女的关系为一条条写的, ``mother``\ 的关系则为直接通过大括号的方式来对应三个节点.
* ``rank``\ 定义设置节点处在同一行, 辅助渲染出来的图的效果.
* 注释和C语言类似, ``/``\ 和\ ``#``\ 为单行注释, ``/* */``\ 为多行注释.
* DOT的写法不算严格, 比如结束可以有分号, 属性可以没有引号.


生成的效果图:

.. graphviz::

    digraph demo {
    	label="示例"
    	bgcolor="beige"

    	node[color="grey"]

    	father[label="爸爸", shape="box"]
    	mother[label="妈妈", shape="box"]
    	brother[label="哥哥", shape="circle"]
    	sister[label="姐姐", shape="circle"]
    	node[color="#FF6347"]
    	strangers[label="路人"]

    	edge[color="#FF6347"]

    	father->mother[label="夫妻", dir="both"]
    	father->brother[label="父子"]
    	father->sister[label="父子"]
    	father->我[label="父子"]

    	mother->{brother,sister,我}[label="母子"]

    	{rank=same; father, mother}
    	{rank=same; brother,sister,我}
	}


常用属性
--------

常用图属性
^^^^^^^^^^

+---------------+-------------+-------------------------------------------------------------+
| 属性名        | 默认值      | 说明                                                        |
+---------------+-------------+-------------------------------------------------------------+
| ``lablel``    |             | 图的标签                                                    |
+---------------+-------------+-------------------------------------------------------------+
| ``bgcolor``   |             | 背景颜色                                                    |
+---------------+-------------+-------------------------------------------------------------+
| ``fontcolor`` | black       | 字体颜色                                                    |
+---------------+-------------+-------------------------------------------------------------+
| ``fontname``  | Times-Roman | 字体                                                        |
+---------------+-------------+-------------------------------------------------------------+
| ``fontsize``  | 14          | 字体大小                                                    |
+---------------+-------------+-------------------------------------------------------------+
| ``rank``      |             | 子图等级限制, same, min, max, source, sink                  |
+---------------+-------------+-------------------------------------------------------------+
| ``rankdir``   | TB          | 排序方向, LR(Left to right) or TB(top to bottom)            |
+---------------+-------------+-------------------------------------------------------------+
| ``compound``  | false       | If true, allow edges between clusters. 配合lhead和ltail使用 |
+---------------+-------------+-------------------------------------------------------------+

常用节点属性
^^^^^^^^^^^^

+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| 属性名        | 默认值                                     | 说明                                                                         |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``label``     | node name                                  | 节点形式内容                                                                 |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``color``     | black                                      | node边框颜色                                                                 |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``fontcolor`` | black                                      | 字体颜色                                                                     |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``fillcolor`` |                                            | 背景色                                                                       |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``fontname``  | Times-Roman                                | 字体                                                                         |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``fontsize``  | 14                                         | 字体大小                                                                     |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``shape``     | elipse                                     | 形状, box, ellipse, circle, diamond, plaintext, point, triangle, invtriangle |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``style``     | 图形样式, e.g bold, dashed, dotted, filled |                                                                              |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+
| ``image``     |                                            | 背景图片地址                                                                 |
+---------------+--------------------------------------------+------------------------------------------------------------------------------+

Shape示例:

.. code-block:: text

    digraph demo{
    bgcolor="florawhite"
    "box"[shape=box]
    "polygon"[shape=polygon, sides=7]
    "ellipse"[shape=circle]
    "circle"[shape=circle]
    "point"[shape=point]
    "triangle"[shape=triangle]
    "invtriangle"[shape=invtriangle]
    "plaintext"[shape=plaintext]
    "diamnd"[shape=diamond]
    }

.. graphviz::

    digraph demo{
        bgcolor="floralwhite"
        "box"[shape=box]
        "polygon"[shape=polygon, sides=7]
        "ellipse"[shape=ellipse]
        "circle"[shape=circle]
        "point"[shape=point]
        "triangle"[shape=triangle]
        "invtriangle"[shape=invtriangle]
        "plaintext"[shape=plaintext]
        "diamond"[shape=diamond]
    }


常用边属性
^^^^^^^^^^

+---------------+---------+-----------------------------------------------------------+
| 属性名        | 默认值  | 说明                                                      |
+---------------+---------+-----------------------------------------------------------+
| ``label``     |         | 描述关系                                                  |
+---------------+---------+-----------------------------------------------------------+
| ``color``     | black   | 箭头颜色                                                  |
+---------------+---------+-----------------------------------------------------------+
| ``fontcolor`` | black   | 关系文字颜色                                              |
+---------------+---------+-----------------------------------------------------------+
| ``dir``       | forward | 设置方向: forward, back, both, none                       |
+---------------+---------+-----------------------------------------------------------+
| ``arrowhead`` | normal  | 箭头头部形状, box, crow, diamond, dot, none, normal, vee. |
+---------------+---------+-----------------------------------------------------------+
| ``arrowtail`` |         | 箭头尾部形状                                              |
+---------------+---------+-----------------------------------------------------------+
| ``arrowsize`` | 1.0     | 箭头大小                                                  |
+---------------+---------+-----------------------------------------------------------+
| ``style``     |         | 图形样式, e.g bold, dashed, dotted, filled                |
+---------------+---------+-----------------------------------------------------------+
| ``lhead``     |         | 当compound为true时, lhead用于指定边指向的cluster          |
+---------------+---------+-----------------------------------------------------------+
| ``ltail``     |         | 与lhead类似                                               |
+---------------+---------+-----------------------------------------------------------+

arrowhead示例

.. code-block:: text

    digraph demo{
        bgcolor="floralwhite"
        randir=LR

        "box"->"crow"[arrowhead=box]
        "crow"->"curve"[arrowhead=crow]
        "curve"->"diamond"[arrowhead=curve]
        "diamond"->"dot"[arrowhead=diamond]
        "dot"->"inv"[arrowhead=dot]
        "inv"->"none"[arrowhead=inv]
        "none"->"normal"[arrowhead=none]
        "normal"->"tee"[arrowhead=normal]
        "tee"->"vee"[arrowhead=tee]
        "vee"->"box"[arrowhead=vee]
     }

.. graphviz::

    digraph demo{
        bgcolor="floralwhite"
        rankdir=LR

        "box"->"crow"[arrowhead=box]
        "crow"->"curve"[arrowhead=crow]
        "curve"->"diamond"[arrowhead=curve]
        "diamond"->"dot"[arrowhead=diamond]
        "dot"->"inv"[arrowhead=dot]
        "inv"->"none"[arrowhead=inv]
        "none"->"normal"[arrowhead=none]
        "normal"->"tee"[arrowhead=normal]
        "tee"->"vee"[arrowhead=tee]
        "vee"->"box"[arrowhead=vee]
    }


一些示例
--------

子图
^^^^

一个图可以包含多个子图, 以及子图也可以嵌套子图.

    * 子图使用关键字\ ``subgraph``\ 定义;
    * 子图的名字必须以\ ``cluster``\ 开头, 否则就直接当节点渲染了.

.. code-block:: text

    digraph demo{
        bgcolor="beige"

        subgraph cluster_husband{
            node[color="grey"]
            {"爸爸", "妈妈"} -> "我"
        }

        subgraph cluster_wife {
            {"岳父", "岳母"} -> "老婆"
        }

        "我" -> "老婆"[label="夫妻", dir="both"]
        {rank=same; "我", "老婆"}
    }

渲染效果如下:

.. graphviz::

    digraph demo{
        bgcolor="beige"

        subgraph cluster_husband{
            node[color="grey"]
            {"爸爸", "妈妈"} -> "我"
        }

        subgraph cluster_wife{
            {"岳父", "岳母"} -> "老婆"
        }

        "我" -> "老婆"[label="夫妻", dir="both"]
        {rank=same; "我", "老婆"}
    }

二叉树形式
^^^^^^^^^^

.. code-block:: text

    digraph demo{
        bgcolor="beige"
        node[shape="record", height=.1]
        node0[label="<f0> | <f1> G | <f2>"]
        node1[label="<f0> | <f1> E | <f2>"]
        node2[label="<f0> } <f1> B | <f2>"]
        node0:f0 -> node1:f1
        node0:f2 -> node2:f1
    }

用\ ``|``\ 隔开的串会在绘制出来的节点中展现为一条分隔符, 用\ ``<>``\ 括起来的串称为锚点.

效果如下:

.. graphviz::
 
    digraph demo{
        bgcolor="beige"
        node[shape="record", height=.1]
        node0[label="<f0> | <f1> G | <f2>"]
        node1[label="<f0> | <f1> E | <f2>"]
        node2[label="<f0> | <f1> B | <f2>"]
        node0:f0 -> node1:f1
        node0:f2 -> node2:f1
    }

记录形式的节点也可以是竖形排列的. 与横向排列的记录的不用只是label的形式不同, label中内容使用\ ``{}``\ 包围则是竖形排列的.

代码如下:

.. code-block:: text

    digraph demo{
        bgcolor="beige"
        node [shape="record"]
        a [label="{a | b | c}"]
    }

.. graphviz::

    digraph demo{
        bgcolor="beige"
        node [shape="record"]
        a [label="{a | b | c}"]
    }

直接指向子图
^^^^^^^^^^^^

边直接指向cluster, 需要设置compound为True, 并配合lhead或ltail来实现.

代码如下:

.. code-block:: text

    digraph demo{
        bgcolor="beige"
        compound=true
        subgraph cluster0{
            a
        }
        subgraph cluster1{
            b
        }

        a -> b [lhead=cluster1];
    }

.. graphviz::

    digraph demo{
        bgcolor="beige"
        compound=true
        subgraph cluster0{
            a
        }
        subgraph cluster1{
            b
        }

        a -> b [lhead=cluster1];
    }
