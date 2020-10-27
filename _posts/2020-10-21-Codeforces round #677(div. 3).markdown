---
layout: post
title: 
tag: Codeforces
---
[<font size=4>***A. Boring Apartments***</font>](https://codeforces.com/contest/1433/problem/A)



### 题目大意：
有 10000 套公寓，编号从 1 到 10000 。现在有一个人特别无聊，他会拨打编号上数字都相同的公寓住户号码，直到有人接听才停止，拨打顺序按递增规律，即：1 −> 11 −> 111 −> 1111 −>2−> 22 ->222 -> 2222-> 3 -> 33 ->----9999。
现给出接听了电话的住户编号，问这个无聊的人总共按了几次数字。

### 思路：
1.对个位数取余得到一个数a，那么从1 ~ (a-1)*1000+(a-1)*100+(a-1)*10+(a-1)的贡献为(a-1)*(1+2+3+4),剩余的项处理一下就行了。

### 代码：
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define IOS                     \
    ios::sync_with_stdio(false);\
    cin.tie(0)

// *start on @date: 2020-10-20 10:35
// *writer: wjm

int main() 
{
    IOS;
    int t;
    cin >> t;
    while(t--)
    {
        ll a, ans = 0, t = 1;
        cin >> a;
        ans = (a % 10 - 1) * 10;
        while(a!=0)
        {
            a = a / 10;
            ans += t;
            t++;
        }
        cout << ans << "\n";
    }
    return 0;
}

```
[<font size=4>***B. Yet Another Bookshelf***</font>](https://codeforces.com/contest/1433/problem/B)


### 题目大意：

1.书架上有很多书，1代表此位置有书，0没有书。

2.每次可以抱一摞书移动一个格子。

3.一摞书，多少都可以，连续的1视为一摞。

4.问最少多少次移动可以把所有的书归为一摞。

### 思路：
1.可以移动连续的书

2.所以答案就是1中间0的数量

3.找到最左边的1和最右边的1统计中间0的个数。
 
### 代码：
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define IOS                     \
    ios::sync_with_stdio(false);\
    cin.tie(0)
 
// *start on @date: 2020-10-20 22:44 
// *writer: wjm
int main() 
{
    IOS;
    int t;
    cin >> t;
    while(t--)
    {
        int n;
        cin >> n;
        vector<ll> a(n,0), b;
        for (int i=0;i<n;i++)
        {
            cin >> a[i];
            if(a[i]-1==0)
            {
                b.push_back(i);
 
            }
        }
        if(b.size()-2>=0)
        {
            int ans= b[b.size() - 1] - b[0] - b.size() + 1 ;
            cout <<ans<< "\n"; 
        }
        else 
        {
            cout << "0" << "\n";
        }
        
    }
    return 0;
}
```


[<font size=4>***C. Dominant Piranha***</font>](https://codeforces.com/contest/1433/problem/C)


### 题目大意：
给你一堆序列，一开始选择一个数，每次可以进行一次操作。
如果当前数大于临近的数则可以把周围数“吃掉”，然后序列数减一，该数加一。
经过多次操作后如果可以把序列数变为1，如果存在这样的数则输出该数的下标,否则输出-1。

### 思路：
1.找出最大的数并且该数旁边至少存在一个比它小的数。

2.考虑全部相等的特殊情况。
   
### 代码：
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define IOS                      \
    ios::sync_with_stdio(false); \
    cin.tie(0)

// *start on @date: 2020-10-20 22:34
// *writer: wjm
vector<ll> a(300000 + 3, 0);
set<ll> s;
int main()
{
    IOS;
    int t;
    cin >> t;
    while (t--)
    {
        a.clear();
        s.clear();
        ll n, ans = 0, mx = 0;
        cin >> n;
        vector<ll> a(n + 3, 0);
        set<ll> s;
        for (int i = 1; i <= n; i++)
        {
            cin >> a[i];
            mx = max(mx, a[i]);
            s.insert(a[i]);
        }
        if (s.size() - 1==0)
        {
            cout << "-1"
                 << "\n";
        }
        else
        {
            a[0] = a[1];
            a[n + 1] = a[n];
            for (int i = 1; i <= n; i++)
            {
                if (mx - a[i]==0)
                {
                    if (a[i + 1] != a[i]||a[i] != a[i-1] )
                    {
                        cout << i << "\n";
                        break;
                    }
                }
            }
        }
    }
    return 0;
}

```
[<font size=4>***D. Districts Connection***</font>](https://codeforces.com/contest/1433/problem/D)



### 题目大意：
 1.给出n个数，要求在每个数之间建一条道路。
 
 2.要求相同的两个数之间不能够直接相连，但可以间接相连。
 
 3.若存在请输出这 n-1 条边，答案存在多个。

### 思路：

 1.取不同数建图。
   
 2.并查集判断。
 
### 代码：

 ```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define IOS                      \
    ios::sync_with_stdio(false); \
    cin.tie(0)

// *start on @date: 2020-10-20 22:34
// *writer: wjm
#define endl "\n"
const int MAX = 1e6 + 7;
const int mod = 1e9 + 7;
const ll inf = 0x3f3f3f3f;
vector<ll> vis(MAX), a(MAX), b[MAX];
vector<pair<ll, ll>> p;
ll n, f = 0; //点数
void run()
{
    ll ans = 0;
    for (int i = 0; i < 100; i++)
    {
        ans += 1;
    }
}
void init()
{
    p.clear();
    f = 1;
    for (ll i = 0; i <= n; i++)
    {
        a[i] = vis[i] = 0;
        b[i].clear();
    }
}
void FIND(ll x)
{
    vis[x] = 1;
    for (ll i = 1; i <= n; i++)
    {
        if (i == x)
            continue;
        if (vis[i] || a[i] == a[x])
            continue;
        b[i].push_back(x);
        b[x].push_back(i);
        p.push_back(make_pair(x, i));
        FIND(i);
    }
    return;
}
void check(ll x, ll fa)
{
    if (a[x] == a[fa])
    {
        f = 0;
        return;
    }
    for (int i = 0; i < b[x].size(); i++)
    {
        if (b[x][i] == fa)
            continue;
        check(b[x][i], x);
        if (f == 0)
        {
            return;
        }
    }
}
int main()
{
    IOS;
    int t;
    cin >> t;
    while (t--)
    {
        cin >> n;
        init();
        run();
        for (ll i = 1; i <= n; i++)
            cin >> a[i];
        FIND(1);
        run();
        check(1, 0);
        for (ll i = 1; i <= n; i++)
            if (vis[i] == 0)
                f = 0;
        if (f == 0)
            cout << "NO" << endl;
        else
        {
            cout << "YES" << endl;
            for (auto x : p)
                cout << x.first << " " << x.second << endl;
        }
    }

    return 0;
}
 ```
[<font size=4>***E. Two Round Dances***</font>](https://codeforces.com/contest/1433/problem/E)


### 题目大意：

 1.有n个人，保证n是偶数。

 2.这n个人每次站成2个圈（无区别），每个圈恰好n/2个人。

 3.问你有多少种站法。

### 思路：

1.给定的是N，我们设N/2=n。 

2.可以得到其中一半人（n人）的舞蹈序列中，有n种序列是相同的（旋转得到n）。对于另外一半人也是如此，所以该舞蹈序列中 有 （n*n）种序列是一种分配方式。也就是说，对于所有的分配方式中每（（N*N）/4）种是相同的。

3.总共的分配方式是 N！ 种（将所有位置看作坑位，第一个坑位能选N个人，第二坑位能选择N-1人）。

4.因为人分为两部分，两部分是等价的，所以坑位1与N/2+1实际上是等价的。所以总分配方式要除2。

5.答案就是 (N！/2) / (（（N*N）/4）)==N!/（N*N）/2）。
   
### 代码：
```python
t = eval(input())
ans=0
num = t
f = 1
for i in range(1, t):
    f = f*i
print(int(f/(num/2)))
```
