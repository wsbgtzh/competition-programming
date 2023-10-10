题目链接：http://poj.org/problem?id=3061

```c++
#include <iostream>
#include <algorithm>
#include <cstring>

using namespace std;

const int N = 100010;
int T, n, m, a[N], s[N];

int main() {
	cin >> T;
	while (T--) {
		cin >> n >> m;
		for (int i = 1; i <= n; i++) cin >> a[i], s[i] = s[i - 1] + a[i];
		int minv = n + 1;
		for (int i = 1, j = 1; i <= n; i++) {
			while (s[j] <= s[i] - m && j < i) j++;
			if (s[j - 1] <= s[i] - m) minv = min(minv, i - j + 1);
		}
		if (minv == n + 1) cout << 0 << endl;
		else cout << minv << endl;
	}
	return 0;
}
```

