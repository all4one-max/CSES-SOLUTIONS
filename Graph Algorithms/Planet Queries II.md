### [Planet Queries II](https://cses.fi/problemset/task/1160/)

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
vector<int> adj[mx2];
vector<vector<int>> dp(mx2, vector<int> (21, -1));
vector<int> visited(mx2, 0);
vector<int> distance_to_bottom_vertex(mx2, 0);

void dfs(int v) {
    visited[v] = 1;
    // every vertex will have only one child as outdegree is 1 for every vertex
    int child_of_v = dp[v][0];
    if (!visited[child_of_v]) dfs(child_of_v);
    distance_to_bottom_vertex[v] = distance_to_bottom_vertex[child_of_v] + 1;
    return;
}

int lift(int v, int k) {
    int bit = 0;
    while (k) {
        if (k & 1) {
            v = dp[v][bit];
        }
        bit++;
        k = k >> 1;
    }
    return v;
}

void solve() {
    cin >> n >> q;
    fo(i, n) {
        cin >> x;
        dp[i + 1][0] = x;
    }
    fo1(j, 21) {
        fo1(i, n + 1) {
            dp[i][j] = dp[dp[i][j - 1]][j - 1];
        }
    }
    // we will visualize the graph in top bottom fashion, now one thing to note is
    // since the graph is a function graph i.e every vertex has outdegree 1, there would
    // only one vertex in the bottom of every component

    // first we will calculate the distance to this bottom vertex from each vertex
    // using dfs
    fo1(i, n + 1) {
        if (!visited[i]) dfs(i);
    }

    fo(i, q) {
        cin >> u1 >> u2;
        // now u2 can be a successor of u1 in that case if we lift u1 by
        // distance_to_bottom_vertex[u2] - distance_to_bottom_vertex[u1]
        // we will get u2

        // otherwise u2 can be a predecessor of u1 so we can check in the same
        // way as previous but by swapping u1 and u2
        int top_vertex = lift(u1, distance_to_bottom_vertex[u1]);
        if (distance_to_bottom_vertex[u1] - distance_to_bottom_vertex[u2] >= 0
                && lift(u1, distance_to_bottom_vertex[u1] - distance_to_bottom_vertex[u2]) == u2) {
            cout << distance_to_bottom_vertex[u1] - distance_to_bottom_vertex[u2] << endl;
        }
        else if (distance_to_bottom_vertex[top_vertex] - distance_to_bottom_vertex[u2] >= 0
                 && lift(top_vertex, distance_to_bottom_vertex[top_vertex] - distance_to_bottom_vertex[u2]) == u2) {
            int ans = (distance_to_bottom_vertex[top_vertex] - distance_to_bottom_vertex[u2] + distance_to_bottom_vertex[u1]);
            cout << ans << endl;
        }
        else cout << -1 << endl;
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
