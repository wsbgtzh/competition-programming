题目链接：http://acm.hdu.edu.cn/showproblem.php?pid=1062

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

const int N = 1010;
char stk[N];
int n;

int main()
{
	cin >> n;
	getchar();
	while (n--) {
		string s; getline(cin, s);
		int tt = 0;
		for (auto &x : s) {
			if (x != ' ') stk[++tt] = x;
			else {
				while (tt) cout << stk[tt--];
				cout << ' ';
			}
		}
		while (tt) cout << stk[tt--];
		cout << endl;
	} 	   
    return 0;
}
```

