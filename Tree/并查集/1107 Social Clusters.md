

[1107 Social Clusters - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805361586847744&page=1)



```
根据hobby合并即可
```



```
#include <bits/stdc++.h>
using namespace std;
int fa[1005]; 
int group[1005];
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
}
vector<int> v[1005];
bool cmp(int a, int b)
{
    return a > b;
}
int main()
{
    int n;
    cin >> n;
    for (int i = 1; i <= 1000; i++)
        fa[i] = -1;
    
    for (int i = 1; i <= n; i++)
    {
        int k;
        cin >> k;
        char c;
        cin >> c;
        for (int j = 0; j < k; j++)
        {
            int num;
            cin >> num;
            if (fa[num] == -1)
                fa[num] = num;
            v[i].push_back(num);
        }

        if (v[i].size() == 1)
        {
            continue;
        }
        else
        {
            for (int j = 1; j < v[i].size(); j++)
                merge(v[i][0], v[i][j]);
        }
    }
    for (int i = 1; i <= n; i++)
    {
        group[find(v[i][0])]++;
    }
    vector<int> ans;
    for (int i = 1; i <= 1000; i++)
        if (group[i] != 0)
            ans.push_back(group[i]);
    sort(ans.begin(), ans.end(), cmp);
    cout << ans.size() << endl;
    for (int i = 0; i < ans.size(); i++)
    {
        if (i)
            cout << " ";
        cout << ans[i];
    }
}
```

