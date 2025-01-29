[1087 All Roads Lead to Rome - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805379664297984&page=0)



```
6个城市 7条路径 求起点到ROM最短路径条件下的最大平均happiness值
输入给定除去起点外5个城市的happiness值分别为[100,40,55,95,80]
以及7条无向路径的长度
先用dijkstra求出最短路径条件下的front数组
再对front跑dfs求最大happiness
//和1003非常相似
```



```
#include <bits/stdc++.h>
using namespace std;
int n, m;
const int MAXN = 205;
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
int ans = 0;
int ans1 = 0;
int cnt = 0;
vector<int> vecc;
vector<int> ret;
void dfs(int cur, int val, int len)
{
    if (cur == s)
        cnt++;
    if (val > ans)
    {
        ans = val;
        ans1 = val / len;
        ret.clear();
        // cout<<1<<vecc.size()<<endl;
        for (int i = 0; i < vecc.size(); i++)
        {
            ret.push_back(vecc[i]);
        }
    }
    for (int i = 0; i < front[cur].size(); i++)
    {
        int nxt = front[cur][i];
        vecc.push_back(nxt);
        dfs(nxt, val + value[nxt], len + 1);
        vecc.pop_back();
    }
}

int main()
{
    cin >> n >> m;
    string start_city;
    cin >> start_city;
    map<string, int> m1;
    map<int, string> m2;
    m1[start_city] = 0;
    m2[0] = start_city;
    for (int i = 1; i < n; i++)
    {
        string s;
        cin >> s;
        m1[s] = i;
        m2[i] = s;
        cin >> value[i];
    }
    for (int i = 1; i <= m; i++)
    {
        string city1, city2;
        cin >> city1 >> city2;
        int u, v, w;
        u = m1[city1], v = m1[city2];
        cin >> w;
        e[u].push_back({v, w});
        e[v].push_back({u, w}); // 无向图
    }
    s = m1[start_city];
    dij(s);
    t = m1["ROM"];
    vecc.push_back(t);
    dfs(t, value[t], 1);
    cout << cnt << " " << dis[t] << " " << ans << " " << ans1 << endl;
    // cout<<start_city;
    for (int i = ret.size(); i >= 0; i--)
    {
        cout << m2[ret[i]];
        if (i != 0)
            cout << "->";
    }
}
// dfs找最大值

```

