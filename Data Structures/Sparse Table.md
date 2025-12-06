The Sparse Table is a algorithm that can answer queries in `O (1)`, it work in arrays that are static. In dinamyc arrays, is used the segment trees or the fenwick tree. 

```
// Insert template here !!

struct SparseTable {
  int n, K;
  vector<vector<int>> st;
  
  // Function to construct 
  SparseTable(const vector<int> &a) {
    n = sz(a);
    K = int(log2(n)) + 1;
    st.assign(n + 1, vector<int>(K));
    forn (i, n) st[i][0] = a[i];
    forn (j, K - 1)
      for (int i = 0; i + (1 << (j + 1)) <= n; ++i)
        st[i][j + 1] = oper(st[i][j], st[i + (1 << j)][j]);
  }

  int oper(int a, int b) { return max(a, b); }

  int query(int l, int r) {
    int k = 31 - __builtin_clz(r - l + 1);
    return oper(st[l][k], st[r - (1 << k) + 1][k]);
  }
};
```
