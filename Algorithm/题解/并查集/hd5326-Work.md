#### 思路
&emsp;&emsp;类似并查集。得到一组关系后，将关系一层层向上更新，用一个向量来保存员工所manage的其他员工。
#### 代码
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<vector>

using namespace std;

struct node{
	int leader;//直接领导编号
	vector<int> stuffs;//被领导员工集合
};

node stuff[101];//stuff[i] 表示员工i的情况

void rel(int a, int b){
	stuff[b].leader = a;
	stuff[a].stuffs.push_back(b);
	int temp = a;
	//将b加入a的领导的员工集合
	while(stuff[temp].leader != 0){
		stuff[stuff[temp].leader].stuffs.push_back(b);
		temp = stuff[temp].leader;
	}
}

int main(){
	freopen("data.txt", "r", stdin);
	int n, k;
	while(cin >> n >> k){
		int a, b, res = 0;
		for(int i = 1; i < n; i++){
			cin >> a >> b;
			rel(a, b);
		}
		
		for(int i = 1; i <= n; i++){
			if(stuff[i].stuffs.size() == k)
				res++;
			stuff[i].leader = 0;
			stuff[i].stuffs.clear();
		}
		cout << res << endl;
	}
	return 0;
}

```