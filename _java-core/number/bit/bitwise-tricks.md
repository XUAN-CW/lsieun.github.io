---
title: "Bitwise Tricks"
sequence: "102"
---

Some of these problems include:

- Checking for odd and even numbers in a sequence
- Counting set bits in an integer
- Multiplying two numbers using bitwise operators (Russian Peasant)
- Generating n-bit Gray Codes
- Detecting if two integers have opposite signs
- Adding 1 to a given number

## Common Bitwise Tricks

### AND: Count set bits

Write a Java program to count the number of bits set to `1` (set bits) of an integer.

```java
class CountSetBit {
    private static int helper(int n) {
        int count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }
 
    public static void main(String[] args) {
        int number = 125;
        System.out.println("SetBit Count is : " + helper(number));
    }
}
```

`n&(n-1)` 这个操作是算法中常见的，作用是消除数字 `n` 的二进制表示中的最后一个 `1`。

{:refdef: style="text-align: center;"}
![](/assets/images/java/number/bitwise-n-and-n-minus-1.png)
{:refdef}

### XOR: Single Number

Find the element in an array that is not repeated.

Input: `nums = { 4, 1, 2, 9, 1, 4, 2 }`

Output: `9`

```java
class SingleNumber {
    private static int singleNumber(int[] nums) {
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }
        return xor;
    }
 
    public static void main(String[] args) {
        int[] nums = {4, 1, 2, 9, 1, 4, 2};
        System.out.println("Element appearing one time is " + singleNumber(nums));
    }
}
```

This solution relies on the following logic:

- If we take XOR of zero and some bit, it will return that bit: `a ^ 0 = a`
- If we take XOR of two same bits, it will return 0: `a ^ a = 0`
- For n numbers, the below math can be applied: `a ^ b ^ a = (a ^ a) ^ b = 0 ^ b = b`

### Left Shift: Get First Set Bit

Given an integer, find the position of the first set-bit (1) from the right.

Input: `n = 18`

18 in binary = `0b10010`

Output: `2`

```java
class FirstSetBitPosition {
    private static int helper(int n) {
        if (n == 0) {
            return 0;
        }
 
        int k = 1;
 
        while (true) {
            if ((n & (1 << (k - 1))) == 0) {
                k++;
            } else {
                return k;
            }
        }
    }
 
    public static void main(String[] args) {
        System.out.println("First setbit position for number: 18 is -> " + helper(18));
        System.out.println("First setbit position for number: 5 is -> " + helper(5));
        System.out.println("First setbit position for number: 32 is -> " + helper(32));
    }
}
```

## Characters

```text
'A': 01000001 (65)
'a': 01100001 (97)
' ': 00100000 (32)
'_': 01011111 (95)
```

### OR: All to lowercase

Use OR (`|`) and space bar coverts English characters to lowercase:

```text
('a' | ' ') == 'a'
('A' | ' ') == 'a'
```

### AND: All to uppercase

Use AND (`&`) and underline coverts English to uppercase:

```text
('b' & '_') == 'B'
('B' & '_') == 'B'
```

### XOR: Switch case

Use XOR (`^`) and space bar for English characters case exchange:

```text
('d' ^ ' ') == 'D'
('D' ^ ' ') == 'd'
```

You can convert any character, `ch`, to the opposite case using `ch ^= 32`.

## Number

### XOR: 符号判断

Determine if the sign of two numbers are different:

```text
int x = -1, y = 2;
bool f = ((x ^ y) < 0); // true

int x = 3, y = 2;
bool f = ((x ^ y) < 0); // false
```

### AND: 偶数判断

This one tests your knowledge of how **AND** works and how even/odd numbers differ in binary.

```text
(x & 1 ) == 0
```

### AND: 指数判断

Determine if a number is an exponent of 2.
If a number is an exponent of 2, its binary representation must contain only one 1:

```text
2^0 = 1 = 0b0001
2^1 = 2 = 0b0010
2^2 = 4 = 0b0100
```

If you use the bit operation technique, it is very simple (note the precedence of the operator, the parentheses cannot be omitted):

```text
bool isPowerOfTwo(int n) {
    if (n <= 0) return false;
    return (n & (n - 1)) == 0;
}
```

### 最小指数：位移

