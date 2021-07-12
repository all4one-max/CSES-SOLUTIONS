### [Finding a Centroid](https://cses.fi/problemset/task/2079/)

```cpp
now it helps to have done some previous problem
namely, the "nearest greater element"
because that sol kinda makes this one intuitive
basically
solve offline
if we sweep from, say, right to left, to answer a query we need sum of [largest element to left] on range
and the easiest way to do that is to maintain an array where a[i] = (largest element to left of i) where the elements considered are only the ones we've seen in the sweepline
so when we move one to the left (basically sticking an element onto the left), how does that change this array?
suppose we stick a[L] onto the left
some values will change their largest value to a[L], and others will be unchanged
the leftmost one that's unchanged has a value >= a[L], meaning a[L] is irrelevant to everything to the right of that, and everything to the left of that will be changed
in other words, some range of the array will be changed
so it's just (set a[l..r] := x) and (sum of a[l..r])
might be able to produce something more coherent at not-4 AM
```
