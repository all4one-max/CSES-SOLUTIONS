### [Rectangle Cutting](https://cses.fi/problemset/task/1744)

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

int n, x, m, y, e, t, k, len, u1, u2,  f, a, b;
//const int mx = 200005, mod = 1000000007, mx2 = 1000005 ;
signed main()
{ tezi
  /*# ifndef ONLINE_JUDGE
    // for getting input from input.txt
    freopen("input.txt", "r", stdin);
    // for getting input from output.txt
    freopen("output.txt", "w", stdout);
  # endif*/
  cin >> a >> b;
  x = max(a, b);
  vector<vector<int>> dp(x + 1, vector<int> (x + 1, 1e9));
  fo(i, x + 1) dp[i][i] = 0;
  fo1(i, x + 1) {
    fo1(j, x + 1) {
      if (i != j) {
        fo1(k, i) dp[i][j] = min(dp[i][j], dp[i - k][j] + dp[k][j] + 1);
        fo1(k, j) dp[i][j] = min(dp[i][j], dp[i][k] + dp[i][j - k] + 1);
      }
    }
  }
  cout << dp[a][b];
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
