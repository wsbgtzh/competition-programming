题目链接：http://acm.hdu.edu.cn/showproblem.php?pid=2527

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
	priority_queue<int, vector<int>, greater<int>>q;
    int t; cin >> t;
    while (t--) {
    	int n; cin >> n;
    	string s; cin >> s;
    	sort(s.begin(), s.end());
    	s = '0' + s;
    	int cnt = 1;
    	for (int i = 1; i < s.size(); i++) 
    		if (s[i] != s[i - 1]) q.push(cnt), cnt = 1;
    		else cnt++;
    	int res = 0;
    	if (q.size() == 1) res = s.size() - 1;
    	while (q.size() > 1) {
    		auto a = q.top(); q.pop();
    		auto b = q.top(); q.pop();
    		q.push(a + b);
    		res += a + b;
    	}
    	q.pop();
    	if (res <= n) cout << "yes" << endl;
    	else cout << "no" << endl;
    }
    return 0;
}
```