给定一个数，找出大于或等于它的最小的2的幂次方：

```java
public class HelloWorld {

    private static int getMinPowOfTwo(int c) {
        int n = c - 1;
        n |= n >>> 1;
        n |= n >>> 2;
        n |= n >>> 4;
        n |= n >>> 8;
        n |= n >>> 16;
        return n + 1;
    }

    public static void main(String[] args) {
        int n = 100;
        int minPowOfTwo = getMinPowOfTwo(n);
        System.out.println("minPowOfTwo = " + minPowOfTwo);
    }
}
```

这段代码是一个常见的用于计算大于等于给定数字 c 的最接近的 2 的幂次方的方法。
具体来说，它会将 n 初始化为 c - 1，然后通过连续的按位或操作（>>> 表示无符号右移）来确保 n 的所有位都被设置为从最高位到最低位的所有位的“1”。
这样一来，n 最终的值将是大于等于 c 的最接近的 2 的幂次方。

```text
// n |= n >>> 1
00100000000000000000000000000000    ---> n
00010000000000000000000000000000    ---> n >>> 1
00110000000000000000000000000000    ---> n | (n >>> 1)

// n |= n >>> 2
00110000000000000000000000000000
00001100000000000000000000000000
00111100000000000000000000000000

// n |= n >>> 4
00111100000000000000000000000000
00000011110000000000000000000000
00111111110000000000000000000000

// n |= n >>> 8
00111111110000000000000000000000
00000000001111111100000000000000
00111111111111111100000000000000

// n |= n >>> 16
00111111111111111100000000000000
00000000000000000011111111111111
00111111111111111111111111111111

// n + 1
01000000000000000000000000000000
```

### XOR: 是否相等

```java
public class HelloWorld {
    static int getAverage(int x, int y) {
        // Calculate the average
        // Floor value of (x + y) / 2
        int avg = (x & y) + ((x ^ y) >> 1);

        return avg;
    }

    public static void main(String[] args) {
        int x = 10, y = 20;
        System.out.print(getAverage(x, y));
    }
}
```

```java
public class HelloWorld {
    static void areSame(int a, int b) {
        if ((a ^ b) != 0) {
            System.out.print("Not Same");
        }
        else {
            System.out.print("Same");
        }
    }

    public static void main(String[] args) {
        areSame(10, 20);
    }
}
```

### 平均数

Fast average of two numbers

```java
public class HelloWorld {
    static int floorAvg(int x, int y) {
        return (x + y) >> 1;
    }

    public static void main(String[] args) {
        int x = 10, y = 20;
        System.out.print(floorAvg(x, y));
    }
}
```

### OR: Number of Flips

Write a program that takes 3 integers and uses the lowest number of flips to make the sum of the first two numbers equal to the third.
The program will return the number of flips required.

> A flip is changing one single bit to the opposite value ie. `1 --> 0` or `0 --> 1`.

Input: `a = 2`, `b = 6`, `c = 5`

Output: `3`

```java
class MinFlips {
    private static int helper(int a, int b, int c) {
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            int bitC = ((c >> i) & 1);
            int bitA = ((a >> i) & 1);
            int bitB = ((b >> i) & 1);
 
            if ((bitA | bitB) != bitC) {
                ans += (bitC == 0) ? (bitA == 1 && bitB == 1) ? 2 : 1 : 1;
            }
        }
        return ans;
    }
 
    public static void main(String[] args) {
        int a = 2;
        int b = 6;
        int c = 5;
        System.out.println("Min Flips required to make two numbers equal to third is : " + helper(a, b, c));
    }
}
```

### Show Off

The following three operations just Show off. No practical use. We just know it.

Swap two Numbers:

```text
int a = 1, b = 2;
a ^= b;
b ^= a;
a ^= b;
// 现在 a = 2, b = 1
```

Plus one:

```text
int n = 1;
n = -~n;
// 现在 n = 2
```

Minus one:

```text
int n = 2;
n = ~-n;
// 现在 n = 1
```

## References

- [Some Useful Bit Manipulations](https://labuladong.gitbook.io/algo-en/iii.-algorithmic-thinking/commonbitmanipulation) [常用的位操作](https://labuladong.gitee.io/algo/4/28/108/)
