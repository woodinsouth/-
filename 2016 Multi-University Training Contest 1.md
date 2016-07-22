# hdu5723 : abandoned country

[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=5723)

## 题目大意



Time Limit: 8000/4000 MS (Java/Others)    Memory Limit: 65536/65536 K


## 做法


**复杂度** $O(n)$



### AC-Code (C++)


time:2948MS	
memory:21520K

```cpp
#include<cstdio>
#include<cstring>
#include<algorithm>
#define ll long long
#define f(x,y,z) for(int x=y;x<=z;x++)
int n,m,T,x,y,fax,fay,k,fa[100005],size[100005],head[100005],next[200005],to[200005];
struct ty{int x,y;ll w;}a[1000005];
ll b[200005],ans;
double ex2;
bool rec[100005];
bool cmp(ty a,ty b)
{
    return a.w<b.w;
}
int find(int x)
{
    if(fa[x]==x)return x;
    fa[x]=find(fa[x]);
    return fa[x];
}
void ad(int x,int y,ll w)
{
    k++;next[k]=head[x];head[x]=k;to[k]=y;b[k]=w;
}
void dfs(int x)
{
    rec[x]=1;
    size[x]=1;
    int now=head[x];
    while(now!=0)
    {
        int y=to[now];
        if(!rec[y])
        {
            ans+=b[now];
            dfs(y);
            size[x]+=size[y];
            //printf("%d %d\n",x,size[x]);
            ex2=ex2+(double)size[y]*(double)(n-size[y])*(double)b[now];
        }
        now=next[now];
    }    
}
int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d%d",&n,&m);
        f(i,1,m)scanf("%d%d%I64d",&a[i].x,&a[i].y,&a[i].w);
        std::sort(a+1,a+1+m,cmp);
        f(i,1,n)fa[i]=i;
        k=0;
        memset(head,0,sizeof(head));
        memset(next,0,sizeof(next));
        memset(rec,0,sizeof(rec));
        memset(size,0,sizeof(size));
        ans=0;
        ex2=0;
        f(i,1,m)
        {
            fax=find(a[i].x);
            fay=find(a[i].y);
            if(fax!=fay)
            {
                ad(a[i].x,a[i].y,a[i].w);
                ad(a[i].y,a[i].x,a[i].w);
                fa[fax]=fay;
            }
        }
        dfs(1);
        printf("%I64d %.2f\n",ans,ex2/((double)n*(double)(n-1)/2));
    }
    return 0;
}
```




 
