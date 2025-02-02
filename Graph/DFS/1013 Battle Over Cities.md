[1013 Battle Over Cities - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805500414115840&page=0)



```
输出去除某个点后 连通块个数-1 的值
dfs染色即可
```



```
#include <bits/stdc++.h>
using namespace std;
vector<int> v[1005];
int color[1005];
int vis[1005];

void dfs(int cur, int occ, int col)
{
    if (cur == occ)
        return;
    vis[cur] = 1;
    color[cur] = col;
    for (int i = 0; i < v[cur].size(); i++)
    {
        int nxt = v[cur][i];
        if (not vis[nxt])
            dfs(nxt, occ, col);
    }
}
int main()
{
    int n, m, k;
    cin >> n >> m >> k;
    while (m--)
    {
        int x, y;
        cin >> x >> y;
        v[x].push_back(y);
        v[y].push_back(x);
    }
    while (k--)
    {
        int occ;
        cin >> occ;
        map<int,int> mp;
        for (int i = 1; i <= n; i++)
        {
            color[i] = i;
            vis[i] = 0;
        } // 初始化
        for (int i = 1; i <= n; i++)
        {
            if (not vis[i])
                dfs(i, occ, i);
        }
        for (int i = 1; i <= n; i++)
        {
            if(i!=occ) 
            mp[color[i]]++;
        }
        cout<<mp.size()-1<<endl;
    }
}
```

