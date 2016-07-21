####  思路
&emsp;&emsp;题意就是找最大子序列和。首先想到动态规划，对于给定的数组，将子序列按照序列末尾数字分组，比如有数组`a,b,c`，其子序列可以分为：以`a`为尾数的子序列、以`b`为尾数的子序列、以`c`为尾数的子序列,以此类推。再假设，以`i`为尾数的子序列中和最大值为`Mi`，那么，`Ma、Mb、Mc`存在一定的关系，`Mb=MAX(b,b+Ma)`。进一步解释就是，以`b`为尾数的子序列也可以分为两类：只有`b`（单个数的子序列）、`b`和以`b`之前的数（也就是`a`）为尾数的子序列组成的子序列，那么其和的最大值，也就是这两类的最大值，而第二类的最大值就是`b+Ma`，这样就产生了状态转移方程：`dp[i]=MAX(num[i],num[i]+dp[i-1])`,其中`dp[i]`表示以第`i`个数为尾数的子序列中和的最大值，`num[i]`表示第`i`个数。然后再寻找`dp`数组中的最大值，就是要求的值，其下标就是尾数的下标，而起始数字，需要对`dp`向前遍历，第一个小于`0`的数（意味着，这个子序列和小于`0`，那肯定就舍弃这一段，从下一段开始）的下标+`1`，就是要求子序列的首个数字。 [题目点这](http://acm.hdu.edu.cn/showproblem.php?pid= 1003) 。
####  代码
``` cpp
#include<iostream>
#include<cstdio> 
using namespace std;

const int MAX = 100000 + 1;
int num[MAX]; //用来存放输入的数字 
int dp[MAX];  //动态规划 
 
int getMax(int a, int b){
	if(a > b)
		return a;
	return b;
}
 
int main(){
	
	//freopen("in.txt", "r", stdin);
	int t, n, j;
	cin >> t;
	for(j = 1; j <= t; j++){
		cin >> n;
		for(int i = 1; i <= n; i++){
			cin >> num[i];
		}
		//动态规划 
		dp[0] = 0;
		for(int i = 1; i <= n; i++){
			dp[i] = getMax(num[i], num[i] + dp[i-1]);
		}
		//找最大和区间下标 
		int ans = dp[1];
		int start = 1;
		int end = 1;
		for(int i = 1; i <= n; i++){
			if(ans < dp[i]){
				ans = dp[i]; 
				end = i;
			}
		} 
		
		for(int i = end-1; i > 0; i--){
			if(dp[i] < 0){
				start = i + 1;
				break;
			}
		}
		cout << "Case " << j << ":" << endl;
		cout << ans << " " << start << " " << end <<endl;;
		if(j < t)
			cout << endl;		
	} 
	return 0;
}
	

```