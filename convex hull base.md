```
#include<iostream>
#include<cstdio>
#include<vector>
#include<cctype>
#include<cstring>
#include<algorithm>
#include<cmath> 
using namespace std;
struct point{
	double x,y;
};
point p[105],ans[105];
double muli(point x1,point x2,point x3){
	return (x2.x-x1.x)*(x3.y-x1.y)-(x3.x-x1.x)*(x2.y-x1.y);
}
double dis(point x1,point x2){
	return sqrt((x1.x-x2.x)*(x1.x-x2.x)+(x1.y-x2.y)*(x1.y-x2.y));
}
int cmp(point a,point b)
{
 if(muli(a,b,p[0])>0)
  return 1;
 if(muli(a,b,p[0])==0&&dis(a,p[0])<dis(b,p[0]))
  return 1;
 return 0;
}
int main(){
	int n;
	while(~scanf("%d",&n)&&n){
		int i,j,k=0;
		scanf("%lf%lf",&p[0].x,&p[0].y);
		for(i=1;i<n;i++){
		scanf("%lf%lf",&p[i].x,&p[i].y);
		if(p[i].y<p[0].y||((p[i].y==p[0].y)&&(p[i].x<p[0].x)))
		swap(p[i],p[0]);
		} 
		if(n==1){printf("0.00\n");continue;}
		if(n==2){printf("%.2lf\n",2*dis(p[0],p[1]));continue;}
		
		sort(p+1,p+n,cmp);
 int top=2;
 ans[0]=p[0],ans[1]=p[1],ans[2]=p[2];
 for(i=3;i<n;i++)
 {
  while(top>1&&muli(ans[top-1],ans[top],p[i])<=0)
   top--;
  ans[++top]=p[i];
 }
	double sum=0;
	for(i=1;i<=top;i++)
	sum+=dis(ans[i],ans[i-1]);
	sum+=dis(ans[0],ans[top]);
	
	printf("%.2lf\n",sum);	
	}
return 0;
}
```