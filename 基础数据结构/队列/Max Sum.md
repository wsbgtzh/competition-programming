题目链接：http://acm.hdu.edu.cn/showproblem.php?pid=1003



方法一：贪心

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

int main()
{
 	int T; cin >> T;
 	for (int t = 1; t <= T; t++) {
 		int n; cin >> n;
 		int s = 0, st = 0, ed = 0, p = 0, mx = -0x3f3f3f3f;
 		for (int i = 0; i < n; i++) {
 			int x; cin >> x;
 			s += x;
 			if (mx < s) mx = s, st = p + 1, ed = i + 1;
 			if (s < 0) s = 0, p = i + 1;
 		}
 		cout << "Case " << t << ':' << endl;
 		cout << mx << ' ' << st << ' ' << ed << endl;
 	}   
    return 0;
}
```

方法二：dp

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

int main()
{
	int T; cin >> T;
	for (int t = 1; t <= T; t++) {
		int n; cin >> n;
		vector<int> f(n + 1);
		Rep(i, 1, n) cin >> f[i];
		int st = 1, ed = 1, p = 1, mx = f[1];
		Rep(i, 2, n) {
			if (f[i] + f[i - 1] >= f[i]) f[i] = f[i - 1] + f[i];
			else p = i;
			if (f[i] > mx) mx = f[i], st = p, ed = i;
		}
		cout << "Case " << t << ':' << endl;
		cout << mx << ' ' << st << ' ' << ed << endl;
	}    
    return 0;
}
```

