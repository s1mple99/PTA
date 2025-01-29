[1003 Emergency - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805523835109376&page=0)



```
5个城市 6条路径 求0到2最短路径条件下的最大value值
输入给定5个城市的value值分别为[1,2,1,5,3]
以及6条无向路径的长度
先用dijkstra求出最短路径条件下的front数组
再对front跑dfs求最大value
```



```
#include<bits/stdc++.h>
using namespace std;
int n,m;
const int MAXN = 1000;
int value[MAXN];

struct edge{
    int v,w;
};
vector<edge> e[MAXN];
vector<int> front[MAXN];
struct node{
    int dis,u;
    bool operator>(const node& a)const
    {
        return dis>a.dis;
    }
};

priority_queue<node,vector<node>,greater<node>> q;
int dis[MAXN];
int vis[MAXN];
void dij(int s){
    for(int i=0;i<n;i++) {dis[i] = INT_MAX;vis[i]=0;}
    dis[s] = 0;
    q.push({0,s});
    while(not q.empty()){
        int u = q.top().u;
        q.pop();
        if(vis[u]) continue;
        vis[u] = 1;
        for(auto ed:e[u]){ 
            int v = ed.v,w=ed.w; //u当前 v下一个点 w边值
            if(dis[v] > dis[u]+w){
                dis[v] = dis[u] + w;
                q.push({dis[v],v});
                //cout<<u<<" "<<v<<" "<<w<<endl;
                front[v].clear();
                front[v].push_back(u);
            }
            else if(dis[v]==dis[u]+w){
                //cout<<u<<" "<<v<<" "<<w<<endl;
                front[v].push_back(u);
            }
        }
    }
    
}
int s,t;
int ans = 0;
int cnt = 0 ;
void dfs(int cur,int val){
    if(cur == s) cnt++;
    ans = max(ans,val);
    for(int i=0;i<front[cur].size();i++){
        int nxt = front[cur][i];
        dfs(nxt,val+value[nxt]);
    }
}
int main(){
    cin>>n>>m;
    cin>>s>>t;
    for(int i=0;i<n;i++) cin>>value[i];
    for(int i=1;i<=m;i++) {
        int u,v,w;cin>>u>>v>>w;
        //cout<<u<<" "<<v<<" "<<w<<endl;
        e[u].push_back({v,w});
        e[v].push_back({u,w});
    }
    dij(s);
    dfs(t,value[t]);
    cout<<cnt<<" "<<ans;
}


```

