### [High Score](https://cses.fi/problemset/task/1673/)

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <map>
using namespace __gnu_pbds;
using namespace std;
#define tezi           ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define ordered_set    tree<int, null_type,less<int>, rb_tree_tag,tree_order_statistics_node_update>
#define int            long long
#define fo(i,n)        for(int i=0;i<n;i++)
#define fo1(i, n)      for (int i = 1; i < n; i++)
#define endl           "\n"
#define MAX(a,b)       (a>b) ? a : b
#define MIN(a,b)       (a>b) ? b : a
#define fi             first
#define se             second
#define pb             push_back
#define mp             make_pair
#define all(v)         v.begin(), v.end()
#define sz(v)          v.size()
#define pii            pair<int, int>

int n,  m, y, e, t, k, q, u1, u2,  w, v, d;
const int mx = 300005, mod = 1000000007, mx2 = 1000005 , mx3 = 100005, INF = 10000000000000000;
struct Edge {
    int src, dest, weight;
};
vector<int> cycle_wale_vertices;
vector<int> visited(3000, 0);
vector<int> adj[3000];

void dfs(int v) {
    visited[v] = 1;
    for (auto it : adj[v]) {
        if (visited[it] == 0) dfs(it);
    }
    return;
}

void bellman_ford(Edge* edges) {
    vector<int> dist(n + 1, INF);
    dist[1] = 0;
    fo(i, n - 1) {
        fo(j, m) {
            int u = edges[j].src, v = edges[j].dest, w = edges[j].weight;
            if ((dist[v] > (dist[u] + w)) && (dist[u] < INF)) {
                dist[v] = (dist[u] + w);
            }
        }
    }
    bool any_change = false;
    fo(i, m) {
        int u = edges[i].src, v = edges[i].dest, w = edges[i].weight;
        if ((dist[v] > (dist[u] + w)) && (dist[u] < INF)) {
            any_change = true;
            if (dist[v] > (dist[u] + w)) {
                cycle_wale_vertices.pb(u);
            }
            dist[v] = (dist[u] + w);
        }
    }
    if (any_change) {
        for (auto it : cycle_wale_vertices) {
            visited.clear();
            dfs(it);
            if (visited[1] || visited[n]) {cout << -1 << endl; return;}
        }
    }
    cout << -1 * dist[n] << endl;
    return;
}

signed main()
{   tezi
# ifndef ONLINE_JUDGE
    // for getting input from input.txt
    freopen("input.txt", "r", stdin);
    // for getting input from output.txt
    freopen("output.txt", "w", stdout);
# endif
    cin >> n >> m;
    Edge* edges = new Edge[m];
    fo(i, m) {
        cin >> u1 >> u2 >> w;
        edges[i].src = u1;
        edges[i].dest = u2;
        edges[i].weight = -1 * w;
        adj[u1].pb(u2);
    }
    bellman_ford(edges);
    return 0;
}
/*
    #######
   #
  #
 #######   #     #  # ####   # #     #
       #  # #   #  # #   #  # # #   #
      #  ####  #  # ####   ####  # #
######  #   # #### #    # #   #   #
*/
```
