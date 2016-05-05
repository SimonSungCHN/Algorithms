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
int g[1500][1500];
int linker[1500];
int vis[1500];
int n;
int dfs(int u){

    for(int v=0;v<n;v++)
        if(g[u][v]&&!vis[v]){
                vis[v]=1;

                if(linker[v]==-1||dfs(linker[v])){
                   linker[v]=u;
                   return 1;
            }
    }
     return 0;
}
int main(){

    while(~scanf("%d",&n)){
    memset(g,0,sizeof(g));

    for(int i=0;i<n;i++){
        int ca,cb,k;
        scanf(" %d : ( %d ) ",&ca,&k);
        while(k--){
            scanf("%d",&cb);
            g[ca][cb]=1;
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