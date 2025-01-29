[1030 Travel Plan - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805464397627392&page=0)



```
4个城市 5条路径 求0到3最短路径条件下的最小cost值
给定5条无向路径的长度和cost
先用dijkstra求出最短路径条件下的front数组
再对front跑dfs求最小cost
//和1003很像
```



```
#include <bits/stdc++.h>
using namespace std;
int n, m;
const int MAXN = 505;
int value[MAXN];

struct edge
{
    int v, w;
};
vector<edge> e[MAXN];
vector<int> front[MAXN];
struct node
{
    int dis, u;
    bool operator>(const node &a) const
    {
        return dis > a.dis;
    }
};

priority_queue<node, vector<node>, greater<node>> q;
int dis[MAXN];
int vis[MAXN];
void dij(int s)
{
    for (int i = 0; i < n; i++)
    {
        dis[i] = INT_MAX;
        vis[i] = 0;
    }
    dis[s] = 0;
    q.push({0, s});
    while (not q.empty())
    {
        int u = q.top().u;
        q.pop();
        if (vis[u])
            continue;
        vis[u] = 1;
        for (auto ed : e[u])
        {
            int v = ed.v, w = ed.w; // u当前 v下一个点 w边值
            if (dis[v] > dis[u] + w)
            {
                dis[v] = dis[u] + w;
                q.push({dis[v], v});
                // cout<<u<<" "<<v<<" "<<w<<endl;
                front[v].clear();
                front[v].push_back(u);
            }
            else if (dis[v] == dis[u] + w)
            {
                // cout<<u<<" "<<v<<" "<<w<<endl;
                front[v].push_back(u);
            }
        }
    }
}
int s, t;
int ans = INT_MAX;
vector<int> road;
vector<int> ret;
int g[MAXN][MAXN];
void dfs(int cur, int val)
{
    if (cur == s)
    {
        if (ans > val)
        {
            ans = min(ans, val);
            ret.clear();
            for (int i = 0; i < road.size(); i++)
                ret.push_back(road[i]);
        }
    }
    for (int i = 0; i < front[cur].size(); i++)
    {
        int nxt = front[cur][i];
        road.push_back(nxt);
        dfs(nxt, val + g[cur][nxt]);
        road.pop_back();
    }
}

int main()
{
    cin >> n >> m;
    cin >> s >> t;
    for (int i = 1; i <= m; i++)
    {
        int u, v, w, cost;
        cin >> u >> v >> w >> cost;
        g[u][v] = cost;
        g[v][u] = cost;
        e[u].push_back({v, w});
        e[v].push_back({u, w});
    }
    dij(s);
    dfs(t, 0);
    for (int i = ret.size() - 1; i >= 0; i--)
        cout << ret[i] << " ";
    cout << t << " " << dis[t] << " " << ans << endl;
}

```

