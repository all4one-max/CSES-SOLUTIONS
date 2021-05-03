### [Hotel Queries](https://cses.fi/problemset/task/1143/)

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
const int mx = 800005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> tre(mx, 0);
vector<int> a(mx2, 0);

void buildTree(int tl, int tr, int treeNode) {
    if (tl == tr) {tre[treeNode] = a[tl]; return;}
    int tm = (tl + tr) / 2;
    buildTree(tl, tm, 2 * treeNode);
    buildTree((tm + 1), tr, 2 * treeNode + 1);
    tre[treeNode] = max(tre[2 * treeNode], tre[2 * treeNode + 1]);
    return;
}

int updateTree(int tl, int tr, int treeNode, int value) {
    if (value > tre[treeNode]) return 0;
    if (tl == tr) {
        tre[treeNode] -= value;
        return tl + 1;
    }
    int tm = (tl + tr) / 2;
    int ans;
    if (value > tre[2 * treeNode]) {
        ans = updateTree(tm + 1, tr, 2 * treeNode + 1, value);
    }
    else ans = updateTree(tl, tm, 2 * treeNode, value);
    tre[treeNode] = max(tre[2 * treeNode], tre[2 * treeNode + 1]);
    return ans;
}

void solve() {
    cin >> n >> q;
    fo(i, n) cin >> a[i];
    buildTree(0, n - 1, 1);
    fo(i, q) {
        cin >> x;
        int ans = updateTree(0, n - 1, 1, x);
        cout << ans << " ";
    }
    cout << endl;
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
