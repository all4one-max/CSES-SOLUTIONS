### [Shortest Routes I](https://cses.fi/problemset/task/1671/)

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
#define all(v)         v.begin(), v.end()
#define sz(v)          v.size()
#define pii            pair<int, int>

int n,  m, y, e, t, k, len, u1, u2,  w, v, d;
const int mx = 300005, mod = 1000000007, mx2 = 1000005 , mx3 = 100005, INF = 1e9;
vector<pii> adj[mx3];
vector<int> dist(mx2, 1e18);

void dijkstra() {
    set<pii> st;
    dist[1] = 0;
    st.insert({0, 1});
    while (!st.empty()) {
        auto it = *st.begin();
        int vv = it.se, ww = it.fi;
        st.erase(st.begin());
        for (auto itt : adj[vv]) {
            int vvv = itt.fi, www = itt.se;
            if (dist[vvv] > (dist[vv] + www)) {
                st.erase({dist[vvv], vvv});
                dist[vvv] = (dist[vv] + www);
                st.insert({dist[vvv], vvv});
            }
        }
    }
    fo1(i, n + 1) {
        cout << dist[i] << " ";
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
    cin >> n >> m;
    fo(i, m) {
        cin >> u1 >> u2 >> w;
        adj[u1].pb({u2, w});
    }
    dijkstra();
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
