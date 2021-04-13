### [Flight Discount](https://cses.fi/problemset/task/1195/)

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

int n,  m, y, e, t, k, len, u1, u2,  w, v, d;
const int mx = 300005, mod = 1000000007, mx2 = 1000005 , mx3 = 200005, INF = 1e15;
vector<array<int, 3>> edges(mx3, { -1, -1, -1});

void dijkstra(int source, vector<int> &dist, vector<pii> adj[]) {
    set<pair<int, int>> q;
    q.insert({0, source});
    dist[source] = 0;
    while (!q.empty()) {
        u1 = q.begin()->se;
        q.erase(q.begin());
        for (auto it : adj[u1]) {
            u2 = it.fi;
            w = it.se;
            if (dist[u2] > (dist[u1] + w)) {
                q.erase({dist[u2], u2});
                dist[u2] = (dist[u1] + w);
                q.insert({dist[u2], u2});
            }
        }
    }
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
    vector<pii> adj[mx3];
    vector<pii> adjR[mx3];
    fo(i, m) {
        cin >> u1 >> u2 >> w;
        edges[i] = {u1, u2, w};
        adj[u1].pb({u2, w});
        adjR[u2].pb({u1, w});
    }
    vector<int> dist1(mx3, INF);
    vector<int> distn(mx3, INF);
    dijkstra(1, dist1, adj);
    dijkstra(n, distn, adjR);
    int ans = INF;
    fo(i, m) {
        int src = edges[i][0], dest = edges[i][1], w = edges[i][2];
        ans = min(ans, dist1[src] + distn[dest] + w / 2);
    }
    cout << ans << endl;
    return 0;
}
/*
    #######
   #
  #
 #######   #     #  # ####   # #     #
       #  # #   #  # #   #  # # #   #
      #  ####  #  # ####   ####  # #
######  #   # #### #    # #   #   #w
*/
```
