### [Mail Delievery](https://cses.fi/problemset/task/1691/)

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

int n,  m, y, e, t, q, u1, u2,  w, v, c, d, x;
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 100005, INF = 1000000000000000000;
set<int> adj[mx2];
vector<int> degree(mx2, 0);

void solve() {
    cin >> n >> m;
    int first = -1;
    fo(i, m) {
        cin >> u1 >> u2;
        adj[u1].insert(u2);
        adj[u2].insert(u1);
        degree[u1]++;
        degree[u2]++;
        first = u1;
    }

    if (first == -1) {
        cout << "IMPOSSIBLE" << endl;
        return;
    }

    fo1(i, n + 1) {
        if (degree[i] & 1) {
            cout << "IMPOSSIBLE" << endl;
            return;
        }
    }

    stack<int> st;
    st.push(1);
    vector<int> res;
    int cnt = 0;
    while (!st.empty()) {
        int v = st.top();
        if (degree[v] > 0) {
            for (auto it : adj[v]) {
                degree[v]--;
                degree[it]--;
                adj[v].erase(adj[v].find(it));
                adj[it].erase(adj[it].find(v));
                st.push(it);
                break;
            }
        }
        else {
            res.pb(v);
            st.pop();
        }
    }

    fo(i, n + 1) {
        if (degree[i]) {
            cout << "IMPOSSIBLE" << endl;
            return;
        }
    }

    for (auto it : res) cout << it << " ";
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
