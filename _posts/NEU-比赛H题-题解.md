---
title: NEU 比赛H题 题解
date: 2017-07-22 20:46:42
tags: [algorithm,trick]
category: [ACM]
---

### 题意
> 很多件事情，每个事件有一个开始时间和一个结束时间，并且做完这件事情，会获得对应的收益，现在要求只做两件事情，两件事情的收益和恰好为一个给定值，这个时候要求完成的这两件事情不重合，同时总时间最短

[链接](https://oj.neu.edu.cn/contest/70/problem/8)

### 思路分析

##### 不完美思路
开N个vector，利用vector的下表记录val从而在O(1)时间找到两部分，一个对于开始时间排序，一个对于结束时间排序，随后二分+ST表进行查询(详情参照我的TLE代码)，虽然进行了大量的常数优化，然而在多组数据的情况下就不是非常好了
但是这种思路是非常好理解的

##### 代码
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <vector>
using namespace std;
const int MAXN = 2e5+10;
const int INF = 0x3f3f3f3f;
int n,m;
struct Node{
    int st,ed;
    Node(int ss=0,int ee=0):st(ss),ed(ee){}
};
vector<Node> vec[MAXN],v1,v2;
bool cmp1(Node a,Node b){ return a.st < b.st; }
bool cmp2(Node a,Node b){ return a.ed < b.ed; }
int Log[MAXN];
int dp[MAXN][20];
void initlog(){
    Log[0] = -1;
    for(int i=1;i<MAXN;i++) {
        Log[i] = Log[i >> 1] + 1;
    }
}
void st_init(vector<Node> tmp){
    // memset(dp,0,sizeof dp);
    int n = tmp.size();
    for(int i=1;i<=n;i++) dp[i][0] = tmp[i-1].ed - tmp[i-1].st + 1;
    int m = Log[n];

    for(int j=1;j<=m;j++){
        int t = n - (1 << j) + 1;
        for(int i=t;i<=t;++i){
            dp[i][j] = min(dp[i][j-1],dp[i+(1<<(j-1))][j-1]);
        } 
    }
}

inline int query(int l,int r){
    int k = Log[r - l + 1];
    return min(dp[l][k],dp[r-(1<<k)+1][k]);
}

int fun(int idx,int tmp,vector<Node> v){
    int l = idx;
    int r = v.size()-1;
    int res = v.size();
    while(l <= r){
        int mid = (l + r) >> 1;
        if(tmp < v[mid].st) {
            res = min(res,mid);
            r = mid - 1;
        }
        else {
            l = mid + 1;
        }
    }
    if(res == v.size()) return -1;
    else return res;
}
vector<int> vvv;
int main(){
    initlog();
    while(scanf("%d%d",&n,&m)!=EOF){
        // cout<<"n = "<<n<<" m = "<<m<<endl;
        for(int i=0;i<=m;i++) vec[i].clear();
        vvv.clear();
        int l,r,val;
        for(int i=1;i<=n;i++){
            scanf("%d%d%d",&l,&r,&val);
            vec[val].push_back(Node(l,r));
            vvv.push_back(val);
        }
        int ans = INF;
        int idx = 0;
        for(int _=0;_<vvv.size();++_){
            // cout<<"i = "<<i<<endl;
            int i = vvv[_];
            if(i > m / 2) break;
            v1 = vec[i];
            v2 = vec[m-i];
            if(v2.size() == 0) continue;
            sort(v1.begin(),v1.end(),cmp1);
            // sort(v2.begin(),v2.end(),cmp2);
            st_init(v1);
            idx = 0;
            for(int j=0;j<v2.size();j++){
                int ed = v2[j].ed;
                idx = fun(idx,ed,v1);
                if(v2[j].ed - v2[j].st + 1 >= ans) continue;
                if(idx == -1) break;
                ans = min(ans,v2[j].ed - v2[j].st + 1 + query(idx+1,v1.size()));
            }
            // sort(v1.begin(),v1.end(),cmp2);
            sort(v2.begin(),v2.end(),cmp1);
            st_init(v2);
            idx = 0;
            for(int j=0;j<v1.size();j++){
                int ed = v1[j].ed;
                idx = fun(idx,ed,v2);
                if(v1[j].ed - v1[j].st + 1 >= ans) continue;
                if(idx == -1) break;
                ans = min(ans,v1[j].ed - v1[j].st + 1 + query(idx+1,v2.size()));
            }
        }

        if(ans != INF)
            printf("%d\n",ans);
        else puts("oh no!");
    }
    return 0;
}
```


### 正确的做法
**感谢CHD的WZM同学提供的解法**

我们在上面的做法中，我们所花的时间最大的是什么；建立ST表，我们需要考虑的是，我们是否真的需要ST表进行最小值的查询

首先，关于我们做两次的事情：
> 启发1：如果我们每次都是用后面的事件匹配前面的程序，那么实际上我们只需要遍历所有点程序就可以了

一个显然的点是，如果我遍历了所有点事件，那么为了避免重复，我们其实是只需要使用后面那个去匹配前面那个就可以了

> 启发2：我既然一定是一个不断向后的过程，那么我是否是需要记录前面所有的值，答案是否定的

由于我只求最小值，所以这个时候我们实际上只需要记录

> 启发3：既然是已知向后扫，那么是否可以直接运用向后的这种机制使得我们不需要进行判断是否重合，显然也是可以的

##### 代码
```cpp
/* 
    非常巧妙的方法

    首先是这样的，因为是一定只有两个事件，所以实际上只需要使用后一个匹配前一个或者是前一个匹配后一个就可以了。现在的问题是，如何去判重，以及如何去取得最小值

    参见我的H.cpp文件，是使用的ST表的方法，但是这个方法有个致命问题是在多组样例的时候需要大量的重复操作，所以TLE了

    首先一点是，如果使用离散化的思路，那么进入一个区间和出去一个区间我都能知道
    其次，我们进入一个点的时候，前面所有我曾经到过出节点的事件，我都是可以去做的
    再次，我只需要求最小值，并且因为cost固定的原因，这个时候我们就完全可以有效的进行更新O(1)
    最后，我们得到思路：
        离散化所有点
        按照前后进行扫，如果是进入区间的点，那么这个时候我们查询所可以匹配的数字的最小值
        当遭遇到一个出区间的点的时候，我们就必须要更新一个最小值
        由于前后的相对关系，这个时候一定不是重复的，而且不会有遗落，这个时候就恰好完成看这道题
 */
#include <bits/stdc++.h>
using namespace std;
const int maxn = 4e5+5;
const int inf = 0x3f3f3f3f;

// 这个是一个价值的类似于hash的东西
struct _COST_{
    int have;
    int len;
}Cost[maxn];

// 记录事件
struct segment{
    int node,len,mark;
    int cost;
    segment(){}
    segment(int Node,int Len,int Mark,int Cost){
        node = Node;
        len = Len;
        mark = Mark;
        cost = Cost;
    }

    // 这个函数就可以使得拆成两个节点
    friend bool operator < (segment A,segment B){
        if(A.node==B.node){
            return A.mark>B.mark;
        }
        else return A.node<B.node;
    }
}seg[maxn];

int main(){
    int n,m;
    while(cin>>n>>m){
        for(int i=0;i<maxn;i++){
            Cost[i].have = -1;
            Cost[i].len = inf;
        }
        memset(seg,0,sizeof(seg));
        int cnt = 0;
        for(int i=1;i<=n;i++){
            int l,r,cost;
            cin>>l>>r>>cost;
            seg[++cnt] = segment(l,r-l+1,1,cost);
            seg[++cnt] = segment(r,r-l+1,-1,cost);
        }
        sort(seg+1,seg+cnt+1);
        int ans = inf;
        for(int i=1;i<=cnt;i++){
            // 如果刚刚进入这个段，则更新之前的和这个进行匹配的答案
            if(seg[i].mark==1){
                int other = m-seg[i].cost;
                if(other>0 && Cost[other].have!=-1){
                    ans = min(ans,Cost[other].len+seg[i].len);
                }
            }
            else{
                // 当出去一个节点的时候这个就进行最小值的更新
                Cost[seg[i].cost].have = 1;
                Cost[seg[i].cost].len = min(Cost[seg[i].cost].len,seg[i].len);
            }
        }
        if(ans==inf){
            cout<<"oh no!"<<endl;
        }
        else cout<<ans<<endl;
      //  cout<<(ans==inf?"oh no!":ans)<<endl;
    }
}
/*
4 10
1 2 3
3 4 7
4 6 7
3 7 7
1 10
1 10 10
*/
```
