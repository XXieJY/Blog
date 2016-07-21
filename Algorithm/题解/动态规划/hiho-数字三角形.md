&emsp;&emsp;[题目点这](<http://hihocoder.com/problemset/problem/1037>)
&emsp;&emsp;**代码如下：**

``` cpp
#include<iostream>
#include<cstring>
#include<cstdio>
using namespace std;

const int Max = 100 + 10;
int arr[Max][Max];
int dp[Max][Max];

int getMax(int x, int y){
	return (x > y) ? x : y;
} 

int main(){
	int num, i, j, max = 0;
	memset(arr, 0, sizeof(arr));
	memset(dp, 0, sizeof(dp));
//	freopen("data.txt", "r", stdin);
	cin >> num;
	for(i = 1; i <= num; i++){
		for(j = 1; j <=i; j++){	
			cin >> arr[i][j];
			dp[i][j] = arr[i][j] + getMax(dp[i-1][j], dp[i-1][j-1]);
		}	
	}
	for(i = 1; i <=num; i++){
		if(dp[num][i] > max)
			max = dp[num][i];
	}
	
	cout << max << endl;
	return 0;
}

```