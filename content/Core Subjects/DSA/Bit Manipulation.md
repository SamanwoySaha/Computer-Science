---
title: Bit Manipulation
draft: false
tags: 
date: 19-Aug-2025
---
# Sources

1. https://en.wikipedia.org/wiki/Hacker%27s_Delight

# Theory

- How `int` Data type is stored in memory?
    
    ![image.png](image%2046.png)
    
    - When we declare an integer variable n and assign it the value 13, the computer needs to represent this value in its memory. Computers represent numbers in binary format, which is a base-2 numeral system ie. represented as combinations of 0s and 1s.
    - The decimal number 13 in binary representation is 1101. In many programming languages, the ‘int’ data type is stored using 32 bits, which means the binary representation of 13 would be padded with leading zeros to fit those 32 bits: 00000000 00000000 00000000 00001101.
    - Signed Representation
        - The leftmost bit in a binary representation of an integer is used as the signed bit.
        - The two’s complement notion is a popular notation for representing signed integers in binary.
        - In two's complement notation:
            - If the leftmost bit is 0, the number is positive.
            - If the leftmost bit is 1, the number is negative.
        - 
            
            ![](https://remnote-user-data.s3.amazonaws.com/dE3m4KsCmcyoqOCBWqIhW6BkOdAqLVWWPQX0RMxrJ-Ru6J02jpgfxDYj-0kV2URW_DFRM5zvDVg3ETrnSWGKGitCuD5LbGI-y_ku76EVlAAPlU8zhN58dvGSlIPRNncD.png)
            
        - This representation allows for both positive and negative integers to be represented using the same binary format.
        - 
            
            ![](https://remnote-user-data.s3.amazonaws.com/yTZEcOOtV--NeXMTondzI7eqb7ZLZ7CBpgglhAHvD5T29KYY1FYkPXarGlo0F5qFZS2WtuftJ60UPnjmjAm69ybtimKAuooyGHGENSmfkFkDVG67mHOx3UYOQz4xsfgB.png)
            
        - In two’s complement notation, the negation of a number is obtained by taking the two’s complement of its positive representation.
        - INT_MAX
            - In a 32-bit signed integer representation, the largest possible integer is where all 31 bits after the signed bit are set to 1.
            - 0111 1111 1111 1111 1111 1111 1111 1111 1111
                - = 1x231 + 1x230 + … + 1x21 + 1x20
                - = 231-1 (Often represented as INT_MAX)
            - If we try to represent a number larger than this in a signed 32-bit integer, we would encounter overflow, which means the value would wrap around to a negative number due to the way signed integer representations work in binary representation.
        - INT_MIN
            - In a 32-bit signed integer representation, the smallest possible integer, or INT_MIN, is represented as follows:
            - 1000 0000 0000 0000 0000 0000 0000 0000
                - = -231 (Often represented as INT_MIN)
            - If we try to represent a number smaller than this in a signed 32-bit integer, it would result in overflow, causing the value to wrap around to a positive number.
        - LONG LONG
            - Long long data type, represents a larger range of integers than int. The computer allocates more bits for its storage. In most systems, a long long typically uses 64 bits.
            - When you assign the value 13 to a long long variable, the computer allocates 64 bits to store this value in binary format. The binary representation of 13 is padded with leading zeros to fit these 64 bits: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00001101.
            - This allows long long variables to handle much larger integers compared to int, while still utilising the same binary representation principles for storage and interpretation.
- What is Binary Number?
    - A **binary number** is a number expressed in the base-2 numeral system or binary numeral system, it is a method of mathematical expression which uses only two symbols: typically "0" (zero) and "1" (one).
    - The binary number  $(a_k a_{k-1} \dots a_1 a_0)_2$  represents the number:
        - $(a_k a_{k-1} \dots a_1 a_0)_2 = a_k \cdot 2^k + a_{k-1} \cdot 2^{k-1} + \dots + a_1 \cdot 2^1 + a_0 \cdot 2^0.$
    - For instance the binary number $1101_2$ represents the number 13 :
        
        $$
        \begin{align} 1101_2 &= 1 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 \\ &= 1\cdot 8 + 1 \cdot 4 + 0 \cdot 2 + 1 \cdot 1 = 13 \end{align}
        $$
        
- How to represent signed and unsigned number in binary?
    - Positive integers (both signed and unsigned) are just represented with their binary digits, and negative signed numbers (which can be positive and negative) are usually represented with the [Two's complement](https://en.wikipedia.org/wiki/Two%27s_complement).
        
        ```cpp
        unsigned int unsigned_number = 13;
        assert(unsigned_number == 0b1101);
        
        int positive_signed_number = 13;
        assert(positive_signed_number == 0b1101);
        
        int negative_signed_number = -13;
        assert(negative_signed_number == 0b1111'1111'1111'1111'1111'1111'1111'0011);
        ```
        
- Benefit of using bit manipulation
    - CPUs are very fast manipulating those bits with specific operations. For some problems we can take these binary number representations to our advantage, and speed up the execution time. And for some problems (typically in combinatorics or dynamic programming) where we want to track which objects we already picked from a given set of objects, we can just use an large enough integer where each digit represents an object and depending on if we pick or drop the object we set or clear the digit.

# Bit Operators

- and `&`
    
    The bitwise AND operator compares each bit of its first operand with the corresponding bit of its second operand.      If both bits are 1, the corresponding result bit is set to 1. Otherwise, the corresponding result bit is set to 0.
    
    ```cpp
    n         = 01011000
    n-1       = 01010111
    --------------------
    n & (n-1) = 01010000
    ```
    
- or `|`
    
    The bitwise inclusive OR operator compares each bit of its first operand with the corresponding bit of its second operand.     If one of the two bits is 1, the corresponding result bit is set to 1. Otherwise, the corresponding result bit is set to 0.
    
    ```cpp
    n         = 01011000
    n-1       = 01010111
    --------------------
    n | (n-1) = 01011111
    ```
    
- not `~`
    
    The bitwise complement (NOT) operator flips each bit of a number, if a  bit is set the operator will clear it, if it is cleared the operator  sets it.
    
    ```cpp
    n         = 01011000
    --------------------
    ~n        = 10100111
    ```
    
    ![image.png](image%2047.png)
    
    ![image.png](image%2048.png)
    
- xor `^`
    
    The bitwise exclusive OR (XOR) operator compares each bit of its first  operand with the corresponding bit of its second operand.     If one bit is 0 and the other bit is 1, the corresponding result bit  is set to 1. Otherwise, the corresponding result bit is set to 0.
    
    ```cpp
    n         = 01011000
    n-1       = 01010111
    --------------------
    n ^ (n-1) = 00001111
    ```
    
- right shift `>>`
    
    ![image.png](image%2049.png)
    
- left shift `<<`
    
    ![image.png](image%2050.png)
    
    ![image.png](image%2051.png)
    

# Conversion

- Decimal to Binary
    
    ![image.png](image%2052.png)
    
    ```cpp
    // O(logn) O(logn)
    string convert2Binary(int n) {
    		res = "";
    		while (n > 1) {
    			if (n % 2 == 1) res += "1";
    			else res += "0";
    			n = n / 2;
    		}
    		res += "1";
    		reverse(res.begin(), res.end());
    		return res;
    }
    ```
    
- Binary to Decimal
    
    ![image.png](image%2053.png)
    
    ```cpp
    // O(n) O(1)
    int convert2Decimal (string x) {
    		int len = x.length;
    		int num = 0;
    		int p = 1;
    		
    		for (int i=len-1; i>=0; i--) {
    			if (x[i] == '1')
    				num += p;
    			p = p * 2;
    		}
    		return num;
    }
    ```
    
- 1's complement
    
    ![image.png](image%2054.png)
    
- 2's complement
    
    ![image.png](image%2055.png)
    
- Bitmask
    
    is the combination of bits used to represent subset
    
    ![image.png](image%2056.png)
    

# Properties

- a|b = ?
    - a|b→a⊕b + a&b
- a⊕(a&b) = ?
    - a⊕(a&b)→(a|b)⊕b
- b⊕(a&b) = ?
    - b⊕(a&b)→(a|b)⊕a
- (a&b)⊕(a|b) = ?
    - (a&b)⊕(a|b)→a⊕b
- Addition (a+b) = ?
    - a+b→a|b + a&b
    - a+b→a⊕b + 2(a&b)
- Subtraction (a-b) = ?
    - a-b→(a⊕(a&b))-((a|b)⊕a)
    - a-b→((a|b)⊕b)-((a|b)⊕a)
    - a-b→(a⊕(a&b))-(b⊕(a&b))
    - a-b→(([a|b)⊕b)-(b⊕(a&b](https://www.remnote.com/doc/cxjiRdEDGKPFLwHCe?isPin=false)))

# Problems

- swap two numbers without third variable
    
    ```cpp
    a  = a ^ b;
    b = a ^ b; // b = (a ^ b) ^ b
    a = a ^ b; // a = (a ^ b) ^ a
    ```
    
- sets the x-th bit in the number n
    
    `n | (1 << x)`
    
- toggle the x-th bit in the number n
    
    `n ^ (1 << x)`
    
- clears the x-th bit in the number n→
    
    `n & ~(1 << x)`
    
- Check if x-th bit is set or not
    
    `(n >> x) & 1 != 0` or `n & (1 << x) != 0`
    
- check if n is odd
    
    `n & 1 == 1`
    
- check if n is even
    
    `n & 1 == 0`
    
- Check if the number is divisible by a power of 2
    
    `n & ((1 << k) - 1) == 0`
    
- https://leetcode.com/problems/power-of-two/
    
    `n > 0 && (n & (n - 1)) == 0` 
    
- Clear the right-most set bit
    
    `n & (n-1)`
    
- count the number of set bits (Brian Kernighan's algorithm)
    
    ```cpp
    int countSetBits(int n) {
        int count = 0;
        while (n)
        {
            n = n & (n - 1);
            count++;
        }
        return count;
    }
    ```
    
- Count set bits upto  n
    
    ```cpp
    int countSetBits(int n) {
            int count = 0;
            while (n > 0) {
                int x = std::bit_width(n) - 1;
                count += x << (x - 1);
                n -= 1 << x;
                count += n + 1;
            }
            return count;
    } 
    ```
    
- clear all trailing ones
    
    $n ~\&~ (n + 1)$  . ex: $0011~0111_2 \rightarrow 0011~0000_2 .$
    
- set the last cleared bit
    
    $n ~|~ (n + 1)$  ex.: $0011~0101_2 \rightarrow 0011~0111_2 .$ 
    
- extract the last set bit
    
    $n ~\&~ -n$ . ex: $0011~0100_2 \rightarrow 0000~0100_2 .$ 
    
- https://leetcode.com/problems/single-number/
    
    ```cpp
    // brute force O(nlogm) O(m)
    1. store every num in map with freq
    
    // optimal O(n) O(1)
    xor all num
    ```
    
- https://leetcode.com/problems/single-number-iii/
    
    ![image.png](image%2057.png)
    
    ![image.png](image%2058.png)
    
    ![image.png](image%2059.png)
    
    ```cpp
    // brute force O(nlogm) O(m)
    1. store every num in map with freq
    
    // optimal O(n) O(1)
    vector<int> singleNumber(vector<int>& nums) {
        long xorr = 0;
        for (auto n: nums) 
            xorr ^= n;
        
        long rightMostBit = (xorr & (xorr - 1)) ^ xorr;
        int buc1 = 0, buc2 = 0;
    
        for (auto n: nums) {
            if (n & rightMostBit) 
                buc1 ^= n;
            else
                buc2 ^= n;
        }
        return {buc1, buc2};
    }
    ```
    
- k times multiply / divide by 2
    
     `n << k`   or,  `n >> k`
    
- https://leetcode.com/problems/minimum-bit-flips-to-convert-number/
    
    ![image.png](image%2060.png)
    
    ![image.png](image%2061.png)
    
    ```cpp
    int minBitFlips(int start, int goal) {
    		if (start == goal) return 0; 
        int ans = start ^ goal;
        int count = 0;
        
        // brute force O(31) O(1)
        for (int i=0; i<=31; i++) {
            if (ans & (1 << i)) 
                count++;
        }
        return count;
        
        // better O(log(start^goal)) O(1)
        while (ans > 1) {
            if (ans & 1) count++;
            ans /= 2;
        }
        count++;
        return count;
    }
    ```
    
- https://leetcode.com/problems/divide-two-integers/
    
    ```cpp
    int divide(int dividend, int divisor) {
        if (dividend == divisor) return 1;
    
        int sign = 1; 
        if ((dividend >= 0 && divisor < 0) || (dividend < 0 && divisor > 0)) 
            sign = -1; 
    
        long long n = abs((long long)dividend);  
        long long d = abs((long long)divisor);
        
        // brute force O(n) O(1)
        long long quotient = 0, count = 0;
    		
        while (quotient + d <= n) {
            quotient += d;
            count++;
        }
        return count*sign;
        
        // optimal O((logn)^2) O(1)
        long long quotient = 0;
        while (n >= d) {
            long long count = 0;
            while (n >= (d << (count + 1))) 
                count++;
            quotient += (1LL << count);
            n -= (d << count);
        }
    
        if (quotient > INT_MAX) 
            return sign == 1 ? INT_MAX : INT_MIN;
    
        return quotient * sign;
    }
    ```
    
- Find xor of numbers from 1 to N
    
    ![image.png](image%2062.png)
    
    ![image.png](image%2063.png)
    
    ```cpp
    // brute force O(n) O(1)
    xor all num
    
    // optimal O(1) O(1)
    int xor1ton(int n) {
    	if (n % 4 == 1) return 1;
    	else if (n % 4 == 2) return n+1;
    	else if (n % 4 == 3) return 0;
    	else return n;
    }
    ```
    
- Find xor of numbers from L to R
    
    ![image.png](image%2062.png)
    
    ![image.png](image%2063.png)
    
    ```cpp
    // brute force O(r-l+1) O(1)
    xor all num
    
    // optimal O(1) O(1)
    int xor1ton(int n) {
    	if (n % 4 == 1) return 1;
    	else if (n % 4 == 2) return n+1;
    	else if (n % 4 == 3) return 0;
    	else return n;
    }
    
    int xorltor(int l, int r) {
    	return xor1ton(l-1) ^ xor1ton(r);
    }
    ```