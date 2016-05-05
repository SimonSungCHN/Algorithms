```
#include <iostream>  
#include <cstring>  
#include <cstdio>  
#include <cstdlib>  
#include <vector>  
using namespace std;  
const int MAX=1000;  
int indegree[MAX];  
int ancestor[MAX];  
int set[MAX];  
int vis[MAX];  
int tim[MAX];  
vector<int> adj[MAX];  
vector<int> que[MAX];  
void init(int n)  
{  
    memset(tim,0,sizeof(tim));  
    memset(vis,0,sizeof(vis));  
    memset(indegree,0,sizeof(indegree));  
    for(int i=1;i<=n;i++)  
    {  
        adj[i].clear();  
        que[i].clear();  
        set[i]=i;  
        ancestor[i]=i;  
    }  
}  
  
int find(int k)  
{  
    if(k!=set[k])
	set[k]=find(set[k]);
    return set[k];  
}  
  
void dfs(int i)  
{  
    int len=adj[i].size();  
    for(int j=0;j<len;j++)  
    {  
        int son=adj[i][j];  
        dfs(son);  
        set[son]=i;  
        ancestor[find(i)]=i;  
    }  
    vis[i]=1;  
    len=que[i].size();  
    for(int j=0;j<len;j++)  
    {  
        int son=que[i][j];  
        if(vis[son])  
        {  
            int ans=ancestor[find(son)];  
            tim[ans]++;  
        }  
    }  
}  
  
int main()  
{  
    int n,i,t,a,b;  
    while(scanf("%d",&n)!=EOF)  
    {  
        init(n);  
        for(i=0;i<n;i++)  
        {  
            scanf("%d:(%d)",&a,&t);  
            while(t--)  
            {  
                scanf("%d",&b);  
                indegree[b]++;  
                adj[a].push_back(b);  
            }  
        }  
        
        scanf("%d",&t);  
        while(t--)  
        {  char s1[100],s2[100],s3[100];
            
            scanf("%1s%d%1s%d%1s",s1,&a,s2,&b,s3);
            que[a].push_back(b); 
            que[b].push_back(a);
        }  
         
        for(i=1;i<=n;i++)  
        {  
            if(indegree[i]==0)  
            {              
                dfs(i);  
                break;  
            }  
        }  
        for(i=1;i<=n;i++)  
            if(tim[i])printf("%d:%d\n",i,tim[i]);  
    }  
    return 0;  
}
```