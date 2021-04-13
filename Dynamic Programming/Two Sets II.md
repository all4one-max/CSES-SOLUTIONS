### [Two Sets II](https://cses.fi/problemset/task/1093)

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

int n, x, m, y, e, t, k, len, u1, u2,  f;
const int mx = 200005, mod = 1000000007, mx2 = 1000005 ;
vector<int> adj[mx];
vector<int> a(mx, 0);
vector<int> b(mx, 0);

bool comp(int a, int b)
{
    return (a < b);
}

main()
{   tezi
    /*# ifndef ONLINE_JUDGE
        // for getting input from input.txt
        freopen("input.txt", "r", stdin);
        // for getting input from output.txt
        freopen("output.txt", "w", stdout);
    # endif*/
    cin >> n;
    int sm = (n * (n + 1)) / 2;
    if (sm % 2) {
        cout << 0;
        return 0;
    }
    vector<vector<int>> dp(sm + 1, vector<int>(n + 1, 0));
    dp[0][0] = 1;
    fo1(i, sm + 1) {
        fo1(j, n + 1) {
            dp[i][j] += dp[i][j - 1];
            if ((i - j) >= 0) {
                dp[i][j] += (dp[i - j][j - 1]);
            }
            dp[i][j] = dp[i][j] % mod;
        }
    }
    sm = sm / 2;
    cout << dp[sm][n];
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
