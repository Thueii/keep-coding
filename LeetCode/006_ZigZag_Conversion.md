# Z 字形变换

Link => [Z 字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)

**题目：将一个给定字符串 s 根据给定的行数 numRows ，以从上往下、从左到右进行 Z 字形排列。比如输入字符串为 "PAYPALISHIRING" 行数为 3 时，排列如下：
**
```
P   A   H   N
A P L S I I G
Y   I   R
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："PAHNAPLSIIGYIR"。请你实现这个将字符串进行指定行数变换的函数：
```
string convert(string s, int numRows);
```
>示例1：<br />
>输入：s = "PAYPALISHIRING", numRows = 3<br />
>输出："PAHNAPLSIIGYIR"<br />
> 
> 示例 2：<br />
```
输入：s = "PAYPALISHIRING", numRows = 4
输出："PINALSIGYAHRPI"
解释：
P     I    N
A   L S  I G
Y A   H R
P     I

``` 
> 示例 3：<br />
>输入：s = "A", numRows = 1<br />
>输出："A"<br />

9.3日改进: 不用放在每一个位置，只要记录每一行的记录就行了，那一行按顺序拍就行，不用把每个数字都放在应该的Z字型位置上
```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if len(s) == 1:
            return s
        if numRows == 1:
            return s
        res_list = list()
        for i in range(numRows):
            res_list.append("")
        t =(numRows - 1) * 2
        for i in range(len(s)):
            remainder = (i) % t
            if remainder > numRows-1:
                res_list[(numRows-1)-(remainder-(numRows-1))] += s[i]
            else:
                res_list[remainder] += s[i]
        res = ""
        return "".join(res_list)
```


```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if len(s) == 1:
            return s
        if numRows == 1:
            return s
        remainder = len(s) % ((numRows-1)*2)
        
        least = len(s) // ((numRows-1)*2)
        if remainder <= numRows:
            width = (least)*(numRows-1) + 1
        else:
            width =(least)*(numRows-1) + 1 + (remainder-numRows)
        count = 0

        dp = [[False]*width for i in range(numRows)]

        for i in range(0, width):
            if i % (numRows-1) == 0:
                for j in range(0, numRows):
                    if count == len(s):
                        break
                    dp[j][i] = s[count]
                    count += 1
                lasti = i
                lastj = j
            else:
                if count == len(s):
                    break
                dp[lastj-1][lasti+1] = s[count]
                lastj -= 1
                lasti += 1

                count += 1

        res = ""
        for i in range(numRows):
            for j in range(width):
                if dp[i][j]:
                    res += dp[i][j]
        return res

```
**2022/03/15**
```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        adict = collections.defaultdict(str)
        t = 2*(numRows-1)
        for i in range(len(s)):
            mod = i % t
            if mod > numRows - 1:
                adict[numRows-(mod % numRows)-2] += s[i]
            else:
                adict[mod] += s[i]
        res = ""
        for i in range(numRows):
            if i not in adict:
                break
            res += adict[i]
        return res
```
**Tag: 字符串**
