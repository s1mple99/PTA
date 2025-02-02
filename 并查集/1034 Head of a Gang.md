[1034 Head of a Gang - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805456881434624&page=0)

```
输入8行 以及 判定值k
每行输入x y time
对于x、y作merge操作，合并两个集合中times较大者作根
输出符合条件(集合成员数>2,集合总时间>k)的集合
```



```
#include <bits/stdc++.h>
using namespace std;
const int maxn = 2005;
int times[maxn];
int fa[maxn];
int group_times[maxn];
int group_cnts[maxn];

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

void merge(int x, int y, int val)
{
    int rx = find(x);
    int ry = find(y);
    if (rx == ry)
    {
        group_times[rx] += val;
    }
    else
    {
        if (times[rx] < times[ry])
        {
            swap(rx, ry);
        }

        fa[ry] = rx; // rx//作根
        group_times[rx] += group_times[ry] + val;
        group_cnts[rx] += group_cnts[ry];
    }
}
struct st
{
    int u, v, cost;
};
vector<st> vec;
struct st1
{
    string name;
    int cost;
};
bool cmp(st1 a, st1 b)
{
    return a.name < b.name;
}
int main()
{
    int n, k;
    cin >> n >> k;
    map<string, int> m1;
    map<int, string> m2;
    int cnt = 1;
    for (int i = 1; i <= n; i++)
    {
        int time;
        string x, y;
        cin >> x >> y >> time;
        if (m1[x] == 0)
        {
            m1[x] = cnt;
            m2[cnt] = x;
            cnt++;
        }
        if (m1[y] == 0)
        {
            m1[y] = cnt;
            m2[cnt] = y;
            cnt++;
        }
        int u = m1[x], v = m1[y];
        vec.push_back({u, v, time});
        times[u] += time;
        times[v] += time;
    }
    for (int i = 1; i <= cnt; i++)
    {
        fa[i] = i;
        group_cnts[i] = 1;
    }

    for (int i = 0; i < vec.size(); i++)
    {
        merge(vec[i].u, vec[i].v, vec[i].cost);
    }
    cnt = 0;
    vector<st1> ans;
    for (int i = 1; i <= n; i++)
    {
        if (group_cnts[i] > 2 and group_times[i] > k and find(i)==i)
        {
            ans.push_back({m2[i], group_cnts[i]});
        }
    }
    sort(ans.begin(), ans.end(), cmp);
    cout << ans.size() << endl;
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i].name << " " << ans[i].cost << endl;
}

```

