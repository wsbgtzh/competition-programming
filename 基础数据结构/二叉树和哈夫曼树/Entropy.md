题目链接：http://poj.org/problem?id=1521

```c++
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cstdio>
#include <queue>

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
	priority_queue<int, vector<int>, greater<int> > q;
 	string s;
 	while (getline(cin, s) && s != "END") {
 		int cnt = 1;
 		sort(s.begin(), s.end());
 		for (int i = 1; i <= s.length(); i++) {
 			if (s[i] != s[i - 1]) q.push(cnt), cnt = 1;
 			else cnt++; 
 		}
 		int res = 0;
 		if (q.size() == 1) res = s.length();
 		while (q.size() > 1) {
 			int a = q.top(); q.pop();
 			int b = q.top(); q.pop();
 			q.push(a + b);
 			res += a + b;
 		}
 		q.pop();
 		printf("%d %d %.1lf\n", s.length() * 8, res, (double)s.length() * 8 / (double)res);
 	}
    return 0;
}
```

