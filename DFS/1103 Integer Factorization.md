[1103 Integer Factorization - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805364711604224&page=1)



```
回溯输出结果即可
```



```
#include <bits/stdc++.h>
using namespace std;
int n, k, p;
vector<int> ret;
vector<vector<int>> ans;
void go(int target, int cur)
{
    if (target == 0 and ret.size() == k)
    {
        ans.push_back(ret);
    }
    else if (target < 0 or ret.size() >= k)
    {
        return;
    }
    for (int i = cur; i >= 1; i--)
    {
        ret.push_back(i);
        go(target - pow(i, p), i);
        ret.pop_back();
    }
}
int main()
{
    cin >> n >> k >> p;
    int num = 1;
    for (int i = 1; i <= n; i++)
    {
        if (pow(i, p) <= n)
        {
            num = i;
        }
        else
        {
            break;
        }
    }
    go(n, num);
    if (ans.size() == 0)
        cout << "Impossible";
    else
    {
        int flg = 0;
        int maxxsum = 0;
        for (int i = 0; i < ans.size(); i++)
        {
            vector<int> tmp = ans[i];
            int sum = 0;
            for (int j = 0; j < tmp.size(); j++)
            {
                sum += tmp[j];
            }
            if (maxxsum < sum)
            {
                maxxsum = sum;
                flg = i;
            }
        }
        cout << n << " = ";
        for (int i = 0; i < ans[flg].size(); i++)
        {
            if (i != 0)
                cout << " + ";
            cout << ans[flg][i] << "^" << p;
        }
    }
}
```

