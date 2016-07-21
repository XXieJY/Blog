
####  思路
&emsp;&emsp;贪心。如果将走廊看作一条线段，每次移动也看做一条线段，第一次我们先同时移动所有互不干扰的线段，再去移动剩下的互不干扰的所有线段，以此类推。如果移动一个线段，就在原线段（走廊）上的对应部分做个计数，由于每次移动都是移动所有互不相关的线段，所以，移动的次数就是这些计数当中的最大值。[题目点这](<http://acm.hdu.edu.cn/showproblem.php?pid=1050>)。

####  代码
``` cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
using namespace std;

const int Max = 200 + 10;
int num[Max]; 
 
int main(){
	//freopen("data.txt", "r", stdin);
	int t, n, from, to, temp1, temp2, i, j, k;
	cin >> t;
	while(t--){
		memset(num, 0, sizeof(num));
		cin >> n;
		for(i = 0; i < n; i++){
			cin >> temp1 >> temp2;
			from = (min(temp1, temp2) - 1) / 2;
			to = (max(temp1, temp2) - 1) / 2;
			for(j = from; j <= to; j++)
				num[j]++;
		}
		sort(num, num + Max);
		cout << num[Max-1] * 10 << endl;
	}
	return 0;
}
```