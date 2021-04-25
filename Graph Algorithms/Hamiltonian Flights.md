### [Hamiltonian Flights](https://cses.fi/problemset/task/1690)

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
vector<vector<int>> adj(25, vector<int> (25, 0));
vector<vector<int>> dp(20, vector<int>(mx3, -1));

int op_tsp(int pos, int mask) {
    if (pos == n - 1 && mask == (1 << n) - 1) {
        return 1;
    }
    if (pos == n - 1) return 0;
    if (dp[pos][mask] != -1) return dp[pos][mask];
    int ans = 0;
    fo(i, n) {
        if ((mask & (1 << i)) == 0) {
            if (adj[pos][i]) {
                ans += adj[pos][i] * op_tsp(i, mask | (1 << i));
                ans %= mod;
            }
        }
    }
    return dp[pos][mask] = ans;
}

void solve() {
    cin >> n >> m;
    fo(i, m) {
        cin >> u1 >> u2;
        u1--; u2--;
        adj[u1][u2]++;
    }
    int ans = op_tsp(0, 1) % mod;
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
