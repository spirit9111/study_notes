# collections模块 #
import collections

## namedtuple() ##
自定义一个tuple对象,使用.方式来调用元素,也可以用index来调用
```python
from collections import namedtuple 
Point = namedtuple('Point', ['x', 'y']) 
p = Point(1, 2) 
print(p.x)
print(p.y)
print(p[0])
print(p[1])
```

## deque() ##
双向list,支持从左从右append/pop数据
```python
from collections import deque
a = deque()
a.appendleft(1)
a.appendleft(2)
print(a)
a.popleft()
print(a)
```

## Counter() ##
一次性统计字符串(元组,字典...)中所有字符出现的次数,以特殊的字典方式输出
```python
from collections import Counter
c = Counter()
for i in 'programming':
    c[i] = c[i] + 1
print(c)
print(c['m'])  # 也可以直接获取某个元素的出现的次数
```
