---
title: "CF1641E Special Positions"
date: 2022-02-27 10:25:20
tags:
  - 卷积
  - 期望
categories:
  - CF题解
---

[题目地址](https://codeforces.com/problemset/problem/1641/E)

题意：

给定长度为 $n$ 的数组 $a$，长度为 $m$ 的数组 $p$，其中 $1 \le p_i \le n$ ，而且 $\forall j, p_i \not = p_j$。

在 $p$ 中等概率选定一个非空集合，求 $\sum_{i = 1} ^ n a_i \times |i - p_j|$ 其中 $p_j$ 是选定集合中 $|i - p_j|$ 最小的 $p$。

$m \le n \le 10^5$。

---

- 我们考虑先将期望拆分成方案数除以总方案，很显然总方案就是 $2^m - 1$。

- 然后我们发现对于每一个数 $a_i$ 本质上是没有影响的，我们只需要计算后面部分总共贡献的次数就好了。

- 再者我们发现 $m$ 是很大的，所以肯定是不能枚举和子集有关的东西了，那么我们可以考虑将数组 $p$ 表示成 $\sum_{i = 1} ^ n [i \in P]$ 的形式。

根据以上的发现我们可以直观感受到这个肯定是和卷积有关的形式。

如果是一个卷积，我们肯定是需要将数组翻转，我们不妨考虑用 $i + j = 2\times pos $ 的形式表示最终的位置。

我们考虑左右两边的贡献，也就是将每个位置的贡献分开算，就是 $i, -i, j, -j$ 四种状况。

我们就拿 $i$ 举例子：

对于 $i$ 对于 $pos$ 的贡献，也就是左边向右的贡献，显然有区间 $(i, 2 \times pos - i]$ 是不能被计算到了。

> 考虑一边取到，为了防止之后算重。
> 
> 当然计算后面的时候就不需要取到了。

我们不妨考虑使用前缀积的形式来表示取到的区间。

然后对于计算贡献需要使用一个分治 $FFT$ 即可。

> 都是左边向右边的贡献。

我们再考虑一下是否还漏掉了什么，一个点在我们这样的计算情况下会被计算几次？

也就是作为 $i, j$ 的时候都分别被计算了一次，那么我们只需要在计算的时候乘一个 $\frac{1}{2}$ 即可。

如果要更详细一点可以参考代码。

```cpp
#include <bits/stdc++.h>
using namespace std;
namespace Legendgod {
	namespace Read {
//		#define Fread
		#ifdef Fread
		const int Siz = (1 << 21) + 5;
		char *iS, *iT, buf[Siz];
		#define gc() ( iS == iT ? (iT = (iS = buf) + fread(buf, 1, Siz, stdin), iS == iT ? EOF : *iS ++) : *iS ++ )
		#define getchar gc
		#endif
		template <typename T>
		void r1(T &x) {
		    x = 0;
			char c(getchar());
			int f(1);
			for(; !isdigit(c); c = getchar()) if(c == '-') f = -1;
			for(; isdigit(c); c = getchar()) x = (x << 1) + (x << 3) + (c ^ 48);
			x *= f;
		}
		template <typename T, typename...Args>
		void r1(T &x, Args&...arg) {
			r1(x), r1(arg...);
		}
		#undef getchar
	}

using namespace Read;

const int maxn = 2e6 + 5;
const int mod = 998244353;

int ksm(int x,int mi) {
    int res(1);
    while(mi) {
        if(mi & 1) res = 1ll * res * x % mod;
        mi >>= 1;
        x = 1ll * x * x % mod;
    }
    return res;
}

int Inv(int x) { return ksm(x, mod - 2); }

int n, m;

int lim, rev[maxn], len;

void getrev(int x) {
    lim = 1, len = 0;
    while(lim <= x) lim <<= 1, ++ len;
    for(int i = 0; i < lim; ++ i) rev[i] = (rev[i >> 1] >> 1) | ((i & 1) << (len - 1));
}

const int G1 = 3, Gi = Inv(G1);

int w[2][21][maxn], inv[maxn];

void init(int up) {
    for(int i = 1; i <= up; ++ i) {
        w[0][i][0] = w[1][i][0] = 1;
        int w0 = ksm(G1, (mod - 1) / (1 << i));
        int w1 = ksm(Gi, (mod - 1) / (1 << i));
        for(int j = 1; j < (1 << i); ++ j) {
            w[0][i][j] = 1ll * w[0][i][j - 1] * w0 % mod;
            w[1][i][j] = 1ll * w[1][i][j - 1] * w1 % mod;
        }
    }
    for(int i = 1; i < (1 << up); ++ i) inv[i] = ksm(i, mod - 2);
}

void NTT(int *A,int opt = 1) {
    for(int i = 0; i < lim; ++ i) if(i < rev[i]) swap(A[i], A[rev[i]]);
    for(int mid = 1, c = 1; mid < lim; mid <<= 1, ++ c) {
        for(int j = 0, s = (mid << 1); j < lim; j += s) {
            int p = (opt == 1 ? 0 : 1);
            for(int k = 0; k < mid; ++ k) {
                int x = A[j + k], y = 1ll * A[j + k + mid] * w[p][c][k] % mod;
                A[j + k] = (x + y) % mod;
                A[j + k + mid] = (x - y + mod) % mod;
            }
        }
    }
    if(opt == -1) {
        for(int i = 0; i < lim; ++ i) A[i] = 1ll * A[i] * inv[lim] % mod;
    }
}

int Mul(const int *s1, const int *s2, int *Ans,int n,int m) {
    getrev(max(n, m) << 1);
    static int tmp1[maxn], tmp2[maxn];
    memset(tmp1, 0, 4 * lim), memcpy(tmp1, s1, n * 4);
    memset(tmp2, 0, 4 * lim), memcpy(tmp2, s2, m * 4);
    NTT(tmp1), NTT(tmp2);
    for(int i = 0; i < lim; ++ i) Ans[i] = 1ll * tmp1[i] * tmp2[i] % mod;
    NTT(Ans, -1);
    return n + m;
}

int F[maxn], G[maxn];

void Solve(int *x,int *y,int *Ans,int l,int r) {
    if(l == r) return ;
    int mid = (l + r) >> 1;
    Solve(x, y, Ans, l, mid), Solve(x, y, Ans, mid + 1, r);
    static int tmp1[maxn], tmp2[maxn], res[maxn];
    for(int i = l; i <= mid; ++ i) tmp1[i - l] = x[i];
    for(int i = mid + 1; i <= r; ++ i) tmp2[i - mid - 1] = y[i];
    int sz = Mul(tmp1, tmp2, res, mid - l + 1, r - mid);
    for(int i = 0; i < sz; ++ i) Ans[l + mid + 1 + i] = (Ans[l + mid + 1 + i] + res[i]) % mod;
}

void Calc(int *x,int *y,int *z) {
    memset(z, 0, 16 * n);
    Solve(x, y, z, 1, 2 * n);
}

int a[maxn], sp[maxn], sum[maxn];

const int Inv2 = ksm(2, mod - 2);

int A[maxn], B[maxn], C[maxn];
int ans[maxn];

signed main() {
	init(20);
	int i, j;
    r1(n, m);
    for(i = 1; i <= n; ++ i) r1(a[i]);
    for(i = 1; i <= m; ++ i) { int c; r1(c); sp[c] = 1; }
    for(i = 1; i <= 2 * n; ++ i) sum[i] = sum[i - 1] + sp[i];
    // left i
    for(i = 1; i <= n; ++ i) A[i] = 1ll * sp[i] * ksm(2, sum[i]) % mod * Inv2 % mod;
    for(i = 1; i <= 2 * n; ++ i) B[i] = ksm(Inv2, sum[i - 1]);
    Calc(A, B, C);
    for(i = 1; i <= n; ++ i) ans[i] = (ans[i] + 1ll * i * C[i * 2] % mod) % mod;
    // left -j
    for(i = 1; i <= n; ++ i) A[i] = 1ll * A[i] * i % mod;
    Calc(A, B, C);
    for(i = 1; i <= n; ++ i) ans[i] = (ans[i] - C[i * 2] + mod) % mod;
    // ---
    memset(A, 0, sizeof(A)), memset(B, 0, sizeof(B));
    // right -i
    for(i = 1; i <= n; ++ i) A[i + n] = 1ll * Inv2 * sp[i] % mod * ksm(Inv2, sum[i - 1]) % mod;
    for(i = 1; i <= n; ++ i) B[i] = 1; // 2 ^ 0
    for(i = n + 1; i <= 2 * n; ++ i) B[i] = ksm(2, sum[i - n - 1]);
    Calc(B, A, C);
    for(i = 1; i <= n; ++ i) ans[i] = (ans[i] - 1ll * i * C[2 * i + 2 * n] % mod + mod) % mod;
//    for(i = 1; i <= n; ++ i) printf("%d%c", ans[i], " \n"[i == n]);
    // right j
    for(i = 1; i <= n; ++ i) A[i + n] = 1ll * A[i + n] * i % mod;
    Calc(B, A, C);
    for(i = 1; i <= n; ++ i) ans[i] = (ans[i] + C[2 * i + 2 * n]) % mod;
    // ---
    int sum(0);
    for(i = 1; i <= n; ++ i) sum = (sum + 1ll * ans[i] * a[i] % mod) % mod;
    sum = 1ll * sum * ksm(2, m) % mod * ksm(ksm(2, m) - 1, mod - 2) % mod;
    printf("%d\n", sum);
	return 0;
}

}


signed main() { return Legendgod::main(), 0; }

```
