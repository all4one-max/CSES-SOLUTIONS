### [Money Sums](https://cses.fi/problemset/task/1745)

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

int n,  m, y, e, t, k, len, u1, u2,  f, sm = 0, cnt = 0;
const int mx = 200005, mod = 1000000007, mx2 = 1000005 ;
signed main()
{ tezi
  /*# ifndef ONLINE_JUDGE
    // for getting input from input.txt
    freopen("input.txt", "r", stdin);
    // for getting input from output.txt
    freopen("output.txt", "w", stdout);
  # endif*/
  cin >> k;
  vector<int> x(k, 0);
  fo(i, k) {cin >> x[i]; sm += x[i];}
  vector<vector<int>> dp(k, vector<int> (sm + 1, 0));
  dp[0][x[0]] = 1;
  fo1(i, k) {
    dp[i][x[i]] = 1;
    fo(j, sm + 1) {
      if (dp[i - 1][j] == 1) dp[i][j] = 1;
      if (((j - x[i]) >= 0) && dp[i - 1][j - x[i]] == 1) {
        dp[i][j] = 1;
      }
    }
  }
  fo(i, sm + 1) {if (dp[k - 1][i] == 1) cnt++;}
  cout << cnt << endl;
  fo(i, sm + 1) {
    if (dp[k - 1][i] == 1) cout << i << " ";
  }


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
