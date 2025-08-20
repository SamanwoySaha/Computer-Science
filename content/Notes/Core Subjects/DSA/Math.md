---
title: Math
draft: false
tags: 
date: 19-Aug-2025
---
# Problems
### check if a num is prime or not
```c++
bool isPrime(int n) {
	if (n == 1) return false;
	
	for (int i=2; i*i<=n; i++) {
		if (n % i == 0) 
			return false;
	}
	return true;
}
```

```python
def isPrime(n):
   if n == 1:
       return False
   
   i = 2
   while i * i <= n:
       if n % i == 0:
           return False
       i += 1
   return True
```
### print all prime factors of a number
```cpp
bool isPrime(int n) {
	if (n == 1) return false;
	
	for (int i=2; i*i<=n; i++) {
		if (n % i == 0) 
			return false;
	}
	return true;
}

vector<int> func(int n) {
	vector<int> factors;
	
	// brute force O(n*sqrt(n)) O(1)
	for (int i=2; i<=n; i++) {
		if (n % i == 0) {
			if (isPrime(i)) {
				factors.push_back(i);
			}
		}
	}
	
	// better O(sqrt(n) * 2 * sqrt(n)) O(1)
	for (int i=1; i*i<=n; i++) {
		if (n % i == 0) {
			if (isPrime(i)) 
				factors.push_back(i);
			if ((n / i != i) && prime(n/i))
				factors.push_back(n/i);
		}
	}
	
	// better O(nlogn) O(1)
	for (int i=2; i<=n; i++) {
		if (n % i == 0) {
			factors.push_back(i);
			while (n % i == 0) 
				n = n / i;
		}
	}
	
	// optimal O(sqrt(n)logn) O(1)
	for (int i=2; i<=sqrt(n); i++) {
		if (n % i == 0) {
			factors.push_back(i);
			while (n % i == 0) 
				n = n / i;
		}
	}
	if (n != 1) 
		factors.push_back(n);
}

// another way to print with power of prime factor
void primeFact(int n) {
	for (int i=2; i*i<=n; i++) {
		if (n % i == 0) {
			int cnt = 0;
			while (n % i == 0) {
				cnt++;
				n /= i;
				cout << i << "^" << cnt << endl;
			}
		}
		if (n > 1) {
			cout << n << "^" << 1 << endl;
		}
	}
}
```

```python
import math

def isPrime(n):
   if n == 1:
       return False
   
   i = 2
   while i * i <= n:
       if n % i == 0:
           return False
       i += 1
   return True

def func(n):
   factors = []
   
   # brute force O(n*sqrt(n)) O(1)
   for i in range(2, n + 1):
       if n % i == 0:
           if isPrime(i):
               factors.append(i)
   
   # better O(sqrt(n) * 2 * sqrt(n)) O(1)
   i = 1
   while i * i <= n:
       if n % i == 0:
           if isPrime(i):
               factors.append(i)
           if (n // i != i) and prime(n // i):
               factors.append(n // i)
       i += 1
   
   # better O(nlogn) O(1)
   for i in range(2, n + 1):
       if n % i == 0:
           factors.append(i)
           while n % i == 0:
               n = n // i
   
   # optimal O(sqrt(n)logn) O(1)
   i = 2
   while i <= math.sqrt(n):
       if n % i == 0:
           factors.append(i)
           while n % i == 0:
               n = n // i
       i += 1
   if n != 1:
       factors.append(n)

# another way to print with power of prime factor
def primeFact(n):
   i = 2
   while i * i <= n:
       if n % i == 0:
           cnt = 0
           while n % i == 0:
               cnt += 1
               n //= i
               print(f"{i}^{cnt}")
       i += 1
   if n > 1:
       print(f"{n}^1")
```
### All Divisors of a Number
```cpp
vector<int> func(int n) {
	vector<int> factors;
	
	// brute force O(n) O(1)
	for (int i=1; i<=n; i++) {
		if (n % i == 0)
			factors.push_back(i);
	}	
	
	// better O(sqrt(n)) O(1)
	for (int i=1; i*i<=n); i++) {
		if (n % i == 0)
			factors.push_back(i);
			if (n/i != i) 
				factors.push_back(i);
	}
}
```

```python
def func(n: int) -> list[int]:
    factors = []

    # brute force O(n) O(1)
    for i in range(1, n + 1):
        if n % i == 0:
            factors.append(i)

    # better O(sqrt(n)) O(1)
    i = 1
    while i * i <= n:
        if n % i == 0:
            factors.append(i)
            if n // i != i:
                factors.append(i)
        i += 1

```
### [sieve of eratosthenes](https://leetcode.com/problems/count-primes/)
![image.png](image%2096.png)

