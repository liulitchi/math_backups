以一道 IBM 网页上的[运筹学习题](https://www.ibm.com/developerworks/cn/linux/l-glpk1/index.html)为例。

原题：某公司生产销售两种木制玩具：士兵和火车。
玩具士兵单价 27 元，原材料耗费 10 元，同时每个玩具士兵耗费公司可变人力成本和间接成本 14 元。
玩具火车单价 21 元，原材料耗费 9 元，同时每辆玩具火车耗费可变人力成本和间接成本 10 元。
制造公司需要两类熟练工人：木工和修整工。
单个玩具士兵需要 2 小时的修整工劳动和 1 小时的木工劳。
单辆玩具火车需要 1 小时的修整工劳动和 1 小时的木工劳动。
公司每周只能提供 100 个修整工和 80 个木工的工时，而市场对于火车的需求是无限的，同时每周最多可以销售 40 个玩具士兵。
求公司每周生产的士兵和火车数量，以使收益（收入 - 成本）最大化。

## 数学表述

在这里，我们有单纯形法来表述。设公司每周生产士兵数量为 X_1 , 生产火车数量为 X_2,收益为 z 。则根据题意，有：

(27 - 10 - 14)*(x_1) + (21 - 9 - 10)*(x_2) =!= max

2*(x_1) + x_2 <= 100

x_1 + x_2 <= 80

x_1 <= 40

x_1 >= 0, x_2 >=0

## GLPK 软件解决：

Debian 安装 GLPK ： `sudo apt install glpk-utils`

OpenBSD 安装 GLPK ： `doas pkg_add glpk-utils`

vim toy.mod

```
  /* Decision variables */
   var x1 >= 0;  # soldier 
   var x2 >= 0;  # train 

  /* Objective function */
  maximize z: 3*x1 + 2*x2;

  /* Constraints */
  s.t. Finishing : 2*x1 + x2 <= 100;
  s.t. Carpentry : x1 + x2 <= 80;
  s.t. Demand    : x1 <= 40;

  end;
```
保存文件后，运行 `glpsol -m toy.mod -o toy.sol`, 然后运行 `vim toy.sol`查看结果。

```toy.sol
Problem:    toy
Rows:       4
Columns:    2
Non-zeros:  7
Status:     OPTIMAL
Objective:  z = 180 (MAXimum)

   No.   Row name   St   Activity     Lower bound   Upper bound    Marginal
------ ------------ -- ------------- ------------- ------------- -------------
     1 z            B            180
     2 Finishing    NU           100                         100             1
     3 Carpentry    NU            80                          80             1
     4 Demand       B             20                          40

   No. Column name  St   Activity     Lower bound   Upper bound    Marginal
------ ------------ -- ------------- ------------- ------------- -------------
     1 x1           B             20             0
     2 x2           B             60             0
```

根据软件运行结果可知，最大收益为 180 元。其中每周生产玩具士兵 20 名，玩具火车 60 辆。
