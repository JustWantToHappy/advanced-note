## 匈牙利算法
https://www.nowcoder.com/practice/b9eae162e02f4f928eac37d7699b352e?tpId=37&tqId=21251&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=%E7%B4%A0%E6%95%B0
```python
from math import sqrt

# 判断是否素数
def isPrime(x):
    if x < 2:
        return False
    for i in range(2, int(sqrt(x)) + 1):
        if x % i == 0:
            return False
    return True


# 匈牙利算法（DFS找增广路）
def find(odd, visited, match, evens):
    for i in range(len(evens)):
        if isPrime(odd + evens[i]) and not visited[i]:
            visited[i] = True
            # 如果这个偶数还没匹配，或者能腾位置
            if match[i] == 0 or find(match[i], visited, match, evens):
                match[i] = odd
                return True
    return False


n = int(input())
nums = list(map(int, input().split()))

# 分奇偶
odds = []
evens = []

for num in nums:
    if num % 2 == 0:
        evens.append(num)
    else:
        odds.append(num)

# match[i] 表示第 i 个偶数匹配的奇数
match = [0] * len(evens)

count = 0

for odd in odds:
    visited = [False] * len(evens)
    if find(odd, visited, match, evens):
        count += 1

print(count)
```