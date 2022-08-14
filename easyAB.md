# 此文章~~借鉴~~抄袭于[https://www.luogu.com.cn/paste/zzmnwrb4](https://www.luogu.com.cn/paste/zzmnwrb4)

### 关于 $A + B$ 这道连大（cai）佬（niao）都做不（de）出的难（shui）题

这里~~我~~总结出了几种方法:

## 1.不是人（monkey）能写的。
```cpp
#include <iostream>
using namespace std;

long long a , b;

int main(void){
	cin.tie(0);
  	cout.tie(0);
	cin >> a >> b;
	cout << a + b;
	return 0;
}
```

## 用数学的方法：

```cpp
#include <iostream>
#include <cmath>
using namespace std;

long long a , b;

int main(void){
	cin >> a >> b;
	cout << (a + b) * ((long long)(abs(a - b)) + 1) / 2 - (a + b) * ((long long)(abs(a - b)) - 1) /  2;
	return 0;
}
```

## 最简单的树状数组
```cpp
#include <cstdio>
#define lowbit(x) (x) & (-x)
#define ll long long
using namespace std;

ll N , a , b;
ll qwq[5];

inline ll read(){
    ll x = 0;
	int f = 1;
    char ch = getchar();
    while(ch < '0' || ch > '9'){
        if(ch == '-')
            f = -1;
        ch = getchar();
    }
    while(ch >= '0' && ch <= '9'){
        x = (x << 1) + (x << 3) + (ch ^ 48);
        ch = getchar();
    }
    return x * f;
}

void add(int i , ll k){
	//第 i 位置上加上 k 
	while(i <= N){
		qwq[i] += k;
		i += lowbit(i);
	}
}

ll getsum(int i){
	//求 qwq[1 ~ i] 的和
	ll rrr = 0;
	while(i){
		rrr += qwq[i];
		i -= lowbit(i);
	}
	return rrr;
}

int main(void){
	N = 3;
	a = read();
	b = read();
	add(1 , a);
	add(2 , b);
	printf("%lld\n" , getsum(2));
}
```

## 有点短但很好理解的高精:
```cpp
#include <iostream>
#include <cstdio>
using namespace std;

struct QWQ{
	int s[5005]; //s[0] = len
	
	void read(){
		string in;
		cin >> in;
		s[0] = in.size();
		for(int i = 1;i <= s[0];i++)
			s[i] = in[s[0] - i] - '0';
	}
	
	void print(string end = ""){
		for(int i = s[0];i >= 1;i--)
			cout << s[i];
		cout << end;
	}
	
	QWQ operator + (QWQ &b){
		QWQ c;
		int len = max(s[0] , b.s[0]);
		int i = 1 , x = 0;
		for(;i <= len;i++){
			c.s[i] = s[i] + b.s[i] + x;
			x = c.s[i] / 10;
			c.s[i] %= 10;
		}
		if(x == 0)
			i--;
		else
			c.s[i] = x;
		c.s[0] = i;
		return c;
	}
	
	QWQ operator = (QWQ b){
		for(int i = 0;i <= b.s[0];i++)
			s[i] = b.s[i];
		return *this;
	}
};

int main(void){
	QWQ a , b , c;
	a.read();
	b.read();
	c = a + b;
	c.print();
}
```

## C艹语言
```cpp
#include <iostream>
#include <cmath>
#define QWQ long long
#define My_name_is_sb std
#define __ int
#define ___ main
#define ____ void
#define _____ return
#define ______ cin
#define _______ cout

QWQ awdrg , sefth;

__ ___(____){
	My_name_is_sb::______ >> awdrg >> sefth;
	My_name_is_sb::_______ << awdrg + sefth;
	_____ 0;
}
```

