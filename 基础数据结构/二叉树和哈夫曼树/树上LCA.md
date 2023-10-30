题目：

给你一棵树，树以下列方式给出：

​	编号为1的节点为根节点；

​	输入第一给出一个数n，表示一共有n个节点；

​	接下来n-1行， 每行给出两个数x，y $$ (x \ne y)$$ , 表示x，y之间有一条边。

接下来有m个询问，每组询问两个数x，y $$ (x \ne y)$$ ， 你需要求出x，y的 LCA 并输出。



##### 样例输入：

```
4
1 2
1 3
3 4
2
1 2
2 4
```

##### 样例输出：

```
1
1
```

##### 数据范围1: $$ 1 \le n, m \le 1000, 1 \le x, y \le n, x \ne y$$

##### 数据范围2: $$ 1 \le n, m \le 100000, 1 \le x, y \le n, x \ne y$$



##### 范围1的代码$$ O(n^2)$$

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
int father[N], n, dist[N], m;
vector<int> edges[N];

inline void dfs(int x) {
	for (auto y : edges[x]) {
		dist[y] = dist[x] + 1;
		dfs(y);
	}
}

int main()
{
    cin >> n;
    for (int i = 1; i < n; i++) {
    	int a, b;
    	cin >> a >> b;
    	edges[a].push_back(b);
    	father[b] = a;
    }

    memset(dist, 0, sizeof dist);
    dfs(1);
    cin >> m;
    for (int i = 1; i <= m; i++) {
    	int x, y;
    	cin >> x >> y;
    	if (dist[x] < dist[y]) swap(x, y);
    	int z = dist[x] - dist[y];
    	for (int j = 1; j <= z; j++) 
    		x = father[x];
    	while (x != y) 
    		x = father[x], y = father[y];
    	cout << x << endl;
    }

    return 0;
}
```

##### 范围2的代码$$ O(n)$$

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
int father[N][21], n, dist[N], m;
vector<int> edges[N];

inline void dfs(int x) {
	for (auto y : edges[x]) {
		dist[y] = dist[x] + 1;
		dfs(y);
	}
}

int main()
{
    cin >> n;
    for (int i = 1; i < n; i++) {
    	int a, b;
    	cin >> a >> b;
    	edges[a].push_back(b);
    	father[b][0] = a;
    }

    for (int i = 1; i <= 20; i++) {
    	for (int j = 1; j <= n; j++) 
    		if (father[j][i - 1])
    			father[j][i] = father[father[j][i - 1]][i - 1];
    }

    memset(dist, 0, sizeof dist);
    dfs(1);
    cin >> m;
    for (int i = 1; i <= m; i++) {
    	int x, y;
    	cin >> x >> y;
    	if (dist[x] < dist[y]) swap(x, y);
    	int z = dist[x] - dist[y];
    	for (int j = 0; j <= 20 && z; j++, z /= 2)
    		if (z & 1) 
    			x = father[x][j];

    	if (x == y) {
    		cout << x << endl;
    		continue;
    	}

    	for (int j = 20; j >= 0; j--) 
    		if (father[x][j] != father[y][j])
    			x = father[x][j], y = father[y][j];
    	cout << father[x][0] << endl;
    }

    return 0;
}
```

