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
int w[1000005];
int node[3000005];
int lazy[3000005];
void build(int tag,int l,int r){
    if(l==r){
        node[tag]=w[l];
        return ;
    }
    int m=(l+r)>>1;
    build(tag<<1,l,m);
    build(tag<<1|1,m+1,r);
    node[tag]=node[tag<<1]+node[tag<<1|1];
}
void pushdown(int tag,int l,int r){
    if(lazy[tag]){
        int m=(l+r)>>1;
        lazy[tag<<1]=lazy[tag<<1|1]=lazy[tag];
        node[tag<<1]=(m-l+1)*lazy[tag];
        node[tag<<1|1]=(r-m)*lazy[tag];
        lazy[tag]=0;
    }

}
void update(int tag,int l,int r,int ql,int qr,int val){
    if(ql<=l&&qr>=r){
        node[tag]=val*(r-l+1);
        lazy[tag]=val;
        return ;
    }
    pushdown(tag,l,r);

    int m=(l+r)>>1;
    if(ql<=m)update(tag<<1,l,m,ql,qr,val);
    if(qr>m)update(tag<<1|1,m+1,r,ql,qr,val);
    node[tag]=node[tag<<1]+node[tag<<1|1];
}
int query(int tag,int l,int r,int ql,int qr){

     if(ql<=l&&qr>=r)
        return node[tag];

    pushdown(tag,l,r);

    int m=(l+r)>>1,ans=0;
    if(ql<=m)ans+=query(tag<<1,l,m,ql,qr);
    if(qr>m)ans+=query(tag<<1|1,m+1,r,ql,qr);

    return ans;
}
int main(){

    int n,q,op,ql,qr,val;
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        scanf("%d",&w[i]);

    memset(lazy,0,sizeof(lazy));
    build(1,1,n);

    scanf("%d",&q);
    while(q--){
        scanf("%d",&op);
        if(op==0){
            scanf("%d%d",&ql,&qr);
            printf("%d\n",query(1,1,n,ql,qr));

        }
        else {
            scanf("%d%d%d",&ql,&qr,&val);
            update(1,1,n,ql,qr,val);
        }
    }

    return 0;
}
```
