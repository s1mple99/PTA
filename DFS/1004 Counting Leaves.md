[1004 Counting Leaves - PAT (Advanced Level) Practice](https://pintia.cn/problem-sets/994805342720868352/exam/problems/type/7?problemSetProblemId=994805521431773184&page=0)



```
数每层叶子节点的个数
```



```
#include<bits/stdc++.h>
using namespace std;
map<string,int> mp;
vector<int> v[105];
int ret[105];
int maxdep = -1;
void dfs(int root,int dep){
    maxdep = max(dep,maxdep);
    if(v[root].size()==0) {ret[dep]++;return;}
    for(int i=0;i<v[root].size();i++){
        int nxt = v[root][i];
        //cout<<nxt<<endl;
        dfs(nxt,dep+1);
    }
}

int main(){
    int n,m;cin>>n>>m;
    int node = -1;
    int cnt= 1;
    for(int i=0;i<m;i++){
        string id;cin>>id;
        if(id=="01" and node==-1){
            node = cnt;
        }
        if(mp[id]==0) 
        {
            mp[id]=cnt;
            //rmp[cnt] = id;
         cnt++;
        }
        int k;cin>>k;
        while(k--){
            string tmp;
            cin>>tmp;
            if(mp[tmp]==0) 
            {
                mp[tmp]=cnt;
                //rmp[cnt] = tmp;
                cnt++;
            }
            v[mp[id]].push_back(mp[tmp]);
        }
    }
    dfs(node,0);
    for(int i=0;i<=maxdep;i++){
        if(i!=0) cout<<" ";
        cout<<ret[i];
    }
}



/*
dfs
数每层的叶子节点个数
*/
```

