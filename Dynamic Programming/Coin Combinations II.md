### [Coin Combinations II](https://cses.fi/problemset/task/1636)

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <map>
using namespace __gnu_pbds;
using namespace std;
#define tezi           ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define ordered_set    tree<int, null_type,less<int>, rb_tree_tag,tree_order_statistics_node_update>
//#define int            long long
#define fo(i,n)        for(int i=0;i<n;i++)
#define fo1(i, n)      for (int i = 1; i < n; i++)
#define endl           "\n"
#define MAX(a,b)       (a>b) ? a : b
#define MIN(a,b)       (a>b) ? b : a
#define fi             first
#define se             second
#define pb             push_back
#define mp             make_pair

int n, x, m, y, e, t, k, len, u1, u2,  f;
const int mx = 200005, mod = 1000000007, mx2 = 1000005 ;
signed main()
{ tezi
  /*# ifndef ONLINE_JUDGE
    // for getting input from input.txt
    freopen("input.txt", "r", stdin);
    // for getting input from output.txt
    freopen("output.txt", "w", stdout);
  # endif*/
  cin >> n >> x;
  vector<int> c(n, 0);
  fo(i, n) cin >> c[i];
  //sort(c.begin(), c.end());
  vector<vector<int>> dp(n, vector<int> (x + 1, 0));
  fo(j, x + 1) {
    if (j == c[0]) dp[0][j]++;
    if ((j - c[0]) >= 0) dp[0][j] += dp[0][j - c[0]];
    dp[0][j] %= mod;
  }
  fo1(i, n) {
    fo(j, x + 1) {
      if (j == c[i]) {
        dp[i][j]++;
      }
      dp[i][j] += dp[i - 1][j];
      if ((j - c[i]) >= 0) {
        dp[i][j] += (dp[i][j - c[i]]);
      }
      dp[i][j] %= mod;
    }
  }
  /*fo(i, n) {
    fo(j, x + 1) {
      cout << dp[i][j] << " ";
    }
    cout << endl;
  }*/
  cout << dp[n - 1][x] << endl;
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
