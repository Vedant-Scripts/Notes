# Python Cheat Sheet for DSA (Python 3)

Review for 5 minutes at the start of every study session. Cover the right side, recite, check. When you look something up while solving, add one line here (in your own words), never twice.

## Basics
```python
x = 5            # no types, no semicolons
7 // 2           # 3   integer divide (floors: -7 // 2 = -4)
7 / 2            # 3.5 always a float
7 % 2, 2 ** 5    # remainder, power
divmod(7, 2)     # (3, 1)
i += 1           # there is NO i++
x is None        # compare to None with "is"
and / or / not   # not && || !
for i in range(n): ...        # 0..n-1
for i in range(a, b, step): ...
while cond: ...
float('inf')     # infinity, also -float('inf')
a, b = b, a      # swap, no temp variable
```

## Lists (like JS arrays)
```python
a = [1, 2, 3]
a.append(4)      # O(1)
a.pop()          # remove last, O(1)
a.pop(0)         # remove first, O(n): avoid, use deque
a.insert(i, x)   # O(n)
len(a), a[-1]    # last element
a[1:3]           # slice (makes a COPY), a[::-1] reversed, a[:] copy
for i, x in enumerate(a): ...
for x, y in zip(a, b): ...
sorted(a)                          # new list
a.sort()                           # in place
sorted(a, key=lambda p: p[1], reverse=True)
sum(a), min(a), max(a)
[x * 2 for x in a if x > 0]        # list comprehension
grid = [[0] * cols for _ in range(rows)]   # 2D grid. NOT [[0]*cols]*rows
```

## Dict (hash map)
```python
d = {}
d[k] = v
d.get(k, 0)             # default if missing
k in d                  # O(1)
d.pop(k), del d[k]
for k, v in d.items(): ...     # also d.keys(), d.values()

from collections import defaultdict, Counter, deque
g = defaultdict(list)   # missing key -> []   (g[k].append(x))
n = defaultdict(int)    # missing key -> 0
c = Counter("aabbbc")   # counts; c.most_common(1) -> [('b', 3)]
```

## Set
```python
s = set()               # {} is an empty DICT, not a set
s.add(x); s.discard(x)  # discard doesn't error if missing
x in s                  # O(1)
a & b, a | b, a - b     # intersection, union, difference
```

## Strings (immutable)
```python
s[i], s[::-1], len(s)
s.split(), s.split(",")
" ".join(list_of_strings)
s.lower(), s.isalnum(), s.isdigit(), s.isalpha()
ord('a') # 97      chr(97) # 'a'
chars = list(s)         # to modify, convert to list ...
"".join(chars)          # ... and join back
```
Never build a big string with `+=` in a loop (O(n^2)). Collect pieces in a list and join once.

## Tuples
```python
t = (1, 2)              # immutable, hashable: can be a dict key or set item
x, y = t                # unpack
```

## deque (queue / BFS)
```python
dq = deque()
dq.append(x); dq.appendleft(x)
dq.pop(); dq.popleft()  # both O(1)
```

## heapq (min-heap only)
```python
import heapq
h = []
heapq.heappush(h, x)
heapq.heappop(h)        # smallest
heapq.heapify(a)        # list -> heap, O(n)
heapq.heappush(h, -x)   # MAX-heap trick: store negatives, negate on pop
heapq.heappush(h, (priority, item))   # tuples compare left to right
heapq.nlargest(k, a)
```

## Binary search helper
```python
import bisect
bisect.bisect_left(a, x)   # index where x would go in sorted a
```

## Functions and misc
```python
def f(a, b=None): ...      # NEVER use b=[] as a default (shared mutable)
from functools import cache
@cache                      # memoization for recursion (DP)
def fib(n): return n if n < 2 else fib(n-1) + fib(n-2)
import sys; sys.setrecursionlimit(10**6)   # default depth is only ~1000
```

## Complexity quick table
| Operation | Cost |
|---|---|
| list append / pop() / index | O(1) |
| list pop(0) / insert / `x in list` | O(n) |
| `x in set` / `x in dict` / dict get | O(1) average |
| sort | O(n log n) |
| slice a[i:j] | O(j - i) |
| deque append/pop both ends | O(1) |
| heap push / pop | O(log n) |

## Gotchas (the ones that bite)
1. `[[0]*c]*r` makes r copies of the SAME row. Use the comprehension.
2. Slicing copies. `a[:]` and `a[1:]` cost O(n).
3. `{}` is a dict. Use `set()` for an empty set.
4. `//` floors toward negative infinity: `-7 // 2 == -4`.
5. Indentation is the syntax.
6. Mutable default arguments are shared across calls.
7. heapq is min-heap only.
8. Modifying a list while looping over it gives wrong results. Loop over a copy.