### [Forest Queries](https://cses.fi/problemset/task/1652/)

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

int n,  m, y, e, t, q, u1, u2,  w, v, c, d, x, k;
const int mx = 800005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;

void solve() {
    char c;
    cin >> n >> q;
    vector<vector<int>> tree(n + 1, vector<int> (n + 1, 0));
    vector<vector<int>> dp(n + 1, vector<int> (n + 1, 0));
    fo1(i, n + 1) {
        fo1(j, n + 1) {
            cin >> c;
            tree[i][j] = (1 ? (c == '*') : 0);
        }
    }
    fo1(i, n + 1) {
        fo1(j, n + 1) {
            dp[i][j] = dp[i][j - 1] + dp[i - 1][j] - dp[i - 1][j - 1] + tree[i][j];
        }
    }
    fo(i, q) {
        cin >> x >> y >> u1 >> u2;
        int ans = dp[u1][u2] - dp[x - 1][u2] - dp[u1][y - 1] + dp[x - 1][y - 1];
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
