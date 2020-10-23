In mathematics, the nth harmonic number is the sum of the reciprocals of the first n natural numbers:
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly92ai56MTgwLmNuL2RiZmYxY2NmM2I0MWYxMTlkODAyMzM1Y2QyMTJjOTRk?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly92ai56MTgwLmNuLzBjYjUzNGJkNWIyMDRmMzMyZTYxZTA5YWZjMDc1YWEz?x-oss-process=image/format,png)
In this problem, you are given n, you have to find Hn.
### Input
 starts with an integer T (≤ 10000), denoting the number of test cases.

Each case starts with a line containing an integer n (1 ≤ n ≤ 108).

### Output
For each case, print the case number and the nth harmonic number. Errors less than 10-8 will be ignored.

### Sample Input

```c
12
1
2
3
4
5
6
7
8
9
90000000
99999999
100000000
```

### Sample Output

```c
Case 1: 1
Case 2: 1.5
Case 3: 1.8333333333
Case 4: 2.0833333333
Case 5: 2.2833333333
Case 6: 2.450
Case 7: 2.5928571429
Case 8: 2.7178571429
Case 9: 2.8289682540
Case 10: 18.8925358988
Case 11: 18.9978964039
Case 12: 18.9978964139
```

### 分析：

对于这道题而言题意比较好理解核心问题就是输入一个n(n<=1e8),
而我们要做的就是求1/1+1/2+1/3+1/4+1/5+1/6+~~~~1/n的和，输出要求为保留十位小数。但是我们知道n可能很大这就会造成超时，所以我们可以采用一种打表的思想,但是我们不是存储每一个n对应的Fn因为这样会占用大量的内存并且耗费很多时间。
### 重点：
我们可以把打表做一个优化，假如我们每100个数打一次表，假如我输入的n为102，这样我们可以直接用打表求得的前100项的和+1/101+1/102就能得到我们需要的结果。
(假如100项打一次表，1e8/100=2000000,因此我们可以开一个容量稍微比2000000大一点的数组就能满足需求)
下面我们上代码：

```c
#include <iostream>
#include <cstdio>
using namespace std;
#define MAX 100000000

double ans[2000100];//分段存储结果
int main()
{
    int t,n,k;
    int casenum;
    casenum=0;
    double sum=0.0;
    k=0;
    ans[0]=0;
    for(int i=1;i<=MAX;i++)//打表：每100项存储一个结果
    {
        sum+=1.0/i;
        if(i%100==0)
        {
            ans[++k]=sum;//先加再用（ans[0]已经赋值为0）
        }
    }
    scanf("%d",&t);//多组输入
    while(t--)
    {
        scanf("%d",&n);
        int num=n/100;//比n小的前num*100项
        double s;
        s=ans[num];
        //求余项的和
        for(int i=100*num+1;i<=n;i++)
        {
            s+=1.0/i;
        }
        printf("Case %d: %.10lf\n",++casenum,s);//保留十位小数
    }
    return 0;
}

```
