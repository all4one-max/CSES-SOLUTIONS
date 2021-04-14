### [Investigation](https://cses.fi/problemset/result/1982760/)

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <map>
// #include "atcoder/math.hpp"
using namespace __gnu_pbds;
using namespace std;
#define tezi           ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define ordered_set    tree<int, null_type,less<int>, rb_tree_tag,tree_order_statistics_node_update>
#define int            long long
#define fo(i,n)        for (int i=0;i<n;i++)
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

int n,  m, y, e, t, k, q, u1, u2,  w, v, c, d, x, ans = 0;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 100005, INF = 1000000000000000000;
vector<pii> adj[mx2];
vector<int> dist(mx2, INF);
vector<array<int, 2>>  nodes(mx2, {INF, -INF});
vector<int> routes(mx2, 0);

void dijkstra() {
    priority_queue<vector<int>, vector<vector<int>>, greater<vector<int>>> q;
    q.push({0, 1});
    nodes[1][0] = nodes[1][1] = 0;
    routes[1] = 1;
    dist[1] = 0;
    while (!q.empty()) {
        vector<int> v = q.top();
        u1 = v[1];
        int d = v[0];
        q.pop();
        if (d != dist[u1]) continue;

        for (auto it : adj[u1]) {
            u2 = it.fi;
            w = it.se;

            if (dist[u2] > (dist[u1] + w)) {
                nodes[u2][0] = INF; nodes[u2][1] = -INF;
                nodes[u2][0] = min(nodes[u2][0], nodes[u1][0] + 1);
                nodes[u2][1] = max(nodes[u2][1], nodes[u1][1] + 1);
                routes[u2] = routes[u1] % mod;
                dist[u2] = (dist[u1] + w);
                q.push({dist[u2], u2});
            }
            else if (dist[u2] == (dist[u1] + w)) {
                nodes[u2][0] = min(nodes[u2][0], nodes[u1][0] + 1);
                nodes[u2][1] = max(nodes[u2][1], nodes[u1][1] + 1);
                routes[u2] = (routes[u2] + routes[u1]) % mod;
            }
        }
    }
    cout << dist[n] << " " << routes[n] % mod << " " << nodes[n][0] << " " << nodes[n][1] << endl;
    return;
}

void solve() {
    cin >> n >> m;
    fo(i, m) {
        cin >> u1 >> u2 >> w;
        adj[u1].pb({u2, w});
    }
    dijkstra();
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
    t = 1;
    fo(i, t) solve();
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
