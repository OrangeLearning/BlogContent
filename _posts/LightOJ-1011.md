---
title: LightOJ-1011
date: 2018-04-22 22:29:27
tags: [algorithm,MST,link-cut-tree]
---
来源：lightOJ1011

MST+树链剖分

树剖写挫了RE一个晚上啊

代码：

```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <vector>
    #define lson rt<<1
    #define rson rt<<1|1
    using namespace std;
    int n,m,Q;
    const int MAXN = 50010;
    struct Edge{//Treelink
        int nxt,to,w;
    }edge[MAXN<<2];
    struct Qnode{//MST
        int u,v,w;
        inline void input(){
            scanf("%d%d%d",&u,&v,&w);
        }
        inline void get(int uu,int vv,int ww){
            u = uu;
            v = vv;
            w = ww;
        }
    }qnode[MAXN<<2],act[MAXN<<2];
    int nnn;
    int cmp(Qnode a,Qnode b){
        return a.w<b.w;
    }
    int head[MAXN],tot;
    int sum[MAXN],fa[MAXN],son[MAXN],p[MAXN],dep[MAXN],fp[MAXN],top[MAXN],pos;
    int gr[MAXN<<1];
    struct Segment{
        int l,r;
        int val;
    }tree[MAXN<<2];
    inline void ini(){
        memset(head,-1,sizeof head);
        memset(son,-1,sizeof son);
        tot = nnn = pos = 0;
    }
    inline void addedge(int u,int v,int w){
        edge[tot].to = v;
        edge[tot].nxt = head[u];
        edge[tot].w = w;
        head[u] = tot ++;
    }
    int Find(int x){
        if(gr[x] == -1) return x;
        else return gr[x] = Find(gr[x]);
    }
    void kruscal(){
        memset(gr,-1,sizeof gr);
        sort(qnode+1,qnode+1+m,cmp);
        for(int i=1;i<=m;i++){
            int u = qnode[i].u;
            int v = qnode[i].v;
            int w = qnode[i].w;
            int f1 = Find(u);
            int f2 = Find(v);
            if(f1!=f2){
                gr[f1] = f2;
                addedge(u,v,w);
                addedge(v,u,w);
                act[++nnn].get(u,v,w);
            }
        }
    }
    void dfs(int rt,int pre,int d){
        sum[rt] = 1;
        fa[rt] = pre;
        dep[rt] = d;
        for(int i=head[rt];i!=-1;i=edge[i].nxt){
            int now = edge[i].to;
            if(now == pre) continue;
            dfs(now,rt,d+1);
            sum[rt] += sum[now];
            if(son[rt] == -1 || sum[now]>sum[son[rt]]) {
                son[rt] = now;
            }
        }
    }
    void getpos(int rt,int sp){
        top[rt] = sp;
        p[rt] = ++pos;
        fp[p[rt]] = rt;
        if(son[rt]==-1) return ;
        getpos(son[rt],sp);
        for(int i=head[rt];i!=-1;i=edge[i].nxt){
            int now = edge[i].to;
            if(now == fa[rt] || now == son[rt]) continue;
            getpos(now,now);
        }
    }
    
    inline void pushup(int rt){
        tree[rt].val = max(tree[lson].val,tree[rson].val);
    }
    void build(int rt,int l,int r){
        tree[rt].l = l;
        tree[rt].r = r;
        tree[rt].val = 0;
        if(l == r) {
            return ;
        }
        int mid = (l+r)>>1;
        build(lson,l,mid);
        build(rson,mid+1,r);
        pushup(rt);
    }
    void update(int rt,int pos,int data){
        if(tree[rt].l == pos && pos == tree[rt].r) {
            tree[rt].val = data;
            return ;
        }
        int mid = (tree[rt].l+tree[rt].r)>>1;
        if(pos<=mid) update(lson,pos,data);
        if(pos>=mid+1) update(rson,pos,data);
        pushup(rt);
    }
    int query(int rt,int l,int r){
        if(l<=tree[rt].l  && tree[rt].r<=r){
            return tree[rt].val;
        }
        int mid = (tree[rt].l+tree[rt].r)>>1;
        if(r<=mid) return query(lson,l,r);
        else if(l>mid) return query(rson,l,r);
        else return max(query(lson,l,mid),query(rson,mid+1,r));
    }
    int solve(int u,int v){
        int ans = -1;
        int f1 = top[u];
        int f2 = top[v];
        while(f1!=f2){
            if(dep[f1]<dep[f2]){
                swap(f1,f2);
                swap(u,v);
            }
            ans = max(ans,query(1,p[f1],p[u]));
            u = fa[f1];
            f1 = top[u];
        }
        if(u == v) return ans;
        else if(dep[u]>dep[v]) swap(u,v);
        ans = max(ans,query(1,p[son[u]],p[v]));
        return ans;
    }
    int main(){
        int T,nc = 1;
        int u,v,w;
        int l,r;
        scanf("%d",&T);
        while(T--){
            ini();
            scanf("%d%d",&n,&m);
            for(int i=1;i<=m;i++){
                qnode[i].input();
            }
            kruscal();
            dfs(1,-1,0);
            pos = 0;
            getpos(1,1);
            build(1,1,pos);
            for(int i=1;i<=nnn;i++){
                int u = act[i].u;
                int v = act[i].v;
                int cost = act[i].w;
                if(dep[u]>dep[v]) swap(u,v);
                update(1,p[v],cost);
            }
            printf("Case %d:\n",nc++);
            scanf("%d",&Q);
            while(Q--){
                scanf("%d%d",&l,&r);
                printf("%d\n",solve(l,r));
            }
        }
        return 0;
    }
```