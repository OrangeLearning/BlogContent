---
title: LightOJ-1129
date: 2018-04-22 22:29:36
tags: [algorithm,Trie]
---
来源：lightOJ1129

字典树，基本上就模板

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN = 100000+10;
    const int ALTN = 10;
    char ch[MAXN][20];
    int n;
    struct Trie{
        int nxt[MAXN][ALTN];
        int idd;
        bool des[MAXN];
        const int root = 0;
        void ini() {
            memset(des,false,sizeof des);
            memset(nxt,0,sizeof nxt);
            idd = 0;
        }
        void ins(char *s) {
            int now = root;
            int len = strlen(s) ;
            for(int i=0;i<len;i++) {
                int ptr = s[i]-'0';
                if(nxt[now][ptr] == 0) nxt[now][ptr] = ++idd;
                now = nxt[now][ptr];
            }
            des[now] = true;
        }
        bool lookfor(char *s){
            int len = strlen(s);
            int now = root;
            for(int i=0;i<len;i++) {
                int ptr = s[i]-'0';
                if(des[now]) return true;
                now = nxt[now][ptr];
            }
            return false;
        }
    }tree;
    bool judge(){
        for(int i=1;i<=n;i++) {
            if(tree.lookfor(ch[i])) return true;
        }
        return false;
    }
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            tree.ini();
            scanf("%d",&n);
            getchar();
            for(int i=1;i<=n;i++){
                gets(ch[i]);
                tree.ins(ch[i]);
            }
            printf("Case %d: ",nc++);
            if(!judge()) puts("YES");
            else puts("NO");
        }
        return 0;
    }
    
```
