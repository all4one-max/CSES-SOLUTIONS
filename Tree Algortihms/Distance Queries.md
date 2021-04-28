### [Distance Queries](https://cses.fi/problemset/task/1135/)

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
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> adj[mx2];
vector<vector<int>> dp(mx2, vector<int>(21, -1));
vector<int> depth(mx2, 0);

void binary_lift(int v, int p) {
    dp[v][0] = p;
    fo1(i, 21) {
        if (dp[v][i - 1] != -1) {
            dp[v][i] = dp[dp[v][i - 1]][i - 1];
        }
        else dp[v][i] = -1;
    }
    for (auto it : adj[v]) {
        if (it != p) {
            depth[it] = depth[v] + 1;
            binary_lift(it, v);
        }
    }
    return;
}

int lift(int v, int k) {
    int i = 0;
    while (k) {
        if (k & 1) {
            v = dp[v][i];
        }
        k = k >> 1;
        i++;
    }
    return v;
}

int LCA(int u1, int u2) {
    if (depth[u1] > depth[u2]) swap(u1, u2);
    u2 = lift(u2, depth[u2] - depth[u1]);
    if (u1 == u2) return u1;
    for (int i = 20; i >= 0; i--) {
        if (dp[u1][i] != dp[u2][i]) {
            u1 = dp[u1][i];
            u2 = dp[u2][i];
        }
    }
    return lift(u1, 1);
}

void solve() {
    cin >> n >> q;
    fo(i, n - 1) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adj[u2].pb(u1);
    }
    binary_lift(1, -1);
    fo(i, q) {
        cin >> u1 >> u2;
        int lca = LCA(u1, u2);
        int ans = depth[u1] + depth[u2] - 2 * depth[lca];
        cout << ans << endl;
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