```cpp
bool isPrime(int n) {
	if (n == 1) return false;
	
	for (int i=2; i*i<=n; i++) {
		if (n % i == 0) 
			return false;
	}
	return true;
}

// brute O(n*sqrt(n)) O(1)
void primes(int n) {
	for (int i=2; i<=n; i++) {
		if (isPrime(i)) {
			cout << i;
		}
	}
}

// optimal 
static const int maxN = 5e6;
bool is_Prime[maxN+1];

void sieve_of_eratosthenes() {
	for (int i=2; i<= maxN; i++) 
		is_Prime[i] = true;
	is_Prime[0] = is_Prime[1] = false;
	
	for (int i=2; i*i<=maxN; i++) {
		if (is_Prime[i]) {
			// O(n) O(1)
			for (int j=2*i; j<=maxN; j+=i) {
				// O(nlog(logn)) O(1) prime harmonic series
				for (int j=i*i; j<=maxN; j+=i) {
					is_Prime[j] = false;
				}
		}
	}
}

int countPrimes(int n) {
	sieve_of_eratosthenes();
	int count = 0;

  for (int i=2; i<n; i++) {
	  if (is_Prime[i]) 
		  count++;
  }
  return count;
}
```

```python
def isPrime(n: int) -> bool:
    if n == 1:
        return False

    i = 2
    while i * i <= n:
        if n % i == 0:
            return False
        i += 1
    return True


# brute O(n*sqrt(n)) O(1)
def primes(n: int):
    for i in range(2, n + 1):
        if isPrime(i):
            print(i, end='')


# optimal
maxN = int(5e6)
is_Prime = [False] * (maxN + 1)


def sieve_of_eratosthenes():
    for i in range(2, maxN + 1):
        is_Prime[i] = True
    is_Prime[0] = False
    is_Prime[1] = False

    i = 2
    while i * i <= maxN:
        if is_Prime[i]:
            # O(n) O(1)
            j = 2 * i
            while j <= maxN:
                j += i
            # O(nlog(logn)) O(1) prime harmonic series
            j = i * i
            while j <= maxN:
                is_Prime[j] = False
                j += i
        i += 1


def countPrimes(n: int) -> int:
    sieve_of_eratosthenes()
    count = 0
    for i in range(2, n):
        if is_Prime[i]:
            count += 1
    return count

```
### Smallest prime factor
```cpp
static const int maxN = 5e6;
bool spf[maxN+1];

void sieve_of_eratosthenes() {
	for (int i=0; i<= maxN; i++) 
		spf[i] = i;
	
	for (int i=2; i*i<=maxN; i++) {
		if (spf[i] == i) {
			// O(nlog(logn)) O(1) prime harmonic series
			for (int j=i*i; j<=maxN; j+=i) {
				if (spf[j] == j)
				spf[j] = i;
			}
		}
	}
}

int countSpf(vector<int> queries) {
	sieve_of_eratosthenes();
	
	for (int i=0; i<queries.size(); i++) {
		int n = queries[i];
		
		while (n != 1) {
			cout << spf[i];
			n /= spf[n];
		} 
	}
}
```

```python
maxN = int(5e6)
spf = [0] * (maxN + 1)


def sieve_of_eratosthenes():
    for i in range(maxN + 1):
        spf[i] = i

    i = 2
    while i * i <= maxN:
        if spf[i] == i:
            # O(nlog(logn)) O(1) prime harmonic series
            j = i * i
            while j <= maxN:
                if spf[j] == j:
                    spf[j] = i
                j += i
        i += 1


def countSpf(queries: list[int]):
    sieve_of_eratosthenes()

    for i in range(len(queries)):
        n = queries[i]

        while n != 1:
            print(spf[i], end='')
            n //= spf[n]

```
### binary exponentiation
```cpp
int binary_exponentiation(int a, int b, int mod) {
	int ans = 1;
	while (b) {
		if (b % 2 == 1) 
			ans = (ans * a) % mod;
		a = (a * a) % mod;
		b /= 2;
	}
	return ans;
}
```

```python
def binary_exponentiation(a: int, b: int, mod: int) -> int:
    ans = 1
    while b:
        if b % 2 == 1:
            ans = (ans * a) % mod
        a = (a * a) % mod
        b //= 2
    return ans
```
### nCr    
```cpp
int C (int n, int k) {
	int ans = 1;

	if (k > n - k) k = n - k;

	for (int i=1; i<=k; i++) {
		ans *= (n - i + 1);
		ans /= i;
	}

	return ans;
}
```

```python
def C(n: int, k: int) -> int:
    ans = 1

    if k > n - k:
        k = n - k

    for i in range(1, k + 1):
        ans *= (n - i + 1)
        ans //= i

    return ans

```
    
