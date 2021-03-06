### [Distinct Colors](https://cses.fi/problemset/task/1734/)

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
#define uniq(v)        v.resize(unique(all(v)) - v.begin())
#define sz(v)          v.size()
#define pii            pair<int, int>

int n,  m, y, e, t, k, q, u1, u2,  w, c, d, x, distinct = 0, cur_time = 1;
const int mx = 800005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
const int block_size = 500;

struct Query
{
    int l;
    int r;
    int idx;
    int blk_no;
};

vector<int> a(mx2, 0);
vector<int> freq(mx2, 0);
vector<int> answer(mx2, 0);
vector<int> euler(mx, 0);
vector<int> start_time(mx2, 0);
vector<int> end_time(mx2, 0);
vector<int> adj[mx2];
vector<Query> queries;

bool comp(Query q1, Query q2) {
    if (q1.blk_no != q2.blk_no) return q1.l < q2.l;
    else {
        if (q1.blk_no & 1) return q1.r > q2.r;
        else return q1.r < q2.r;
    }
    return false;
}

void add(int idx) {
    if (freq[euler[idx]] == 0) distinct++;
    freq[euler[idx]]++;
}

void remove(int idx) {
    if (freq[euler[idx]] == 1) distinct--;
    freq[euler[idx]]--;
}

void dfs(int v, int p) {
    start_time[v] = cur_time;
    euler[cur_time] = a[v];
    cur_time++;

    for (auto it : adj[v]) {
        if (it != p) {
            dfs(it, v);
        }
    }

    end_time[v] = cur_time;
    euler[cur_time] = a[v];
    cur_time++;
    return;
}

void solve() {
    cin >> n;
    vector<int> xs;
    fo1(i, n + 1) {
        cin >> a[i];
        xs.pb(a[i]);
    }

    fo(i, n - 1) {
        cin >> u1 >> u2;
        adj[u1].pb(u2);
        adj[u2].pb(u1);
    }

    // co-ordinate compression using vector since map gives TLE
    sort(all(xs));
    uniq(xs);
    fo1(i, n + 1) a[i] = lower_bound(all(xs), a[i]) - xs.begin() + 1;

    dfs(1, -1);

    fo1(i, n + 1) {
        u1 = start_time[i], u2 = end_time[i];
        queries.pb({u1, u2, i, u1 / block_size});
    }
    sort(all(queries), comp);
    int cur_l = 0;
    int cur_r = -1;
    for (auto q : queries) {
        while (cur_l > q.l) {
            cur_l--;
            add(cur_l);
        }
        while (cur_r < q.r) {
            cur_r++;
            add(cur_r);
        }
        while (cur_l < q.l) {
            remove(cur_l);
            cur_l++;
        }
        while (cur_r > q.r) {
            remove(cur_r);
            cur_r--;
        }
        answer[q.idx] = distinct;
    }
    fo1(i, n + 1) cout << answer[i] << " ";
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
