[1114 Family Property - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805356599820288&page=1)

```
以id小的作根作merge操作 
用vector存储每个集合的根，然后作sort操作
输出每个集合的元素数量 平均sets 平均area
```



```
#include <bits/stdc++.h>
using namespace std;
const int maxn = 10005;
int fa[maxn];

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
map<string, int> idtonum;
map<int, string> numtoid;

void merge(int x, int y)
{
    int rx = find(x);
    int ry = find(y);
    if(numtoid[ry]>numtoid[rx]) swap(rx,ry);
    fa[rx] = ry;
    
}
int  contt[maxn];
int es[maxn];
int area[maxn];

struct st{
    string id;
    int cnt;
    double es;
    double area;
};
bool cmp(st a,st b){
    if(a.area!=b.area){
        return a.area> b.area;
    }
    else{
        return a.id<b.id;
    }
}
int main()
{
    int n;
    cin >> n;
    int cnt = 1;
    for(int i=1;i<=10000;i++) {fa[i] = i;contt[i]=1;}
    for (int i = 0; i < n; i++)
    {
            string cur;
            cin >> cur;
            if (idtonum[cur])
            {
                ;
            }
            else
            {
                idtonum[cur] = cnt;
                numtoid[cnt] = cur;
                cnt++;
            }
        for (int j = 0; j < 2; j++)
        {
            string id;
            cin >> id;
            if(id=="-1") continue;
            if (idtonum[id])
            {
               ;
            }
            else
            {
                idtonum[id] = cnt;
                numtoid[cnt] = id;
                cnt++;
            }
            merge(idtonum[cur],idtonum[id]);
        }
        int k;
        cin >> k;
        for (int j = 0; j < k; j++)
        {
            string id;
            cin >> id;
            if(id=="-1") continue;
            if (idtonum[id])
            {
                ;
            }
            else
            {
                idtonum[id] = cnt;
                numtoid[cnt] = id;
                cnt++;
            }
             merge(idtonum[cur],idtonum[id]);
        }
        int es_,area_;cin>>es_>>area_;
        es[ idtonum[cur]]+=es_;
        area[ idtonum[cur]]+=area_;
    
    }
    set<int> st1;
    for(int i=1;i<cnt;i++){
        int root = find(i);
        st1.insert(root);
        if(root!=i){
            contt[root]+=contt[i];
            es[root]+=es[i];
            area[root]+=area[i];    
        }
        
    }
    vector<st> v;
    for(auto i:st1){
        v.push_back({numtoid[i],contt[i],es[i]*1.0/contt[i],area[i]*1.0/contt[i]});
    }
    sort(v.begin(),v.end(),cmp);
    cout<<v.size()<<endl;
    for(int i=0;i<v.size();i++)
        cout<<v[i].id<<" "<<v[i].cnt<<" "
        <<fixed<<setprecision(3)<<v[i].es<<" "
        <<fixed<<setprecision(3)<<v[i].area<<endl;
}
```

