### [Tree Distance I](https://cses.fi/problemset/task/1132/)

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
const int mx = 400005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> adj[mx2];

int bfs(int v) {
    queue<int> q;
    q.push(v);
    vector<int> visited(n + 1, 0);
    visited[v] = 1;
    int last;
    while (!q.empty()) {
        int v = q.front();
        last = v;
        q.pop();
        for (auto it : adj[v]) {
            if (visited[it] == 0) {
                q.push(it);
                visited[it] = 1;
            }
        }
    }
    return last;
}

void bfs2(int v, vector<int> &dist) {
    queue<int> q;
    q.push(v);
    vector<int> visited(n + 1, 0);
    visited[v] = 1;
    while (!q.empty()) {
        int v = q.front();
        q.pop();
        for (auto it : adj[v]) {
            if (visited[it] == 0) {
                q.push(it);
                visited[it] = 1;
                dist[it] = dist[v] + 1;
            }
        }
    }
    return;
}

void solve() {
    cin >> n;
    fo(i, n - 1) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adj[u2].pb(u1);
    }
    int end_point1 = bfs(1);
    int end_point2 = bfs(end_point1);
    vector<int> dist1(n + 1, 0);
    vector<int> dist2(n + 1, 0);
    bfs2(end_point1, dist1);
    bfs2(end_point2, dist2);
    fo1(i, n + 1) {
        int vl = max(dist1[i], dist2[i]);
        cout << vl << " ";
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
