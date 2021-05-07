### [Range Update and Sums](https://cses.fi/problemset/task/1735/)

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

int n, x, m, y, e, k, len, u1, u2, q, f;
const int mx = 800005, mod = 1000000007, mx2 = 200005 , mx3 = 2000005, INF = 1000000000000000000;

struct dat
{
    int sum;
    int increment;
    int setAll;
    int marked;
};

vector<dat> tre(mx, {0, 0, 0, 0});
vector<int> a(mx2, 0);

void buildTree(int tl, int tr, int treeNode) {
    if (tl == tr) {tre[treeNode].sum = a[tl]; return;}
    int tm = (tl + tr) / 2;
    buildTree(tl, tm, 2 * treeNode);
    buildTree((tm + 1), tr, 2 * treeNode + 1);
    tre[treeNode].sum = tre[2 * treeNode].sum + tre[2 * treeNode + 1].sum;
    return;
}

void push(int tl, int tr, int treeNode) {
    int tm = (tl + tr) / 2;
    if (tre[treeNode].marked) {
        tre[2 * treeNode].sum = (tm - tl + 1) * tre[treeNode].setAll;
        tre[2 * treeNode + 1].sum = (tr - tm) * tre[treeNode].setAll;
        tre[2 * treeNode].setAll = tre[treeNode].setAll;
        tre[2 * treeNode + 1].setAll = tre[treeNode].setAll;
        tre[2 * treeNode].increment = 0;
        tre[2 * treeNode + 1].increment = 0;
        tre[treeNode].setAll = 0;
        tre[treeNode].marked = 0;
        tre[2 * treeNode].marked = 1;
        tre[2 * treeNode + 1].marked = 1;
    }
    tre[2 * treeNode].sum += (tm - tl + 1) * tre[treeNode].increment;
    tre[2 * treeNode + 1].sum += (tr - tm) * tre[treeNode].increment;
    tre[2 * treeNode].increment += tre[treeNode].increment;
    tre[2 * treeNode + 1].increment += tre[treeNode].increment;
    tre[treeNode].increment = 0;
    return;
}

void updateTree(int tl, int tr, int treeNode, int l, int r, int new_value, int type) {
    if (l > r) return;
    if (tl == l && tr == r) {
        if (type == 1) {
            tre[treeNode].sum += (tr - tl + 1) * new_value;
            tre[treeNode].increment += new_value;
        }
        else {
            tre[treeNode].sum = (tr - tl + 1) * new_value;
            tre[treeNode].marked = 1;
            tre[treeNode].setAll = new_value;
            tre[treeNode].increment = 0;
        }
        return;
    }
    push(tl, tr, treeNode);
    int tm = (tl + tr) / 2;
    updateTree(tl, tm, 2 * treeNode, l, min(tm, r), new_value, type);
    updateTree(tm + 1, tr, 2 * treeNode + 1, max(l, tm + 1), r, new_value, type);
    tre[treeNode].sum = tre[2 * treeNode].sum + tre[2 * treeNode + 1].sum;
    return;
}

int query(int tl, int tr, int treeNode, int left, int right) {
    if (left > right) return 0;
    if (left == tl && right == tr) return tre[treeNode].sum;
    push(tl, tr, treeNode);
    int tm = (tl + tr) / 2;
    int ans1 = query(tl, tm, 2 * treeNode, left, min(right, tm));
    int ans2 = query(tm + 1, tr, 2 * treeNode + 1, max(left, tm + 1), right);
    return ans1 + ans2;
}

signed main()
{   tezi
# ifndef ONLINE_JUDGE
    // for getting input from input.txt
    freopen("input.txt", "r", stdin);
    // for getting input from output.txt
    freopen("output.txt", "w", stdout);
# endif
    cin >> n >> q;
    fo(i, n) cin >> a[i];
    buildTree(0, n - 1, 1);
    fo(i, q) {
        cin >> x;
        if (x == 1) {
            cin >> u1 >> u2 >> k;
            u1--; u2--;
            updateTree(0, n - 1, 1, u1, u2, k, 1);

        }
        else if (x == 2) {
            cin >> u1 >> u2 >> k;
            u1--; u2--;
            updateTree(0, n - 1, 1, u1, u2, k, 2);
        }
        else {
            cin >> u1 >> u2;
            u1--; u2--;
            cout << query(0, n - 1, 1, u1, u2) << endl;
        }
    }
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
