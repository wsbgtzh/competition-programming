题目链接：http://acm.hdu.edu.cn/showproblem.php?pid=1710



方法一：

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
int pre[N], in[N], mm[N];
vector<int> post;
int n;

void dfs(int prel, int prer, int inl, int inr) {
	int root = mm[pre[prel]];
	int lsz = root - inl, rsz = inr - root;
	if (lsz) dfs(prel + 1, prel + lsz, inl, root - 1);
	if (rsz) dfs(prel + lsz + 1, prer, root + 1, inr);
	post.push_back(in[root]);
}

int main()
{
    while (cin >> n) {
    	post.clear();
    	rep(i, n) cin >> pre[i];
	    rep(i, n) cin >> in[i], mm[in[i]] = i;
	    dfs(0, n - 1, 0, n - 1);
	    for (int i = 0; i < post.size() - 1; i++) cout << post[i] << ' ';
	   	cout << post[post.size() - 1] << endl;
    }
    return 0;
}
```

方法二：

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
int a[N], b[N];
int n, cnt;

void dfs(int *a, int *b, int n) {
	if (n == 0) return;
	int i;
	for (i = 0; i < n; i++) if (a[0] == b[i]) break;
	dfs(a + 1, b, i);
	dfs(a + i + 1, b + i + 1, n - i - 1);
	if (cnt) cout << ' ';
	cnt++;
	cout << a[0];
}

int main()
{
    while (cin >> n) {
    	cnt = 0;
    	rep(i, n) cin >> a[i];
   		rep(i, n) cin >> b[i];
   		dfs(a, b, n);
    }
    return 0;
}
```

