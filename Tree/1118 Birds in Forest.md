

[[1118 Birds in Forest - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805354108403712&page=1)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805361586847744&page=1)



```
merge后查询即可
```



```
#include <bits/stdc++.h>
using namespace std;
int fa[10005];
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

int root = 0;
vector<int> nums;
bool cmp(int a, int b)
{
    return a > b;
}
int main()
{
    int n;
    cin >> n;
    for (int i = 1; i <= 10000; i++)
        fa[i] = i;
    for (int i = 0; i < n; i++)
    {
        int k;
        cin >> k;
        if (k == 1)
        {
            int num;
            cin >> num;
            nums.push_back(num);
        }
        else
        {
            cin >> root;
            nums.push_back(root);
            for (int i = 1; i < k; i++)
            {
                int num;
                cin >> num;
                nums.push_back(num);
                merge(root, num);
            }
        }
    }
    int q;
    cin >> q;
    sort(nums.begin(), nums.end(), cmp);

    map<int, int> mp;
    for (auto i : nums)
    {
        mp[find(i)]++;
    }
    cout << mp.size() << " ";
    cout << nums[0]<< endl;
    while (q--)
    {
        int a, b;
        cin >> a >> b;

        if (find(a) == find(b))
            cout << "Yes\n";
        else
            cout << "No\n";
    }
}
```

