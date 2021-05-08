### [Path Queries](https://cses.fi/problemset/task/1138/)

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

int n,  m, y, e, t, q, u1, u2,  w, v, c, d, x, timer = 1;;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> adj[mx2];
vector<int> values(mx2, 0);
vector<int> BIT(mx, 0);
vector<int> start_time(mx2, 0);
vector<int> end_time(mx2, 0);

void update(int index,  int val) {
    while (index <= mx) {
        BIT[index] += val;
        index += (index & (-index));
    }
    return;
}

int query(int index) {
    int sum = 0;
    while (index > 0) {
        sum += BIT[index];
        index -= (index & (-index));
    }
    return sum;
}

void dfs(int v, int p) {
    start_time[v] = timer;
    update(start_time[v], values[v]);
    timer++;

    for (auto it : adj[v]) {
        if (it != p) {
            dfs(it, v);
        }
    }
    end_time[v] = timer;
    update(end_time[v], -1 * values[v]);
    timer++;
    return;
}

void solve() {
    cin >> n >> q;
    fo1(i, n + 1) cin >> values[i];
    fo(i, n - 1) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adj[u2].pb(u1);
    }
    dfs(1, -1);
    fo(i, q) {
        cin >> x;
        if (x == 1) {
            int s, val;
            cin >> s >> val;
            update(start_time[s], val - values[s]);
            update(end_time[s], -1 * (val - values[s]));
            values[s] = val;
        }
        else {
            int s;
            cin >> s;
            cout << query(start_time[s]) << endl;
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
