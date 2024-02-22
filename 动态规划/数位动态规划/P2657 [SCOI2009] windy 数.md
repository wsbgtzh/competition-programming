题目链接：https://www.luogu.com.cn/problem/P2657

```c++
#include <bits/stdc++.h>

using namespace std;

#define rep(i, n) for (int i = 0; i < n; i++) 
#define Rep(i, a, b) for (int i = a; i <= b; i++)
#define Repp(i, a, b) for (int i = a; i >= b; i--)
#define x first
#define y second
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
typedef long long ll;
typedef pair<int, int> PII;

ll l, r, a[11], f[11][11];

ll dfs(int pos, bool limit, bool lead0, int last) {
	if (pos == 0) return 1;
	if (!limit && !lead0 && ~f[pos][last]) return f[pos][last];
	ll res = 0;
	int up = limit ? a[pos] : 9;
	for (int i = 0; i <= up; i++) {
		if (abs(i - last) < 2) continue;
		if (lead0 && !i) res += dfs(pos - 1, limit && i == up, true, -2);
		else res += dfs(pos - 1, limit && i == up, false, i);
	} 
	if (!limit && !lead0) f[pos][last] = res;
	return res;
}

ll solve(int n) {
	int m = 0;
	for (; n; n /= 10) a[++m] = n % 10;
	memset(f, -1, sizeof f);
	return dfs(m, true, true, -2);
}

int main()
{
    cin >> l >> r;
    cout << solve(r) - solve(l - 1) << endl;
    return 0;
}
```

