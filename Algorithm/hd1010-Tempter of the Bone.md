####  思路
&emsp;&emsp;深搜加剪枝，注意部分在注释中。[题目点这](<http://acm.hdu.edu.cn/showproblem.php?pid=1010>)。
####  代码
``` cpp
#include<iostream>
#include<cstdio>
#include<algorithm>
using namespace std;

const int Max = 7 + 1;
char maze[Max][Max];
int offset_x[4] = {0, -1, 0, 1};//水平偏移 
int offset_y[4] = {-1, 0, 1, 0};//竖直偏移 
int door_x, door_y;
int start_x, start_y;
int n, m;
int time;
bool isOk;

void dfs(int x, int y, int cnt){
	//恰好走出 
	if(x == door_x && y == door_y && cnt == time){
		isOk = true;
		return;
	}
	//当前走到出口后还余下的时间 
	int remaining = time - cnt - abs(door_x - x) - abs(door_y - y);
	//剪枝(时间不够或余下时间为奇数（如果走到重点还有奇数时间，没法继续了）) 
	if(remaining < 0 || remaining & 1){
		isOk = false;
		return; 
	} 
	for(int i = 0; i < 4; i++){
		int cx = x + offset_x[i];
		int cy = y + offset_y[i];
		//检查边界 
		if(cx < 0|| cx > n-1 || cy < 0 || cy > m-1)
			continue;
			
		if(maze[cx][cy] != 'X'){
			maze[cx][cy] = 'X';
			dfs(cx, cy, cnt + 1);
			//深搜回来要还原 
			maze[cx][cy] = '.'; 
		}
		if(isOk)
			break; 
	}
}

int main(){
	freopen("data.txt", "r", stdin);
	int i, j;
	char ch;
	while(cin >> n >> m >> time && !(n==0 && m==0 && time==0)){
		isOk = false;
		for(i = 0; i < n; i++){
			for(j = 0; j < m; j++){
				cin >> ch;
				maze[i][j] = ch;
				if(ch == 'S'){
					start_x = i;
					start_y = j;
					maze[i][j] = 'X';
				}	
				if(ch == 'D'){
					door_x = i;
					door_y = j;
				}
			}
		}
		dfs(start_x, start_y, 0); 
		if(isOk)
			cout << "YES" << endl;
		else
			cout << "NO" << endl;
	}
	return 0;
}


```