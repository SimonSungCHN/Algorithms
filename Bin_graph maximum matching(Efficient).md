```
#include<iostream>
#include<cstdio>
#include<cstring>
#include<queue>
#include<algorithm>
#include<vector>
#include<cmath>
#include<list>
#include<set>
#include<map>
using namespace std;
vector<int>g[2000];
int linker[2000];
int vis[2000];
int n;
int dfs(int u){
    for(int v=0;v<g[u].size();v++)
        if(!vis[g[u][v]]){
            vis[g[u][v]]=1;
      if(linker[g[u][v]]==-1||dfs(linker[g[u][v]])){
                linker[g[u][v]]=u;
                return 1;
            }
    }
    return 0;
}
int main(){


    while(~scanf("%d",&n)){
    for(int i=0;i<2000;i++)
        g[i].clear();

        for(int i=0;i<n;i++){
            int ca,k,cb;
            scanf(" %d : ( %d )",&ca,&k);
            while(k--){
                scanf("%d",&cb);
                g[ca].push_back(cb);
            }
        }

    memset(linker,-1,sizeof(linker));
    int flag=0;
    for(int i=0;i<n;i++){
        memset(vis,0,sizeof(vis));
        if(dfs(i))flag++;
    }
    printf("%d\n",flag);


    }
	return 0;
}
```