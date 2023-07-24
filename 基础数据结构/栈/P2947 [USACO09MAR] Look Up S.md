题目链接：https://www.luogu.com.cn/problem/P2947

单调栈:)

```c++
#include <bits/stdc++.h>

using namespace std;

#define rep(i, n) for (int i = 0; i < n; i++) 
#define Rep(i, a, b) for (int i = a; i <= b; i++)
#define Repp(i, a, b) for (int i = a; i >= b; i--)
#define x first
#define y second
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
typedef long long LL;
typedef pair<int, int> PII;

const int N = 100010;
int n;
int h[N], stk[N];

int main()
{
    cin >> n;
   	rep(i, n) cin >> h[i];
   	vector<int> res;
   	int tt = 0;
   	for (int i = n - 1; i >= 0; i--) {
   		while (tt && h[stk[tt]] <= h[i]) tt--;
   		if (tt) res.push_back(stk[tt] + 1);
   		else res.push_back(0);
   		stk[++tt] = i;
   	}
   	reverse(res.begin(), res.end());
   	for (auto x : res) cout << x << endl;
    return 0;
}
```

