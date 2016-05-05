```
#include<cstdio>
#include<cstring>
#include<cmath>
#include<iostream>
#include<algorithm>
#include<set>
#include<map>
#include<queue>
#include<vector>
#include<numeric>
using namespace std;
#define inf 1000000000
int n,x,s,t,cap[105][105],vis[105];
bool bfs(int s,int t){
  queue<int>que;
  memset(vis,-1,sizeof(vis));
  vis[s]=0;
  que.push(s);
  while(!que.empty()){
    int now=que.front();
    que.pop();

    for(int i=0;i<n;i++)
    if(cap[now][i]>0&&vis[i]==-1){
        vis[i]=vis[now]+1;
        que.push(i);
    }
  }
  return vis[t]>=0;
}
int dfs(int s,int t,int MAX){
    int a;
    if(s==t)
        return MAX;

     for(int i=0;i<n;i++)
         if(cap[s][i]>0&&vis[i]==vis[s]+1&&(a=dfs(i,t,min(MAX,cap[s][i]))))
         {
             cap[s][i]-=a;
             cap[i][s]+=a;
             return a ;
         }
     return 0;
}
int dinic(int s,int t){
   int sum=0,ans;
        while(bfs(s,t))
            sum+=dfs(s,t,inf);

            return sum;
}
```