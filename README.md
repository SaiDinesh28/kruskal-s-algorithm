//# kruskal-s-algorithm
#include<bits/stdc++.h>
using namespace std;
struct node{
    int u;
    int v;
    int wt;
    node(int f,int s,int x){
        u=f;
        v=s;
        wt=x;
    }
};
bool comp(node a,node b){
   return a.wt<b.wt;
}
int findpar(int x,vector<int>&parent){
    if(parent[x]==x) return x;
    return parent[x]=findpar(parent[x],parent);
}
void runion(int a,int b,vector<int>&parent,vector<int>&rank){
     a=findpar(a,parent);
     b=findpar(b,parent);
    if(rank[a]<rank[b]){
        parent[a]=b;

    }
    else if(rank[b]<rank[a]){
        parent[b]=a;
    }
    else{
        parent[a]=b;
        rank[b]++;
    }
}
int main(){
    int t;
    cin>>t;
    while(t--){
        int n,m;
        cin>>n>>m;
        vector<node>v;
        for(int i=0;i<m;i++){
            int a,b,c;
            cin>>a>>b>>c;
            v.push_back(node(a,b,c));
        
        }
        sort(v.begin(),v.end(),comp);
        
        vector<int>rank(n);
        vector<int>parent(n);
        for(int i=0;i<n;i++){
            parent[i]=i;
            rank[i]=0;
        }
        
        vector<pair<int,int>> ans;
        
        int cost=0;
        for(auto it:v){
            if(findpar(it.u,parent)!=findpar(it.v,parent)){
                ans.push_back({it.u,it.v});
                cost+=(it.wt);
                runion(it.u,it.v,parent,rank);
            }
        }
         cout<<cost<<endl;
        for(auto it: ans) cout<<it.first<<"->"<<it.second<<endl;
    }
}
