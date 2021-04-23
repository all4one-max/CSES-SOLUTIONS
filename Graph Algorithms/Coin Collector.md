### [Coin Collector](https://cses.fi/problemset/task/1686/)

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

int n,  m, y, e, t, q, u1, u2,  w, v, c, d, x;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 100005, INF = 1000000000000000000;
vector<int> adj[mx2];
vector<int> adjT[mx2];
vector<int> scc[mx2];
vector<int> visited(mx2, 0);
vector<int> money_comp(mx2, 0);
vector<int> scc_comp_head(mx2, 0);
vector<int> dp(mx2, 0);
vector<int> order;
vector<int> k(mx2, 0);

void dfs1(int v) {
    visited[v] = 1;
    for (auto it : adj[v]) {
        if (!visited[it]) dfs1(it);
    }
    order.pb(v);
    return;
}

void dfs2(int v, int num_comp) {
    visited[v] = 1;
    scc_comp_head[v] = num_comp;
    money_comp[num_comp] += k[v];
    for (auto it : adjT[v]) {
        if (!visited[it]) dfs2(it, num_comp);
    }
    return;
}

int get_money(int v) {
    visited[v] = 1;
    dp[v] += money_comp[v];
    // you can't go to all the components with the current component, you can only go to one
    // and once you do you won't be able to return from that component so thats why we will take
    // the maximum from all the components connected with the current one
    int res = 0;
    for (auto it : scc[v]) {
        if (!visited[it]) res = max(res, get_money(it));
        else res = max(res, dp[it]);
    }
    dp[v] += res;
    return dp[v];
}

void solve() {
    cin >> n >> m;
    fo1(i, n + 1) cin >> k[i];
    fo(i, m) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adjT[u2].pb(u1);
    }
    fo1(i, n + 1) {
        if (!visited[i]) dfs1(i);
    }
    reverse(all(order));
    fo(i, n + 1) visited[i] = 0;
    int num_comp = 0;
    for (auto v : order) {
        if (!visited[v]) {
            num_comp++;
            dfs2(v, num_comp);
        }
    }
    fo1(i, n + 1) {
        for (auto it : adj[i]) {
            if (scc_comp_head[i] != scc_comp_head[it]) scc[scc_comp_head[i]].pb(scc_comp_head[it]);
        }
    }
    fo(i, n + 1) visited[i] = 0;
    int ans = 0;
    fo1(i, num_comp + 1) {
        if (!visited[i]) {
            ans = max(ans, get_money(i));
        }
    }
    cout << ans << endl;
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
