### [Counting Rooms](https://cses.fi/problemset/task/1192/)

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <map>
using namespace __gnu_pbds;
using namespace std;
#define tezi           ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define ordered_set    tree<int, null_type,less<int>, rb_tree_tag,tree_order_statistics_node_update>
//#define int            long long
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
vector<vector<char>> store(1005, vector<char> (1005, 0));
vector<vector<int>> visited(1000, vector<int> (1000, 0));
vector<array<int, 2>> mov = {{ -1, 0}, {0, 1}, {1, 0}, {0, -1}};

void dfs(int i, int j) {
    visited[i][j] = 1;
    for (auto it : mov) {
        int nx = i + it[0], ny = j + it[1];
        if (nx >= 0 && nx < n && ny >= 0 && ny < m && store[i][j] == '.' && visited[nx][ny] == 0) {
            dfs(nx, ny);
        }
    }
    return;
}

void count_rooms() {
    //for (auto it : mov) cout << it[0] << " " << it[1] << endl;
    int rooms = 0;
    fo(i, n) {
        fo(j, m) {
            if (visited[i][j] == 0 && store[i][j] == '.') {
                dfs(i, j);
                rooms++;
            }
        }
    }
    cout << rooms << endl;
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
    fo(i, n) fo(j, m) cin >> store[i][j];
    count_rooms();
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
