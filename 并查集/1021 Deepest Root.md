[1021 Deepest Root - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805482919673856&page=0)



```
并查集 or dfs染色判定是否有多颗树
若仅有一棵树 输出所有叶节点
```



```
#include<bits/stdc++.h>
using namespace std;
int fa[10005]; 
int huan = 0;
int find(int x)
{ 
    if (fa[x] == x)
        return x;
    else
    {
        fa[x] = find(fa[x]);
        return fa[x];
    }
}

void merge(int x, int y)
{
    x = find(x);
    y = find(y);
    fa[x] = y;
    if(x==y) huan = 1;
}
vector<int> v[10005];
int n;

int dep;
int visited[10005];
void dfs(int root,int deep){
    dep = max(dep,deep);
    visited[root]=1;
    for(int i=0;i<v[root].size();i++){
        int nxt = v[root][i];
        if(not visited[nxt])
        dfs(nxt,deep+1);
    }
}
void f(){
    int maxdep = 0;
    int ans_root=-1;
    vector<int> ans;
    for(int i=1;i<=n;i++){
        dep = 0;
        for(int j=1;j<=n;j++) visited[j] = 0;
        dfs(i,1);
        //cout<<dep<<endl;
        if(dep > maxdep)
        {
            maxdep = dep;
            ans.clear();
            ans.push_back(i);
        }
        else if(dep==maxdep){
            ans.push_back(i); 
        }
    }
    for(auto i:ans) cout<<i<<endl;
}
int main(){
    cin>>n;
    for(int i=1;i<=n;i++)
        fa[i]=i;
    for(int i=1;i<n;i++){
        int x,y;
        cin>>x>>y;
        merge(x,y);
        v[x].push_back(y);
        v[y].push_back(x);
    }
    if(huan){
        int cnt[n+1]={0};
        int k=0;
        for(int i=1;i<=n;i++) cnt[find(i)]++;
        for(int i=1;i<=n;i++) { 
            if(cnt[i]) k++;
        }
        cout<<"Error: "<<k<<" components";  
    }
    else
    {
        f();
    }
}
```

