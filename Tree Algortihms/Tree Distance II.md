### [Tree Distance II](https://cses.fi/problemset/task/1133/)

```cpp
// in-out DP on trees
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
vector<int> sums(mx2, 0);
vector<int> num_vertex(mx2, 1);
vector<int> ans(mx2, 0);

void dfs(int v, int p) {
  for (auto it : adj[v]) {
    if (it != p) {
      dfs(it, v);
      sums[v] += (sums[it] + num_vertex[it]);
      num_vertex[v] += num_vertex[it];
    }
  }
  return;
}

void helper(int v, int p, int par_ans) {
  int num_parent_vertex = (n - num_vertex[v]);
  ans[v] = (sums[v] + par_ans + num_parent_vertex);
  int vl = (sums[v] + par_ans + num_parent_vertex), tot_vertex = num_vertex[v];

  for (auto it : adj[v]) {
    if (it != p) {
      vl -= (sums[it] + num_vertex[it]);
      helper(it, v, vl);
      vl += (sums[it] + num_vertex[it]);
    }
  }
  return;
}

void solve() {
  cin >> n;
  fo(i, n - 1) {
    cin >> u1 >> u2;
    adj[u1].pb(u2);
    adj[u2].pb(u1);
  }
  dfs(1, -1);
  helper(1, -1, 0);
  fo1(i, n + 1) cout << ans[i] << " "; cout << endl;
  return;
}

signed main()
{ tezi
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
