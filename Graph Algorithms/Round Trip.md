### [Round Trip](https://cses.fi/problemset/task/1669/)

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
vector<int> adj[mx3];
vector<int> visited(mx3, 0);
vector<int> parent(mx3, -1);

vector<int> dfs(int v, int p) {
    visited[v] = 1;
    for (auto it : adj[v]) {
        if (visited[it] == 0) {
            parent[it] = v;
            vector<int> rec = dfs(it, v);
            if (rec[0] != -1) return rec;
        }
        else {
            if (p != it) {
                return {v, it};
            }
        }
    }
    return { -1, -1};
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
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adj[u2].pb(u1);
    }
    // basically it's asking us to detect cycle
    bool not_found = true;
    fo1(i, n + 1) {
        if (visited[i] == 0) {
            vector<int> rec = dfs(i, -1);
            if (rec[0] != -1) {
                int start = rec[0], end = rec[1], cur = start;
                vector<int> ans;
                while (cur != end) {
                    ans.pb(cur);
                    cur = parent[cur];
                }
                ans.pb(end);
                ans.pb(start);
                cout << sz(ans) << endl;
                for (auto it : ans) cout << it << " ";
                cout << endl;
                not_found = false;
                break;
            }
        }
    }
    if (not_found) cout << "IMPOSSIBLE" << endl;
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
