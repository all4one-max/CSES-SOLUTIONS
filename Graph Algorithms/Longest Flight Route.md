### [Longest Flight Route](https://cses.fi/problemset/task/1680)

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
vector<int> adj[mx2];
vector<int> visited(mx2, 0);
vector<int> nodes(mx2, 0);
vector<int> children(mx2, 0);

void dfs(int v, int p) {
    visited[v] = 1;
    if (v == n) {
        nodes[v] = 1;
        return;
    }
    for (auto it : adj[v]) {
        if (visited[it] == 0) {
            dfs(it, v);
            if (nodes[it]) {
                if (nodes[it] + 1 > nodes[v]) {
                    nodes[v] = nodes[it] + 1;
                    children[v] = it;
                }
            }
        }
        else {
            if (nodes[it]) {
                if (nodes[it] + 1 > nodes[v]) {
                    nodes[v] = nodes[it] + 1;
                    children[v] = it;
                }
            }
        }
    }
    return;
}

void solve() {
    cin >> n >> m;
    fo(i, m) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
    }
    dfs(1, -1);
    if (nodes[1]) {
        vector<int> ans = {1};
        int v = children[1];
        while (v != n) {
            ans.pb(v);
            v = children[v];
        }
        ans.pb(n);
        cout << sz(ans) << endl;
        for (auto it : ans) cout << it << " "; cout << endl;
    }
    else cout << "IMPOSSIBLE" << endl;
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
