---
title: LightOJ-AC_AutoMata
date: 2018-04-22 22:29:21
tags: [algorithm,AC_AutoMata]
---

来源：lightOJ

lightOJ 只有一个AC自动机

    
```cpp 
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <queue>
    using namespace std;
    int n;
    const int MAXN = 262145;
    const int ATLN = 26;
    struct AC_Machine{
        int nxt[MAXN][ATLN];
        int des[MAXN];
        int fail[MAXN];
        int fp[MAXN];
        int root,L;
        void ini(){
            L = 1;
            root = 0;
            memset(fail,0,sizeof fail);
            memset(nxt,0,sizeof nxt);
            memset(fp,0,sizeof fp);
            memset(des,0,sizeof des);
        }
        int ins(char *s){
            int len = strlen(s);
            int now = root;
            for(int i=0;i<len;i++) {
                int ptr = s[i]-'a';
                if(nxt[now][ptr] == 0) nxt[now][ptr] = L++;
                now = nxt[now][ptr];
            }
            des[now] ++;
            return now;
        }
        void build(){
            queue<int>Q;
            while(!Q.empty()) Q.pop();
            int ff;
            for(int i=0;i<ATLN;i++) {
                if(nxt[root][i] != 0) Q.push(nxt[root][i]);
            }
            while(!Q.empty()){
                int now = Q.front();
    //            cout<<"now = "<<now<<endl;
                Q.pop();
                for(int i=0;i<ATLN;i++){
                    int ptr = nxt[now][i];
                    if(!ptr) continue;
                    Q.push(ptr);
                    ff = fail[now];
                    while(ff && nxt[ff][i] == 0) ff = fail[ff];
                    fail[ptr] = nxt[ff][i];
                }
            }
        }
        void lookfor(char *s){
            int len = strlen(s);
            int now = root;
            for(int i=0;i<len;i++) {
                int ptr = s[i]-'a';
                while(now && nxt[now][ptr] == 0) now = fail[now];
                now = nxt[now][ptr];
                int tmp = now;
                while(tmp){
                    fp[tmp]++;
                    tmp = fail[tmp];
                }
            }
        }
    }tree;
    int ans[600];
    char P[1000000+100];
    char Text[600];
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            tree.ini();
            scanf("%d",&n);
            scanf("%s",P);
            for(int i=1;i<=n;i++){
                scanf("%s",Text);
                ans[i] = tree.ins(Text);
            }
    //        cout<<"d1"<<endl;
            tree.build();
    //        cout<<"d2"<<endl;
            tree.lookfor(P);
            printf("Case %d:\n",nc++);
            for(int i=1;i<=n;i++) {
                printf("%d\n",tree.fp[ans[i]]);
            }
        }
        return 0;
    }
    
```