## 加点优化:
```cpp
#include <iostream>
#pragma GCC diagnostic error "-std=c++11"
#pragma GCC target("avx")
#pragma GCC optimize(1)
#pragma GCC optimize(2)
#pragma GCC optimize(3)
#pragma GCC optimize("Ofast")
#pragma GCC optimize("inline")
#pragma GCC optimize("-fgcse")
#pragma GCC optimize("-fgcse-lm")
#pragma GCC optimize("-fipa-sra")
#pragma GCC optimize("-ftree-pre")
#pragma GCC optimize("-ftree-vrp")
#pragma GCC optimize("-fpeephole2")
#pragma GCC optimize("-ffast-math")
#pragma GCC optimize("-fsched-spec")
#pragma GCC optimize("unroll-loops")
#pragma GCC optimize("-falign-jumps")
#pragma GCC optimize("-falign-loops")
#pragma GCC optimize("-falign-labels")
#pragma GCC optimize("-fdevirtualize")
#pragma GCC optimize("-fcaller-saves")
#pragma GCC optimize("-fcrossjumping")
#pragma GCC optimize("-fthread-jumps")
#pragma GCC optimize("-funroll-loops")
#pragma GCC optimize("-fwhole-program")
#pragma GCC optimize("-freorder-blocks")
#pragma GCC optimize("-fschedule-insns")
#pragma GCC optimize("inline-functions")
#pragma GCC optimize("-ftree-tail-merge")
#pragma GCC optimize("-fschedule-insns2")
#pragma GCC optimize("-fstrict-aliasing")
#pragma GCC optimize("-fstrict-overflow")
#pragma GCC optimize("-falign-functions")
#pragma GCC optimize("-fcse-skip-blocks")
#pragma GCC optimize("-fcse-follow-jumps")
#pragma GCC optimize("-fsched-interblock")
#pragma GCC optimize("-fpartial-inlining")
#pragma GCC optimize("no-stack-protector")
#pragma GCC optimize("-freorder-functions")
#pragma GCC optimize("-findirect-inlining")
#pragma GCC optimize("-fhoist-adjacent-loads")
#pragma GCC optimize("-frerun-cse-after-loop")
#pragma GCC optimize("inline-small-functions")
#pragma GCC optimize("-finline-small-functions")
#pragma GCC optimize("-ftree-switch-conversion")
#pragma GCC optimize("-foptimize-sibling-calls")
#pragma GCC optimize("-fexpensive-optimizations")
#pragma GCC optimize("-funsafe-loop-optimizations")
#pragma GCC optimize("inline-functions-called-once")
#pragma GCC optimize("-fdelete-null-pointer-checks")
#include <bits/stdc++.h>
#include <algorithm>
#include <bitset>
#include <cctype>
#include <cerrno>
#include <cfloat>
#include <ciso646>
#include <climits>
#include <clocale>
#include <cmath>
#include <complex>
#include <csignal>
#include <csetjmp>
#include <cstdarg>
#include <cstddef>
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <ctime>
#include <cwchar>
#include <cwctype>
#include <deque>
#include <exception>
#include <fstream>
#include <functional>
#include <limits>
#include <list>
#include <locale>
#include <map>
#include <memory>
#include <new>
#include <numeric>
#include <iomanip>
#include <ios>
#include <iosfwd>
#include <iostream>
#include <istream>
#include <iterator>
#include <ostream>
#include <queue>
#include <set>
#include <sstream>
#include <stack>
#include <stdexcept>
#include <streambuf>
#include <string>
#include <typeinfo>
#include <utility>
#include <valarray>
#include <vector>
using namespace std;

long long a , b;

inline long long read(){
    long long x = 0;
	int f = 1;
    char ch = getchar();
    while(ch < '0' || ch > '9'){
        if(ch == '-')
            f = -1;
        ch = getchar();
    }
    while(ch >= '0' && ch <= '9'){
        x = (x << 1) + (x << 3) + (ch ^ 48);
        ch = getchar();
    }
    return x * f;
}

void write(long long x) {
    if(x < 0) {
        putchar('-'); 
        x = -x;
    }
    if(x > 9) write(x / 10);
    putchar(x % 10 + '0');
}

int main(void){
	a = read();
	b = read();
	write(a + b);
	return 0;
}
```

## 打标（预处理）:
```cpp
#include <iostream>
using namespace std;

int da_biao[20000][20000];
int a , b;

void init(){
	for(int i = 0;i < 20000;i++)
		for(int j = 0;j < 20000;j++)
			da_biao[i][j] = i + j;
}

int main(void){
	init();
	cin.tie(0);
	cout.tie(0);
	cin >> a >> b;
	cout << da_biao[a][b];
	return 0;
}
```
## 暴力枚举:
```cpp
#include <cstdio>
using namespace std;

int a, b;

int main() {
    scanf("%d%d", &a , &b);
    for (int i = 0;i <= 100000000;i++){
    	if (a + b == i){
			printf("%d\n", i);
			break;
		}
	}	
    return 0;
} 
```

## 超级优化：
```cpp
#include <iostream>
#include <ctime>
using namespace std;

int st = clock();
int a , b;

int main(void){
    cin >> a >> b;
    while(clock() - st < 999000);
    cout << a + b;
    return 0;
}
```
![AC](https://tdog.oss-cn-hangzhou.aliyuncs.com/together-h5/8h3tQbtJMts8Antk7GPpDCJW2ff3jCxB.png?x-oss-process=image/resize,w_400,limit_0/auto-orient,1)

## STL(queue) + qpow:
```cpp
#include <iostream>
#include <queue>
#include <cmath>
using namespace std;

long long a;
queue <long long> q;

inline long long qpow(long long a , int b){
    long long s = 1;
    while(b){
		if(b & 1)
			s = s * a;
		a = a * a;
		b >>= 1;
	}
    return s;
}

int main(void){
	scanf("%lld" , &a);
	q.push(qpow(a , 1));
	scanf("%lld" , &a);
	q.push(q.front() + qpow(a , 1));
	q.pop();
	printf("%lld\n" , q.front());
}
```

## 二分递归:
```cpp
#include <iostream>
#include <cmath>
using namespace std;

long long a , b , ans = -0x7ffffff;

void digui(long long l , long long r){
	long long mid = (l + r) >> 1;
	if(abs(mid - a - b) < 1)
		ans = mid;
	else if(mid < (a + b))
		digui(mid + 1 , r);
	else
		digui(l , mid - 1);
}

int main(void){
	cin.tie(0);
	cin >> a >> b;
	digui(1 , a + b + 1);
	printf("%d\n" , ans);
}
```

## 位运算：
```cpp
#include <cstdio>

long long m , n;

int main(void){
    scanf("%lld%lld", &m, &n);
    long long u = m & n;
    long long v = m ^ n;
    while (u) {
        long long s = v;
        long long t = u << 1;
        u = s & t;
        v = s ^ t;
    }
    printf("%lld\n", v);
}
```