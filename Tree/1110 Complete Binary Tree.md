

[1110 Complete Binary Tree - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805359372255232&page=1)



```
层序遍历
定义
	[有左节点，有右节点]的节点为1类节点
	[有左节点，无右节点]的节点为2类节点
	[无左节点，有右节点]的节点为3类节点
	[无左节点，无右节点]的节点为4类节点

非完全二叉树的判定
	1.若存在3类的节点，则此树不是完全二叉树
	2.层序遍历第一次遇到24类节点后，不能后序节点中出现12类节点
```



```
#include <bits/stdc++.h>
using namespace std;
struct node
{
    int l;
    int r;
};
node v[100];
int in[100];

vector<int> ans; // 层序遍历结果
int n;
bool bubaohe = 0; // 不饱和
bool flg = 0;
void level(int root)
{
    queue<int> q;
    q.push(root);
    while (not q.empty())
    {
        int cur = q.front();
        ans.push_back(cur);
        q.pop();
        int l = v[cur].l, r = v[cur].r;
        if (l != -1 and r != -1) // 1类节点
        {
            q.push(l);
            q.push(r);
            if (bubaohe)
                flg = 1;
        }
        else
        {
            if (l != -1 and r == -1) // 2类节点
            {
                q.push(l);
                if (bubaohe)
                    flg = 1;
                bubaohe = 1;
            }
            else if (l == -1 and r != -1) // 3类节点
            {

                q.push(r);
                flg = 1;
            }

            else if (l == -1 and r == -1) // 4类节点
            {
                bubaohe = 1;
            }
        }
    }
}

int main()
{

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        string a, b;
        cin >> a >> b;
        v[i].l = (a == "-") ? -1 : stoi(a);
        v[i].r = (b == "-") ? -1 : stoi(b);
        if (v[i].l != -1)
            in[v[i].l]++;
        if (v[i].r != -1)
            in[v[i].r]++;
    }
    int root = -1;
    for (int i = 0; i < n; i++)
        if (in[i] == 0)
            root = i;
    level(root);
    if (flg)
    {
        cout << "NO " << root;
    }
    else
    {
        cout << "YES " << ans.back();
    }
}

```

