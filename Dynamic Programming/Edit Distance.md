### [Edit Distance](https://cses.fi/problemset/task/1639)

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

bool comp(int a, int b)
{
  return (a < b);
}

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
  string a, b;
  cin >> a >> b;
  u1 = a.length(), u2 = b.length();
  vector<vector<int>> dp(u1 + 1, vector<int> (u2 + 1, 1e9));
  dp[0][0] = 0;
  fo(i, u1 + 1) {
    fo(j, u2 + 1) {
      if (i) dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);
      if (j) dp[i][j] = min(dp[i][j], dp[i][j - 1] + 1);
      if (i && j) dp[i][j] = min(dp[i][j], dp[i - 1][j - 1] + (a[i - 1] != b[j - 1]));
    }
  }
  cout << dp[u1][u2];

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
