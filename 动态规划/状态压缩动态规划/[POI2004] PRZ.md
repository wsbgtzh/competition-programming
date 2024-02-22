题目链接：https://www.luogu.com.cn/problem/P5911

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

int main()
{
 	int n, W;
 	cin >> W >> n;

 	vector<int> ts(1 << n), tw(1 << n);
 	for (int i = 0, t, w; i < n; i++) {
 		cin >> t >> w;
 		for (int j = 0; j < 1 << n; j++)
 			if (j & (1 << i)) {
 				ts[j] = max(ts[j], t);
 				tw[j] += w;
 			}
 	}   
 	vector<int> f(1 << n, 1 << 30);
 	for (int s = 0; s < 1 << n; s++) {
 		if (tw[s] <= W) f[s] = ts[s];
 		for (int j = s; j; j = (j - 1) & s)
 			if (tw[j ^ s] <= W)
 				f[s] = min(f[s], f[j] + ts[j ^ s]);
 	}
 	cout << f[(1 << n) - 1] << '\n';
    return 0;
}
```

