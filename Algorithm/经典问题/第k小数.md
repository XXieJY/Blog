###  第k小数
 &emsp;&emsp;用快速排序思想来做。代码如下：   
``` cpp
#include<iostream>
#include<cstdio>
using namespace std;

int getK(int* num, int left, int right, int k){
	if(left >= right)
		return num[left];
	int i = left;
	int j = right;
	int base = num[left];
	
	while(i < j){
		while(i < j && num[j] >= base)j--;
		if(i < j)
			num[i++] = num[j];
		while(i < j && num[i] < base)i++;
		if(i < j)
			num[j--] = num[i];
	} 
	num[i] = base;
	int n = i - left + 1;
	if(n == k)
		return num[i];
	else if(n < k)
		return getK(num, i+1, right, k-n);
	else
		return getK(num, left, i-1, k);
} 

int main(){
	freopen("data.txt", "r", stdin);
	int n, k;
	while(cin >> n && n != 0){
		cin >> k;
		int num[n];
		for(int i = 0; i < n; i++)
			cin >> num[i];
		cout << getK(num, 0, n-1, k) << endl;
	}
	return 0;
}

```