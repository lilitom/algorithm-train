#案例1 烽火传递
>Description 
　　烽火台又称烽燧，是重要的军事防御设施，一般建在险要或交通要道上。一旦有敌情发生，白天燃烧柴草，通过浓烟表达信息；夜晚燃烧干柴，以火光传递军情，在某两座城市之间有n个烽火台，每个烽火台发出信号都有一定代价。为了使情报准确地传递，在连续m个烽火台中至少要有一个发出信号。请计算总共最少花费多少代价，才能使敌军来袭之时，情报能在这两座城市之间准确传递。 
Input 
　　第一行：两个整数N，M。其中N表示烽火台的个数，M表示在连续m个烽火台中至少要有一个发出信号。接下来N行，每行一个数Wi，表示第i个烽火台发出信号所需代价。 
Output 
　　一行，表示答案。 
Sample Input 
5 3 
1 
2 
5 
6 
2
Sample Output 
4
Data Constraint 
对于50%的数据，M≤N≤1,000 。 对于100%的数据，M≤N≤ 100,000，Wi≤100。

博客 https://blog.csdn.net/A1847225889/article/details/77777009
先用简单的动态规划来试试吧，动态转移方程为
$
\begin{array}{l}
dp[i] = \min (dp[j]) + w[i]\;\;\;\;\;(\max (i - m,0) \le j < i)\\
\;\;\;\;\;\;\;\;\;  = \min (dp[i - 1],dp[i - 2], \cdots ,dp[i - m])+ w[i]\\
\;\;\;\;\;\;\;
\tag{1}
\end{array}
$
$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$
\\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\)

```
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
int n,m;
int w[100001];
int f[100001];
int main()
{
    scanf("%d%d",&n,&m);
    int i,j;
    for (i=1;i<=n;++i)
        scanf("%d",&w[i]);
    memset(f,127,sizeof f);
    f[0]=0;
    	for (int i = 1; i <= n; i++)
	{
		for (j = max(0, i - m); j<i; ++j)//这里把博客中的合并了
			f[i] = min(f[i], f[j]);
		f[i] += w[i];
	}


	int ans = 0x7f7f7f7f;
	for (i = n - m + 1; i <= n; ++i)
		ans = min(ans, f[i]);
	printf("%d\n", ans);
}
```

来看看我们的单调队列是怎么做的吧？

```
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
int n, m;
int w[10];
int que[10], head = 0, tail = 0;
int f[10];
int main()
{
	scanf("%d%d", &n, &m);
	int i, j;
	for (i = 1; i <= n; ++i)
		scanf("%d", &w[i]);
	memset(f, 127, sizeof f);
	f[0] = 0;
	que[0] = 0;
	for (i = 1; i <= n; ++i)
	{
		if (que[head]<i - m)
			++head;//将超出范围的队头删掉
		f[i] = f[que[head]] + w[i];//转移（用队头）
		while (head <= tail && w[que[tail]]>w[i])
			--tail;//将不比它优的全部删掉
		que[++tail] = i;//将它加进队尾
	}
	int ans = 0x7f7f7f7f;
	for (i = n - m + 1; i <= n; ++i)
		ans = min(ans, f[i]);
	printf("%d\n", ans);
}
```
对比一下就可以发现这个代码是怎么一步一步写到这里的。


个人比较喜欢Python的代码，简洁表达如下：

```python
# -*- coding: utf-8 -*-
##code2
##用来求滑动窗口最小值问题
a = [0, 4, 2, 5, 6, 1, 7]
n = len(a) - 1
m = 3 #窗口大小
head = 1
tail = 0 #这里初始化为0是有必要的
dp = [0] * 10
queue = [0] * 10
ansl = [0] * 10
for i in range(1, n + 1) :
while (head <= tail and queue[head] <= i - m) :
head = head + 1 #head的递增是有条件的，即不能让下标的距离太大，m = 3, 超过肯定不行，前初始化tail = 0也是有道理的
dp[i] = dp[queue[head]] + a[i]
while (head <= tail and a[i]<a[queue[tail]]) : #发现比队尾还小的情况，那就果断出队
	tail = tail - 1
	tail = tail + 1
	queue[tail] = i
	ansl[i] = a[queue[head]]

	for ii in range(m, n + 1) :
		print ansl[ii]
		print min(dp[n - m + 1:n]) #输出总体最小值


## code2方法一
## 用来求烽火传递问题
		a = [0, 4, 2, 5, 6, 1, 7]
		n = len(a) - 1
		m = 3 #窗口大小
		head = 0
		tail = 0 #这里初始化为0是有必要的
		dp = [0] * 10
		queue = [0] * 10
		ansl = [0] * 10
		for i in range(1, n + 1) :
			while (head <= tail and queue[head]< i - m) :
				head = head + 1 #head的递增是有条件的，即不能让下标的距离太大，m = 3, 超过肯定不行，前初始化tail = 0也是有道理的
				dp[i] = dp[queue[head]] + a[i]
				while (head <= tail and dp[i]<dp[queue[tail]]) : #发现比队尾还小的情况，那就果断出队
					tail = tail - 1
					tail = tail + 1
					queue[tail] = i
					ansl[i] = a[queue[head]]
					# dp[i] = dp[queue[head]] + a[i]
					print(a[queue[head]])

					for ii in range(m, n + 1) :
						print(ansl[ii])
						print(min(dp[n - m + 1:n])) #输出总体最小值

## code2方法二
						import queue
						a = [1, 2, 5, 6, 3, 7]
						queuearray = []
						dp = [0] * 10
						for i in range(len(a)) :
							queuearray.append(a[i])
							while a[i] < queuearray[max(len(queuearray) - 2, 0)] :
								queuearray.remove(queuearray[len(queuearray) - 2])
								if i>2 :
									dp[i] = temp + a[i]
									if  len(queuearray) > 3:
queuearray.remove(queuearray[0])
temp = queuearray[0]
print(queuearray)
print(dp)
#这里我用的是一个list来做的，比方法一中的que以及索引要简单且好理解，中间也打印出了queuearray方便观察整个过程
```