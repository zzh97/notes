### Easy

#### 7. Reverse Integer

##### Problem Description

> Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
>
> 给你一个 32 位的有符号整数 `x` ，返回将 `x` 中的数字部分反转后的结果。
>
> 如果反转后整数超过 32 位的有符号整数的范围 `[−231, 231 − 1]` ，就返回 0。
>
> 
>
> **Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**
>
> **假设环境不允许存储 64 位整数（有符号或无符号）。**
>
> 
>
> **Example 1:**
>
> ```
> Input: x = 123
> Output: 321
> ```
>
> **Example 2:**
>
> ```
> Input: x = -123
> Output: -321
> ```
>
> **Example 3:**
>
> ```
> Input: x = 120
> Output: 21
> ```
>
> **Example 4:**
>
> ```
> Input: x = 0
> Output: 0
> ```
>
> **Constraints:**
>
> * ` -231 <= x <= 231 - 1`



##### Javascript

```
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    if (x === 0) {
        return 0
    }
    else if (x > 0) {
        x = x.toString()
        let arr = x.split('')
        let newArr = arr.reverse()
        let str = arr.join('')
        let y = parseInt(str)
        if (y > Math.pow(2, 31) - 1) {
          return 0
        }
        return y
    }
    else {
        x = Math.abs(x)
        x = x.toString()
        let arr = x.split('')
        let newArr = arr.reverse()
        let str = arr.join('')
        let y = parseInt(str)
        if (y > Math.pow(2, 31)) {
          return 0
        }
        return -y
    }
};
```



##### Python3

```
class Solution:
    def reverse(self, x: int) -> int:
        if x == 0 :
            return 0
        
        elif x > 0 :
            s = str(x)
            arr = list (s)
            arr.reverse()
            y = "".join(arr)
            y = int (y)
            if y > pow(2,31)-1:
                return 0
            return y

        else :
            x = abs(x)
            s = str(x)
            arr = list (s)
            arr.reverse()
            y = "".join(arr)
            y = int (y)
            if y > pow(2,31):
                return 0
            return -y
```

```
class Solution:
    def reverse(self, x: int) -> int:
        y = 0
        b = 1
        if x < 0:
            x = abs(x)
            b = -1
        while x != 0:
            if y > (pow(2,31)-1)/10 :
                return 0 
            y = y * 10 + x % 10
            x = int (x / 10)
        return b*y
```



##### C

```
int reverse(int x){
	int y = 0;
	while (x != 0) {
		if (abs(y) > INT_MAX / 10) {
			return 0;
		}
		y = y * 10 + x % 10;
		x /= 10;
	}
    return y;
}
```



##### C++

```
class Solution {
public:
    int reverse(int x) {
        int y = 0;
        while (x != 0) {
            if (abs(y) > INT_MAX / 10) {
				return 0;
			}
			y = y * 10 + x % 10;
			x /= 10;
        }
        return y;
    }
};
```



#### 121. Best Time to Buy and Sell Stock

>You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.
>
>You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.
>
>Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
>
>给定一个数组`prices`，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。
>
>你只能选择**某一天**买入这只股票，并选择在**未来的某一个不同的日子**卖出该股票。设计一个算法来计算你所能获取的最大利润。
>
>返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。
>
>
>
>**Example 1:**
>
>```
>Input: prices = [7,1,5,3,6,4]
>Output: 5
>Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
>Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
>```
>
>**Example 2:**
>
>```
>Input: prices = [7,6,4,3,1]
>Output: 0
>Explanation: In this case, no transactions are done and the max profit = 0.
>```
>**Constraints**
>
>*  `1 <= prices.length <= 10^5 `
>*  `0 <= prices[i] <= 10^4 `





```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        def next (i):
            j = i + 1
            M = 0
            while 1:
                if j >= len(prices):
                    return M
                if prices[j] > M:
                    M = prices[j]
                else:
                    j = j + 1
        
        def nice ():
            money = 0
            i = 0
            while i < len(prices)-1:
                temp = next(i) - prices[i]
                if temp > money:
                    money = temp
                i = i + 1
            return money

        return nice ()
```

