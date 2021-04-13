### [Labyrinth](https://cses.fi/problemset/task/1193/)

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
vector<vector<int>> visited(1001, vector<int> (1001, 0));
vector<array<int, 2>> mov = {{ -1, 0}, {0, 1}, {1, 0}, {0, -1}};
vector<vector<pii>> parent(1001, vector<pii> (1001, { -1, -1}));
map<pii, char> ind;

void bfs(int i, int j) {
    queue<pii> q;
    q.push({i, j});
    visited[i][j] = 1;
    bool found = false;
    //cout << "ok" << 1 << endl;
    pii start = {i, j};
    pii end = { -1, -1};
    while (!q.empty()) {
        auto it = q.front();
        int x = it.fi, y = it.se;
        //cout << x << " " << y << endl;
        if (store[x][y] == 'B') {
            found = true;
            end = {x, y};
            break;
        }
        q.pop();
        for (auto it : mov) {
            int nx = x + it[0], ny = y + it[1];
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && visited[nx][ny] == 0 && (store[nx][ny] == '.' || store[nx][ny] == 'B')) {
                visited[nx][ny] = 1;
                q.push({nx, ny});
                parent[nx][ny] = {x, y};
            }
        }
    }
    //cout << "ok" << 2 << endl;
    if (found) {
        cout << "YES" << endl;
        string s = "";
        pii cur = end;
        while (true) {
            pii get = parent[cur.fi][cur.se];
            if (get == make_pair(-1, -1)) break;
            if (get.fi > cur.fi) s += 'U';
            else if (get.fi < cur.fi) s += 'D';
            else if (get.se > cur.se) s += 'L';
            else s += 'R';
            cur = get;
        }
        reverse(all(s));
        cout << s.length() << endl;
        cout << s << endl;
    }
    else cout << "NO" << endl;
    return;
}

void has_path() {
    fo(i, n) {
        fo(j, m) {
            if (store[i][j] == 'A') {
                bfs(i, j);
                return;
            }
        }
    }
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
    ind[ { -1, 0}] = 'U'; ind[ {0, 1}] = 'R'; ind[ {1, 0}] = 'D'; ind[ {0, -1}] = 'L';
    has_path();
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
