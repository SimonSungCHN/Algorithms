```
#include<vector>
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>
#include<set>
#include<list>
#include<queue>
#include<cmath>
using namespace std;
#define inf 10000000
struct edge{
   int from,to,cap,cost;
};
vector<edge>edges;
vector<int>g[105];
int inq[105];
int d[105];
int p[105];
int a[105];
int n,m,cost,flow;
void addedge(int from,int to,int cap,int cost){
   edges.push_back((edge){from,to,cap,cost});
   edges.push_back((edge){to,from,0,-cost});
   int l=edges.size();
   g[from].push_back(l-2);
   g[to].push_back(l-1);
}
bool fun(int s,int t){
    memset(inq,0,sizeof(inq));
    for(int i=1;i<=n;i++)
    d[i]=inf;
    d[s]=0;
    inq[s]=1;
    p[s]=0;
    a[s]=inf;

    queue<int>que;
    que.push(s);

    while(!que.empty()){
        int u=que.front();
        que.pop();
        inq[u]=0;
        for(int i=0;i<g[u].size();i++){
            edge e=edges[g[u][i]];
            if(e.cap>0&&d[e.to]>d[u]+e.cost){
                d[e.to]=d[u]+e.cost;
                p[e.to]=g[u][i];
                a[e.to]=min(a[u],e.cap);
                if(!inq[e.to]){
                    que.push(e.to);
                    inq[e.to]=1;
                }
            }
        }
    }
    
     if(d[t]==inf)
        return false;

     flow+=a[t];
     cost+=d[t]*a[t];
    
     int u=t;
     while(u!=s){
        edges[p[u]].cap-=a[t];
        edges[p[u]^1].cap+=a[t];
        u=edges[p[u]].from;
     }
    return true;
}
int mincost(int s,int t){
	  flow=0,cost=0;
	while(fun(s,t));
	return cost;
}

int main(){

    
  return 0;
}
```