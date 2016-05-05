```
#include<iostream>
#include<vector>
#include<cstdio>
#include<cstring>
#include<map>
#include<cmath>
#include<list>
#include<algorithm>
#include<set>
#include<queue>
#include<string>
#include<stack>
using namespace std;
int n,w[10000005];
int node[10000005];
void build(int tag,int l,int r){
    int m=(l+r)>>1;
    if(l==r){
        node[tag]=w[l];
        return ;
    }

    build(tag<<1,l,m);
    build(tag<<1|1,m+1,r);
    node[tag]=max(node[tag<<1],node[tag<<1|1]);
}

void update(int tag,int l,int r,int p,int val){
    int m=(l+r)>>1;
    if(l==r){
        node[tag]=val;
        return ;
    }

    if(p<=m)
    update(tag<<1,l,m,p,val);
    else
    update(tag<<1|1,m+1,r,p,val);
    node[tag]=max(node[tag<<1],node[tag<<1|1]);
}
int query(int tag,int l,int r,int ql,int qr){
    int m=(l+r)>>1,ans=-1;

    if(ql<=l&&qr>=r)
        return node[tag];
    if(ql<=m)ans=max(ans,query(tag<<1,l,m,ql,qr));
    if(m<qr)ans=max(ans,query(tag<<1|1,m+1,r,ql,qr));

    return ans;
}
int main(){

    int t;
    scanf("%d",&t);
    while(t--){

    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        scanf("%d",&w[i]);

    build(1,1,n);
    int q,op,l,r;
    scanf("%d",&q);

    while(q--){
        scanf("%d%d",&l,&r);

            printf("%d\n",query(1,1,n,l,r));

    }
    }
    return 0;
}
```
