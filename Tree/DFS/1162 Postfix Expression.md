[1162 Postfix Expression - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=1478635599577522176&page=1)



```
和1130没什么区别 后序输出即可
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

    if (l == -1 and r != -1) // 只有右节点
    {
        cout << "(";
        cout << c[cur];
        dfs(l);
        dfs(r);

        cout << ")";
    }
    else if (l != -1 and r == -1) // 只有左
    {
        cout << "(";
        cout << c[cur];
        dfs(l);
        dfs(r);
        cout << ")";
    }
    else if (l != -1 and r != -1)
    {
        cout << "(";
        dfs(l);
        dfs(r);
        cout << c[cur];
        cout << ")";
    }
    else if (l == -1 and r == -1)
    {
        cout << "(";
        cout << c[cur];
        cout << ")";
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
    // 找根
    for (int i = 1; i <= n; i++)
        if (in[i] == 0)
            root = i;
    // dfs输出
    dfs(root);
    cout << endl;
}

```

