####  思路：
&emsp;&emsp;很简单的问题,[题目点这里](<http://acm.hdu.edu.cn/showproblem.php?pid=1020>)，我只想测试一下getchar和putchar。
####  代码：
``` cpp
#include<iostream>
#include<cstdio>
using namespace std;
int main(){
	freopen("data.txt", "r", stdin);
	int n, i, cnt;
	char ch, temp;
	cin >> n;
	getchar();
	while(n--){
		ch = getchar();
		temp = ch;
		cnt = 1;
		while(ch = getchar()){
			if(temp == ch)
				cnt++;
			else{
				if(cnt != 1)
					cout << cnt;
				putchar(temp);
				cnt = 1;
				temp = ch;
			}
			if(ch == '\n'){
				break;
			}
		}
		putchar('\n');
	}
	return 0;
} 

```
