[1130 Infix Expression - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805347921805312&page=1)



```
dfs输出即可
```



```
#include <bits/stdc++.h>
using namespace std;
struct node
{
    int l, r;
};
node v[25];
string c[25];
int in[25];
int root = 0;
void dfs(int cur)
{
    if (cur == -1)
        return;
    int l = v[cur].l, r = v[cur].r;
    if (cur == root)
    {
        dfs(l);
        cout << c[cur];
        dfs(r);
    }
    else
    {
        if (l != -1 or r != -1)
        {
            cout << "(";
            dfs(l);
            cout << c[cur];
            dfs(r);
            cout << ")";
        }
        else if (l == -1 and r == -1)
        {
            cout << c[cur];
            ;
        }
    }
}
int main()
{
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        string chr;
        cin >> chr;
        c[i] = chr;
        int l, r;
        cin >> l >> r;
        v[i].l = l, v[i].r = r;
        in[l]++;
        in[r]++;
    }
    //找根
    for (int i = 1; i <= n; i++)
        if (in[i] == 0)
            root = i;
    //dfs输出
    dfs(root);
}

```

