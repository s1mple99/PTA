[1053 Path of Equal Weight - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805424153280512&page=0)



```
输出和为S的根到叶的路径
```



```
#include <bits/stdc++.h>
using namespace std;

vector<int> v[105];
int value[105];
int n, m, s;
vector<int> sum_;
vector<vector<int>> ans;
void dfs(int cur, int sum)
{
    if (sum == s and v[cur].size() == 0)
    {
        ans.push_back(sum_);
        // for(auto i:sum_)cout<<i<<" ";
        // cout<<endl;
        return;
    }
    // if(v[cur].size()==0) return;
    for (int i = 0; i < v[cur].size(); i++)
    {
        int nxt = v[cur][i];
        sum_.push_back(value[nxt]);
        dfs(nxt, sum + value[nxt]);
        sum_.pop_back();
    }
}
bool cmp(vector<int> &a, vector<int> &b)
{
    int minLen = min(a.size(), b.size());
    for (int i = 0; i < minLen; ++i)
    {
        if (a[i] != b[i])
        {
            return a[i] > b[i];
        }
    }
    return a.size() < b.size();
}
int main()
{
    cin >> n >> m >> s;
    for (int i = 0; i < n; i++)
        cin >> value[i];
    for (int i = 0; i < m; i++)
    {
        string s;
        cin >> s;
        int num = stoi(s);
        int u;
        cin >> u;
        while (u--)
        {
            string s;
            cin >> s;
            int nxt = stoi(s);
            v[num].push_back(nxt);
        }
    }
    sum_.push_back(value[0]);
    dfs(0, value[0]);
    sort(ans.begin(), ans.end(), cmp);
    for (int i = 0; i < ans.size(); i++)
    {
        for (int j = 0; j < ans[i].size(); j++)
        {
            if (j)
                cout << " ";
            cout << ans[i][j];
        }
        cout << endl;
    }
}
```

