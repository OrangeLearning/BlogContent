---
title: lightOJ-1040
date: 2018-04-21 23:28:31
tags: [algorithm,MST]
---
#  lightOJ 1040

一个简单的最小生成树的问题，只要注意取一个最小值就可以了。还是比较轻松的。

    
```cpp    
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
const int MAXN = 55;
const int INF = 0x3f3f3f3f;
int mat[MAXN][MAXN];
int n;
int dist[MAXN];
bool vis[MAXN];

int solve(int sum){
    int begin = 1;
    for(int i = 1;i <= n;i++){
        if(i == begin) dist[i] = 0;
        else dist[i] = min(mat[begin][i],mat[i][begin]);
    }
    int dv,ds;
    memset(vis,false,sizeof vis);
    vis[begin] = true;
    int res = 0;
    for(int cas = 1;cas < n;cas ++){
        dv = -1;
        ds = INF;
        for(int i=1;i<=n;i++){
            if(!vis[i] && dist[i] < ds){
                dv = i;
                ds = dist[i];
            }
        }
        if(dv == -1) return -1;
        vis[dv] = true;
        res += ds;
        for(int i=1;i<=n;i++){
            if(!vis[i] && dist[i] > min(mat[dv][i],mat[i][dv])){
                dist[i] = min(mat[dv][i],mat[i][dv]);
            }
        }
    }
    return sum - res;
}
int main(){
    int T,nc = 1;
    scanf("%d",&T);
    while(T--){
        scanf("%d",&n);
        int sum = 0;
        for(int i = 1;i<=n;i++) {
            for(int j = 1;j<=n;j++) {
                scanf("%d",&mat[i][j]);
                sum += mat[i][j];
                if(mat[i][j] == 0) mat[i][j] = INF;
            }
        }
        // prim();
        printf("Case %d: %d\n",nc++,solve(sum));
    }
    return 0;
}
```