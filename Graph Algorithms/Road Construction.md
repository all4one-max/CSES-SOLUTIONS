### [Road Construction](https://cses.fi/problemset/task/1676/)

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

int n,  m, y, e, t, k, q, u1, u2,  w, v, c, d, x, ans = 0;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 100005, INF = 1000000000000000000;
int num_compo, mx_compo;

struct subset {
    int rank, parent, size;
};
vector<subset> ranks;

int find_parent_nd_compress(int cur) {
    if (ranks[cur].parent != cur) {
        ranks[cur].parent = find_parent_nd_compress(ranks[cur].parent);
    }
    return ranks[cur].parent;
}

int uunion(int x, int y) {
    int xroot = find_parent_nd_compress(x);
    int yroot = find_parent_nd_compress(y);

    if (ranks[xroot].rank > ranks[yroot].rank) {
        ranks[yroot].parent = xroot;
        ranks[xroot].size += ranks[yroot].size;
        return xroot;
    }
    else if (ranks[xroot].rank < ranks[yroot].rank) {
        ranks[xroot].parent = yroot;
        ranks[yroot].size += ranks[xroot].size;
        return yroot;
    }
    else {
        ranks[yroot].parent = xroot;
        ranks[xroot].rank += 1;
        ranks[xroot].size += ranks[yroot].size;
        return xroot;
    }
}

void solve() {
    cin >> n >> m;
    ranks.pb({ -1, -1, -1});
    fo1(i, n + 1) {
        ranks.pb({0, i, 1});
    }
    num_compo = n, mx_compo = 1;
    fo(i, m) {
        cin >> u1 >> u2;
        int p1 = find_parent_nd_compress(u1);
        int p2 = find_parent_nd_compress(u2);
        if (p1 != p2) {
            num_compo--;
            int papa = uunion(p1, p2);
            mx_compo = max(mx_compo, ranks[papa].size);
        }
        cout << num_compo << " " << mx_compo << endl;
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
