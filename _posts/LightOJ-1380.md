---
title: LightOJ-1380
date: 2018-04-22 22:31:31
tags: [algorithm,zhuliu]
---
来源：lightOJ  1380

最小树形图

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN = 1010;
    const int MAXM = 10010;
    struct Edge{
        int u,v,w;
    }edge[MAXN<<2];
    int pre[MAXN];
    int id[MAXN];
    int vis[MAXN];
    int in[MAXN];
    const int INF = 0x3f3f3f3f;
    int zhuliu(int root,int n,int m,Edge edge[]){
        int res = 0;
        int u,v;
        while(1){
            for(int i=0;i<n;i++) in[i] = INF;
            for(int i=0;i<m;i++){
                if(edge[i].u != edge[i].v && edge[i].w < in[edge[i].v]){
                    pre[edge[i].v] = edge[i].u;
                    in[edge[i].v] = edge[i].w;
                 }
            }
            for(int i=0;i<n;i++){
                if(i!=root && in[i] == INF) return -1;
            }
            int tn = 0;
            memset(id,-1,sizeof id);
            memset(vis,-1,sizeof vis);
            in[root] = 0;
            for(int i=0;i<n;i++){
                res += in[i];
                v = i;
                while(vis[v] != i && id[v] == -1 && v!=root){
                    vis[v] = i;
                    v = pre[v];
                }
                if(v!=root && id[v] == -1){
                    for(int u = pre[v];u!=v;u=pre[u]){
                        id[u] = tn;
                    }
                    id[v] = tn ++;
                }
            }
            if(tn == 0) break;
            for(int i=0;i<n;i++){
                if(id[i] == -1) id[i] = tn++;
            }
            for(int i=0;i<m;){
                v = edge[i].v;
                edge[i].u = id[edge[i].u];
                edge[i].v = id[edge[i].v];
                if(edge[i].u != edge[i].v)
                    edge[i++].w -= in[v];
                else
                    swap(edge[i],edge[--m]);
            }
            n = tn;
            root = id[root];
        }
        return res;
    }
    int g[MAXN][MAXN];
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            int n,m,rt;
            scanf("%d%d%d",&n,&m,&rt);
            for(int i=0;i<n;i++)
                for(int j=0;j<n;j++)
                    g[i][j] = INF;
            int u,v,w;
            while(m--){
                scanf("%d%d%d",&u,&v,&w);
                if(u == v) continue;
                g[u][v] = min(g[u][v],w);
            }
            int L = 0;
            for(int i =0;i<n;i++){
                for(int j=0;j<n;j++){
                    if(g[i][j] < INF){
                        edge[L].u = i;
                        edge[L].v = j;
                        edge[L++].w = g[i][j];
                    }
                }
            }
            int ans = zhuliu(rt,n,L,edge);
            printf("Case %d: ",nc++);
            if(ans == -1) puts("impossible");
            else printf("%d\n",ans);
        }
        return 0;
    }
    
```
