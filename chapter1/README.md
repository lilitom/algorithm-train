# 动态规划问题
动态规划是算法题中经常要考的内容，复杂度较大，若没有一般的长期的积累的话，通过正常的思路去解一些题
的时候是很难解出来的。

#定义
1）动态规划是运筹学中用于求解决策过程中的最优化数学方法。 当然，我们在这里关注的是作为一种算法设计技术，作为一种使用多阶段决策过程最优的通用方法。

它是应用数学中用于解决某类最优化问题的重要工具。


2）如果问题是由交叠的子问题所构成，我们就可以用动态规划技术来解决它，一般来说，这样的子问题出现在对给定问题求解的递推关系中，这个递推关系包含了相

同问题的更小子问题的解。动态规划法建议，与其对交叠子问题一次又一次的求解，不如把每个较小子问题只求解一次并把结果记录在表中（动态规划也是空间换时间

的），这样就可以从表中得到原始问题的解。


关键词：

它往往是解决最优化问题滴

问题可以表现为多阶段决策（去网上查查什么是多阶段决策！）

交叠子问题：什么是交叠子问题，最有子结构性质。

动态规划的思想是什么：记忆，空间换时间，不重复求解，由交叠子问题从较小问题解逐步决策，构造较大问题的解。

#分类

动态规划一般可分为线性动规，区域动规，树形动规，背包动规四类。

举例：

线性动规：拦截导弹，合唱队形，挖地雷，建学校，剑客决斗等；

区域动规：石子合并， 加分二叉树，统计单词个数，炮兵布阵等；

树形动规：贪吃的九头龙，二分查找树，聚会的欢乐，数字三角形等；

背包问题：01背包问题，完全背包问题，分组背包问题，二维背包，装箱问题，挤牛奶等。