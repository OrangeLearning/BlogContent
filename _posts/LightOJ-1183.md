---
title: LightOJ-1183
date: 2018-04-22 22:29:40
tags: [algorithm,Segment_Tree]
---
来源：lightOJ1183

线段树，稍加改动而已

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #define lson rt<<1
    #define rson rt<<1|1
    #define L (tree[rt].l)
    #define R (tree[rt].r)
    using namespace std;
    const int  MAXN = 100010;
    struct Segment{
        int l,r;
        long long sum;
        long long lazy;
    }tree[MAXN<<2];
    long long gcd(long long a,long long b){
        if(!b) return a;
        else return gcd(b,a%b);
    }
    inline void pushdown(int rt) {
        if(tree[rt].lazy!=-1) {
            long long lazy = tree[rt].lazy;
            int mid = (tree[rt].l + tree[rt].r)>>1;
            tree[rt].lazy = -1;
            tree[lson].lazy = tree[rson].lazy = lazy;
            tree[lson].sum = lazy * (tree[lson].r-tree[lson].l+1);
            tree[rson].sum = lazy * (tree[rson].r-tree[rson].l+1);
            tree[rt].sum = lazy * (tree[rt].r - tree[rt].l + 1);
        }
    }
    inline void pushup(int rt){
        tree[rt].sum = tree[lson].sum + tree[rson].sum;
    }
    void build(int rt,int l,int r){
        tree[rt].l = l;
        tree[rt].r = r;
        tree[rt].sum = 0;
        tree[rt].lazy = -1;
        if(l == r) return ;
        int mid = (l+r) >> 1;
        build(lson,l,mid);
        build(rson,mid+1,r);
        pushup(rt);
    }
    void update(int rt,int l,int r,int data){
        if(l <= tree[rt].l && tree[rt].r <= r) {
            tree[rt].lazy = data;
            tree[rt].sum = data*(tree[rt].r - tree[rt].l + 1);
            return ;
        }
        pushdown(rt);
        int mid = (tree[rt].l + tree[rt].r) >> 1;
        if(l <= mid) update(lson,l,r,data);
        if(r  > mid) update(rson,l,r,data);
        pushup(rt);
    }
    long long query(int rt,int l,int r){
        if(l <= tree[rt].l && tree[rt].r <= r){
            return tree[rt].sum;
        }
        pushdown(rt);
    //    long long res = 0;
        int mid = (tree[rt].l + tree[rt].r) >> 1;
        if(r <= mid) return query(lson,l,r);
        else if(l > mid) return query(rson,l,r);
        else return (query(lson,l,mid) + query(rson,mid+1,r));
    }
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            int n,Qm;
            scanf("%d%d",&n,&Qm);
            build(1,1,n);
            printf("Case %d:\n",nc++);
            while(Qm--){
                int op;
                scanf("%d",&op);
                if(op == 1) {
                    int l,r,data;
                    scanf("%d%d%d",&l,&r,&data);
                    l++;r++;
                    update(1,l,r,data);
                }
                else if(op == 2){
                    int l,r;
                    scanf("%d%d",&l,&r);
                    l++;r++;
                    long long sum = query(1,l,r);
                    long long duan = (long long)r-l+1;
                    long long du = gcd(sum,duan);
                    sum /= du;
                    duan /= du;
                    if(duan == 1) printf("%lld\n",sum);
    //                else if(sum == 0) printf("%lld\n",sum);
                    else printf("%lld/%lld\n",sum,duan);
                }
            }
        }
        return 0;
    }

```
