---
title: LightOJ-1339
date: 2018-04-22 22:29:42
tags: [algorithm,Segment_Tree]
---

来源：lightOJ1339

线段树，要维护的东西比较多，但是稍微想想还是可做的

代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #define lson rt<<1
    #define rson rt<<1|1
    using namespace std;
    const int MAXN = 100010;
    int a[MAXN];
    struct Segment{
        int l,r;
        int lsum,lc;
        int rsum,rc;
        int sum;
    }tree[MAXN<<2];
    inline void pushup(int rt) {
        int len = tree[rt].r - tree[rt].l + 1;
        if(tree[lson].rc != tree[rson].lc) {
            tree[rt].sum = max(tree[lson].sum,tree[rson].sum);
        }
        else {
            int sum = tree[lson].rsum + tree[rson].lsum;
            tree[rt].sum = max(sum,max(tree[lson].sum,tree[rson].sum));
        }
        tree[rt].lc = tree[lson].lc;
        tree[rt].rc = tree[rson].rc;
        tree[rt].lsum = tree[lson].lsum;
        tree[rt].rsum = tree[rson].rsum;
        if(tree[rt].lsum == ((len+1)>>1) && tree[rson].lc == tree[lson].rc) tree[rt].lsum += tree[rson].lsum;
        if(tree[rt].rsum == (len>>1) && tree[lson].rc == tree[rson].lc) tree[rt].rsum += tree[lson].rsum;
    }
    void build(int rt,int l,int r){
        tree[rt].l = l;
        tree[rt].r = r;
        tree[rt].lsum = tree[rt].rsum = tree[rt].sum = 0;
        tree[rt].lc = tree[rt].rc  = 0;
        if(l == r) {
            int x;
            scanf("%d",&x);
            tree[rt].lsum = tree[rt].rsum = tree[rt].sum = 1;
            tree[rt].lc = tree[rt].rc  = x;
            return ;
        }
        int mid = (l + r) >> 1;
        build(lson,l,mid);
        build(rson,mid+1,r);
        pushup(rt);
    }
    int query(int rt,int l,int r){
        if(l <= tree[rt].l && tree[rt].r <= r){
            return tree[rt].sum;
        }
        int res = 0;
        int mid = (tree[rt].l + tree[rt].r) >> 1;
        if(l <= mid) res = max(res,query(lson,l,r));
        if(r  > mid) res = max(res,query(rson,l,r));
        if(tree[lson].rc == tree[rson].lc) {
            int tmpa = min(tree[lson].rsum,mid-l+1);
            int tmpb = min(tree[rson].lsum,r-mid);
            res = max(res,tmpa+tmpb);
        }
        return res;
    }
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            int n,c,Qm;
            scanf("%d%d%d",&n,&c,&Qm);
            build(1,1,n);
            printf("Case %d:\n",nc++);
            while(Qm--) {
                int l,r;
                scanf("%d%d",&l,&r);
                printf("%d\n",query(1,l,r));
            }
        }
        return 0;
    }
    
``` 

