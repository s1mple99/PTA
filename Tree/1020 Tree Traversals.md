[1020 Tree Traversals - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805485033603072&page=0)



```
分治build树
层序输出即可
```



```
#include <bits/stdc++.h>
using namespace std;

int n;
vector<int> post;
vector<int> in;
int mp1[35];
int mp2[35];
vector<int> ret[35];
void build(int l, int r) // 队列1的左和右
{
    if (l == r)
    {
        // cout<<post[l];
        return;
    }
    else if (l < r)
    {
        int num = post[r];
        int index = mp2[num]; // 在队列2种的位置
        int flg_l = 0, ll = -1;
        int flg_r = 0;
        for (int i = l; i <= r; i++)
        {
            int num = post[i];
            if (mp2[num] < index) // 存在左子树
            {
                flg_l = 1;
                ll = max(ll, mp1[num]);
            }
            else if (mp2[num] > index)
                flg_r = 1; // 存在右子树
        }
        if (flg_l and flg_r)
        {
            ret[num].push_back(post[ll]);
            ret[num].push_back(post[r - 1]);
            build(l, ll);
            build(ll + 1, r - 1);
        }
        else
        {
            ret[num].push_back(post[r - 1]);
            build(l, r - 1);
        }
    }
}

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        int num;
        cin >> num;
        post.push_back(num);
        mp1[num] = i;
    }
    for (int i = 0; i < n; i++)
    {
        int num;
        cin >> num;
        in.push_back(num);
        mp2[num] = i;
    }
    build(0, n - 1);
    int root = post[n - 1];
    vector<int> v;
    queue<int> q;
    q.push(root);
    while (!q.empty())
    {
        int num = q.front();
        q.pop();
        v.push_back(num);
        for (int i = 0; i < ret[num].size(); i++)
            q.push(ret[num][i]);
    }
    for (int i = 0; i < v.size(); i++)
    {
        if (i != 0)
            cout << " ";
        cout << v[i];
    }
}
```

