
## [A. Filling Diamonds](https://codeforces.com/contest/1339/problem/A)

![ ](https://img-blog.csdnimg.cn/20200413171212947.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1ODQ1NDA0,size_16,color_FFFFFF,t_70#pic_center)

AC代码：

```cpp
/*思维*/
#include<iostream>
using namespace std;
int main()
{
   long long int t;
    cin>>t;
    while(t--)
    {
       long long int n;
       cin>>n;
        cout<<n<<endl;
    }
    return 0;
}
```

## [B. Sorted Adjacent Differences](https://codeforces.com/contest/1339/problem/B)

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041317244110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1ODQ1NDA0,size_16,color_FFFFFF,t_70#pic_center)
AC代码：

```cpp
/*先排序再中间往两边遍历*/
#include<iostream>
#include<algorithm>
using namespace std;
int a[100010];
int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int n;
        cin>>n;
        for(int i=0; i<n; i++)
        {
            cin>>a[i];
        }
        sort(a,a+n);
        if(n%2==0)//偶数
        {

            for(int i=n/2-1; i>=0; i--)
            {
                cout<<a[i]<<" "<<a[n-i-1]<<" ";
            }
            cout<<endl;
        }
        else//奇数
        {
            cout<<a[n/2]<<" ";
            for(int i=n/2-1; i>=0; i--)
            {
                cout<<a[i]<<" "<<a[n-i-1]<<" ";
            }
            cout<<endl;
        }
    }
    return 0;
}
```

## [C. Powered Addition](https://codeforces.com/contest/1339/problem/C)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200413173348848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1ODQ1NDA0,size_16,color_FFFFFF,t_70#pic_center)
AC代码：
```cpp
/*二进制最高位*/
#include<iostream>
#include<string.h>
using namespace std;
int a[100009];
int maxx=1e9+9;
int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        memset(a,0,sizeof(a));
        int maxn=-maxx;
        int maxt=0;
        int n;
        cin>>n;
        for(int i=1;i<=n;i++)
        {
            cin>>a[i];
            maxn=max(maxn,a[i]);
            maxt=max(maxt,maxn-a[i]);
        }
    int cnt=0;
    while(maxt)
    {
        maxt>>=1;
        cnt++;
    }
        cout<<cnt<<endl;
    }
    return 0;
}
```
