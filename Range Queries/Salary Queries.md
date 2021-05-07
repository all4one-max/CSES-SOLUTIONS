### [Salary Queries](https://cses.fi/problemset/task/1144/)

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

int n,  m, y, e, t, k, q, u1, u2,  w, v, c, d, x, timer = 1;;
const int mx = 800005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;
vector<int> tre(2000005, 0);
vector<int> salary_cnt(400005, 0);
vector<int> emp(mx2, 0);
map<int, int> big_salary_small;

void buildTree(int tl, int tr, int treeNode) {
    if (tl == tr) {
        tre[treeNode] = salary_cnt[tl];
        return;
    }
    int tm = (tl + tr) / 2;
    buildTree(tl, tm, 2 * treeNode);
    buildTree((tm + 1), tr, 2 * treeNode + 1);
    tre[treeNode] = tre[2 * treeNode] + tre[2 * treeNode + 1];
    return;
}

void updateTree(int tl, int tr, int treeNode, int idx, int value) {
    if (tl == tr) {
        tre[treeNode] += value;
        return;
    }
    int tm = (tl + tr) / 2;
    if (idx > tm) updateTree(tm + 1, tr, 2 * treeNode + 1, idx, value);
    else updateTree(tl, tm, 2 * treeNode, idx, value);
    tre[treeNode] = tre[2 * treeNode] + tre[2 * treeNode + 1];
    return;
}

int query(int tl, int tr, int treeNode, int left, int right) {
    if (left > right) return 0;
    if (left == tl && right == tr) return tre[treeNode];
    int tm = (tl + tr) / 2;
    int ans1 = query(tl, tm, 2 * treeNode, left, min(right, tm));
    int ans2 = query(tm + 1, tr, 2 * treeNode + 1, max(left, tm + 1), right);
    return ans1 + ans2;
}

void solve() {
    cin >> n >> q;
    vector<int> vals;
    fo(i, n) {
        cin >> x;
        emp[i] = x;
        vals.pb(x);
    }
    buildTree(0, 400000, 1);
    vector<array<int, 3>> queries;
    fo(i, q) {
        char c;
        cin >> c;
        if (c == '!') {
            cin >> k >> x;
            queries.pb({0, k - 1, x});
            vals.pb(x);
        }
        else {
            cin >> u1 >> u2;
            queries.pb({1, u1, u2});
        }
    }
    sort(all(vals));
    uniq(vals);
    fo(i, sz(vals)) big_salary_small[vals[i]] = (i + 1);
    fo(i, n) emp[i] = big_salary_small[emp[i]];
    fo(i, n) salary_cnt[emp[i]]++;
    int szv = sz(vals);
    buildTree(0, 400005, 1);
    fo(i, q) {
        if (queries[i][0]) {
            int start, end;
            int x = lower_bound(all(vals), queries[i][1]) - vals.begin();
            if (x == szv) {
                cout << 0 << endl;
                continue;
            }
            else start = big_salary_small[vals[x]];

            int y = lower_bound(all(vals), queries[i][2]) - vals.begin();
            if (y == szv) end = big_salary_small[vals[szv - 1]];
            else {
                if (vals[y] == queries[i][2]) end = big_salary_small[vals[y]];
                else {
                    y -= 1;
                    if (x > y) {
                        cout << 0 << endl;
                        continue;
                    }
                    else end = big_salary_small[vals[y]];
                }
            }
            cout << query(0, 400005, 1, start, end) << endl;
        }
        else {
            updateTree(0, 400005, 1, emp[queries[i][1]], -1);
            emp[queries[i][1]] = big_salary_small[queries[i][2]];
            updateTree(0, 400005, 1, emp[queries[i][1]], 1);
        }
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
