#题目描述
>kkk做了一个人体感觉分析器。每一天，人都有一个感受值Ai，Ai越大，表示人感觉越舒适。在一段时间[i, j]内，人的舒适程度定义为[i, j]中最不舒服的那一天的感受值 * [i, j]中每一天感受值的和。现在给出kkk在连续N天中的感受值，请问，在哪一段时间，kkk感觉最舒适？

#输出输出格式
输入格式：

第一行为N，代表数据记录的天数

第二行N个整数，代表每一天的感受值

输出格式：

一行，表示在最舒适的一段时间中的感受值。

#输入输出样例
>输入：6
3 1 6 4 5 2

>输出：
60

#说明

样例解释：

kkk最开心的一段时间是第3天到第5天，开心值：(6+4+5)*4=60

对于30%的数据，1<=N<=100

对于70%的数据，1<=N<=2000

对于100%的数据，1<=N<=100000，1<=感受值<=1000000

#代码
````c++
#include<cstdio>
#include<iostream>
#include<algorithm>
#define N 10

int n;
int val[N];
int qzh[N];
int l[N], r[N];
int stk[N], top;

signed main(){
	scanf("%lld", &n);
	for (int i = 1; i <= n; i++) scanf("%lld", &val[i]), qzh[i] = qzh[i - 1] + val[i];
	for (int i = 1; i <= n; i++){
		while (top&&val[i]<val[stk[top]]) 
			l[stk[top]] = i, 
			top--;
		stk[++top] = i;
	}
	while (top) l[stk[top--]] = n + 1;
	for (int i = n; i; i--){
		while (top&&val[i]<val[stk[top]]) r[stk[top]] = i, top--;
		stk[++top] = i;
	}
	while (top) r[stk[top--]] = 0;
	int ans = -1234567890;
	for (int i = 1; i <= n; i++)
		ans = std::max(ans, (qzh[l[i] - 1] - qzh[r[i]])*val[i]);
	printf("%lld\n", ans);
	return 0;
}
````