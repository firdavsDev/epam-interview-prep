

## 💡 5-BO‘LIM: Algorithms, Data Structures & Real-World Coding Patterns – savollar va javoblar

---

### **1. “Two sum” masalasi: algoritm va murakkabligi**

**Masala**: Ikki sonni topingki, ularning yig‘indisi `target`ga teng bo‘lsin.

```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in seen:
            return [seen[diff], i]
        seen[num] = i
```

* 🧠 **Time**: O(n) | **Space**: O(n)

---

### **2. Sliding window misoli: Maksimum subarray sum**

```python
def max_subarray_sum(nums, k):
    window_sum = sum(nums[:k])
    max_sum = window_sum

    for i in range(k, len(nums)):
        window_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, window_sum)

    return max_sum
```

* Window’ni siljitish orqali har bir variantni ko‘rmasdan yechim topiladi.
* Time: O(n)

---

### **3. LRU Cache qanday ishlaydi?**

* Least Recently Used cache → `OrderedDict` yoki `collections.deque + dict` bilan ishlanadi.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key, value):
        self.cache[key] = value
        self.cache.move_to_end(key)
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

---

### **4. Graph traversal: BFS vs DFS**

* BFS – queue (layer-by-layer), shortest path topish uchun qulay
* DFS – stack (depth-first), cycle detection uchun ishlatiladi

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()
        if node not in visited:
            visited.add(node)
            queue.extend(graph[node])
```

---

### **5. Real example: Rate limiter qanday yozasiz?**

```python
from collections import deque
import time

class RateLimiter:
    def __init__(self, max_requests, period):
        self.requests = deque()
        self.max_requests = max_requests
        self.period = period

    def allow(self):
        now = time.time()
        while self.requests and now - self.requests[0] > self.period:
            self.requests.popleft()
        if len(self.requests) < self.max_requests:
            self.requests.append(now)
            return True
        return False
```

---

### **6. HashMap, Set qanday ishlaydi Python’da?**

* HashMap = `dict`, Set = `set`
* O(1) access va insert, chunki hash table asosida ishlaydi
* `__hash__` va `__eq__` methodlariga bog‘liq

---

### **7. Priority Queue (heapq) misoli**

```python
import heapq

nums = [4, 1, 7, 3]
heapq.heapify(nums)
heapq.heappush(nums, 2)
min_val = heapq.heappop(nums)
```

* O(log n) vaqt
* `heapq` – min-heap default, max-heap uchun -val saqlanadi

---

### **8. Recursion va Tail Recursion optimizatsiyasi**

* Python’da **tail call optimization yo‘q**, stack depth cheklangan
* StackOverflow oldini olish uchun iterativ versiya afzal

---

### **9. Sorting algoritmlari haqida nimalarni bilasan?**

* `Timsort` (Python’da default sort)
* QuickSort – O(n log n) average, O(n²) worst
* MergeSort – always O(n log n), stable

```python
sorted(nums, reverse=True)  # Timsort
```

---

### **10. Real-world: URL Shortener qanday arxitektura bilan yoziladi?**

* Random yoki hashlangan `short_code`
* Redis: short ↔ long mapping uchun
* Rate limiting
* Monitoring
* Horizontal scale (stateless)

