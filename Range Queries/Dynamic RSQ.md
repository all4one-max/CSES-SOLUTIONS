### [Dynamic Range Sum Queries](https://cses.fi/problemset/task/1648/)

```cpp
// solved using square root decomposition
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

int n,  m, y, e, t, q, u1, u2,  w, v, c, d, x, timer = 1;;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> a(mx2, 0);
vector<int> blocks(mx2, 0);

void pre_process() {
    int sq = floor(sqrt(n));
    int cur_blk = -1;
    fo(i, n) {
        if (i % sq == 0) cur_blk++;
        blocks[cur_blk] += a[i];
    }
    return;
}

int queries(int l, int r) {
    int sq = floor(sqrt(n));
    int ans = 0;
    while (l % sq != 0 && l < r) {
        ans += a[l];
        l++;
    }
    while (l + sq - 1 <= r) {
        ans += blocks[l / sq];
        l += sq;
    }
    while (l <= r) {
        ans += a[l];
        l++;
    }
    return ans;
}

void update(int pos, int val) {
    int sq = floor(sqrt(n));
    blocks[pos / sq] += (val - a[pos]);
    a[pos] = val;
}

void solve() {
    cin >> n >> q;
    fo(i, n) cin >> a[i];
    pre_process();
    fo(i, q) {
        cin >> x >> u1 >> u2;

        if (x == 1) {
            u1--;
            update(u1, u2);
        }
        else {
            u1--; u2--;
            cout << queries(u1, u2) << endl;
        }
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