### [Find square root of a number in log n](https://takeuforward.org/binary-search/finding-sqrt-of-a-number-using-binary-search/)
```cpp
int floorSqrt(int n) {
	int ans = 0;

	// brute force O(n) O(1)
	for (long long i = 1; i <= n; i++) {
		long long val = i * i;
		if (val <= n * 1ll) {
			ans = i;
		} else {
			break;
		}
	}
	return ans;

	// optimal (built-in sqrt()) O(logn) O(1)
	int ans = sqrt(n);
	return ans;

	// optimal O(logn) O(1)
	int low = 1, high = n;
	//Binary search on the answers:
	while (low <= high) {
		long long mid = (low + high) / 2;
		long long val = mid * mid;
		if (val <= (long long)(n)) {
			//eliminate the left half:
			low = mid + 1;
		}
		else {
			//eliminate the right half:
			high = mid - 1;
		}
	}
	return high;
}

```

```python
import math

def floorSqrt(n: int) -> int:
    ans = 0

    # brute force O(n) O(1)
    i = 1
    while i <= n:
        val = i * i
        if val <= n:
            ans = i
        else:
            break
        i += 1
    return ans

    # optimal (built-in sqrt()) O(logn) O(1)
    ans = int(math.sqrt(n))
    return ans

    # optimal O(logn) O(1)
    low, high = 1, n
    while low <= high:
        mid = (low + high) // 2
        val = mid * mid
        if val <= n:
            low = mid + 1
        else:
            high = mid - 1
    return high

```
### [Find the Nth root of a number using binary search](https://takeuforward.org/data-structure/nth-root-of-a-number-using-binary-search/)
```cpp
// brute force O(m) O(1) (m = given num)
// Power exponential method:
long long func(int b, int exp) {
	long long  ans = 1;
	long long base = b;
	while (exp > 0) {
		if (exp % 2) {
			exp--;
			ans = ans * base;
		}
		else {
			exp /= 2;
			base = base * base;
		}
	}
	return ans;
}

int NthRoot(int n, int m) {
	//Use linear search on the answer space:
	for (int i = 1; i <= m; i++) {
		long long val = func(i, n);
		if (val == m * 1ll) return i;
		else if (val > m * 1ll) break;
	}
	return -1;
}

// optimal O(logn) O(1)
//return 1, if == m:
//return 0, if < m:
//return 2, if > m:
int func(int mid, int n, int m) {
	long long ans = 1;
	for (int i = 1; i <= n; i++) {
		ans = ans * mid;
		if (ans > m) return 2;
	}
	if (ans == m) return 1;
	return 0;
}

int NthRoot(int n, int m) {
	//Use Binary search on the answer space:
	int low = 1, high = m;
	while (low <= high) {
		int mid = (low + high) / 2;
		int midN = func(mid, n, m);
		if (midN == 1) {
			return mid;
		}
		else if (midN == 0) low = mid + 1;
		else high = mid - 1;
	}
	return -1;
}

```

```python
# brute force O(m) O(1) (m = given num)
# Power exponential method:
def func_pow(b: int, exp: int) -> int:
    ans = 1
    base = b
    while exp > 0:
        if exp % 2:
            exp -= 1
            ans = ans * base
        else:
            exp //= 2
            base = base * base
    return ans


def NthRoot_linear(n: int, m: int) -> int:
    for i in range(1, m + 1):
        val = func_pow(i, n)
        if val == m:
            return i
        elif val > m:
            break
    return -1


# optimal O(logn) O(1)
# return 1 if == m
# return 0 if < m
# return 2 if > m
def func_check(mid: int, n: int, m: int) -> int:
    ans = 1
    for _ in range(1, n + 1):
        ans = ans * mid
        if ans > m:
            return 2
    if ans == m:
        return 1
    return 0


def NthRoot_binary(n: int, m: int) -> int:
    low, high = 1, m
    while low <= high:
        mid = (low + high) // 2
        midN = func_check(mid, n, m)
        if midN == 1:
            return mid
        elif midN == 0:
            low = mid + 1
        else:
            high = mid - 1
    return -1

```
### https://leetcode.com/problems/powx-n/
```cpp
// brute force O(n)
ans = 1;
for (int i=1; i<=n; i++) {
	ans *= n;
}

// binary exponentiation O(logn) 
double myPow(double x, int n) {
	if (x == 0) return 0;
	if (n == 0) return 1;

	double ans = 1;
	long long p = abs((long long)n);

	while(p) {
		if (p & 1)
			ans *= x;
		x *= x;
		p /= 2;
	}
	return n >= 0 ? ans : 1 / ans;
}
```

```python
# brute force O(n)
ans = 1
for i in range(1, n + 1):
    ans *= n


# binary exponentiation O(logn)
def myPow(x: float, n: int) -> float:
    if x == 0:
        return 0
    if n == 0:
        return 1

    ans = 1
    p = abs(int(n))

    while p:
        if p & 1:
            ans *= x
        x *= x
        p //= 2

    return ans if n >= 0 else 1 / ans

```