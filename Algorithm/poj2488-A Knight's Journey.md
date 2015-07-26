####  思路
&emsp;&emsp;题意就是马走日，能不能不重复地走完所有格子。深搜。但是由于要按照字典序，所以要从A1出发搜索，并且方向偏移数组的顺序是有要求的，我按照X轴表示数字，Y轴表示字母来写代码。[题目点这里](<http://poj.org/problem?id=2488>)。
####  代码
``` cpp
#include<iostream>
#include<cstdio>
#include<cstring>
using namespace std;

const int Max = 26 + 1;
int chessboard[Max][Max];
char path[2*Max*Max];
int offset_x[8] = {-1,1,-2,2,-2,2,-1,1};//顺序有要求的
int offset_y[8] = {-2,-2,-1,-1,1,1,2,2};
bool isOk;
int p, q;

void dfs(int x, int y, int step){
	path[2*step] = y + 'A';
	path[2*step+1] = x + '1';
	if(step == p * q - 1){
		isOk = true;
		return; 
	}
	for(int i = 0; i < 8; i++){
		int cx = x + offset_x[i];
		int cy = y + offset_y[i];
		
		if(cx < 0 || cx > p-1 || cy < 0 || cy > q-1)
			continue;
		
		if(!chessboard[cx][cy]){
			chessboard[cx][cy] = 1;
			dfs(cx, cy, step+1);
			chessboard[cx][cy] = 0;
		}
		if(isOk)
			break;
	}
}

int main(){
	freopen("data.txt", "r", stdin);
	int t, i = 1;
	cin >> t;
	while(t--){
		cin >> p >> q;
		isOk = false;
		memset(chessboard, 0, sizeof(chessboard));
		chessboard[0][0] = 1;//起点 
		dfs(0, 0, 0);
		cout << "Scenario #" << i++ << ":" << endl;
		if(isOk){
			path[2*p*q] = 0; //截断之后的多余数据 
			cout << path << endl;
		}
		else{
			cout << "impossible" << endl;
		}
		cout << endl;
	}
	return 0;
}



```