### sort简介
&emsp;&emsp;C++ STL里面有个sort函数，顾名思义，是用来排序的。sort的头文件是`#include<algorithm> using namespace std;`，时间复杂度是`nlog2(n)`。sort()函数的参数有两种情况：
>* ```void sort(RanIt first, RanIt last);``` first为首地址，last为尾地址的下一个地址，排序方式是升序。
>* ```void sort(RanIt first, RanIt last, Pred pr);``` first与last同上，pr为自定义的比较函数，可以自定义排序方式。

### sort用法举例
