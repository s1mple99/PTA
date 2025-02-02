[1099 Build A Binary Search Tree - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805367987355648&page=0)



```
中序建树
层序输出
```



```
#include <bits/stdc++.h>
using namespace std;
struct node
{
    int num;
    int l;
    int r;
};
node v[105];
vector<int> nums;
int cnt = 0;
void midorder(int cur)
{
    if (cur == -1)
        return;
    midorder(v[cur].l);
    v[cur].num = nums[cnt++];
    midorder(v[cur].r);
}

int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        int l, r;
        cin >> l >> r;
        v[i].l = l;
        v[i].r = r;
    }
    for (int i = 0; i < n; i++)
    {
        int num;
        cin >> num;
        nums.push_back(num);
    }
    sort(nums.begin(), nums.end());
    //中序建树
    midorder(0);
    //层序输出
    queue<int> q;
    q.push(0);
    int t = 0;
    while (!empty(q))
    {
        int tp = q.front();
        q.pop();
        if (t)
        {
            cout << " ";
        }
        cout << v[tp].num;
        t++;
        if (v[tp].l != -1)
            q.push(v[tp].l);
        if (v[tp].r != -1)
            q.push(v[tp].r);
    }
}
```

