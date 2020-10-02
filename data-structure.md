## Set
```python
a = set()
a.add(2)             # a: {2}
a.add(3)             # a: {2, 3}
a.remove(2)          # a: {3}
a.discard(2)         # a: {3}. no error
a.pop()              # output: 3. a: {}
3 in a               # output: false
```

## Dict
```python
a = {}
a['foo'] = 'bar'                      # a: {"foo": "bar"}
del a['foo']                          # a: {}
a.setdefault('arr1', []).append(1)    # a: {'arr1': [1]}
a['arr1'].append(2)                   # a: {'arr1': [1, 2]}
```

## List (also Stack)
```python
a = []
a.append(1)           # a: [1]
a += [2, 3]           # a: [1, 2, 3]
len(a)                # output: 3
a.pop()               # output: 3. a: [1, 2]
a.remove(1)           # a: [2]
a.insert(2, 1)        # a: [2, 1]
a.insert(10, 3)       # a: [2, 1, 3]
a.count(2)            # output: 1
a.index(2)            # output: 0
```

## Queue
```python
from queue import Queue

q = Queue()
q.put(1)
q.get()               # output: 1
q.empty()             # output: True
q.qsize()             # output: 0
```

## Deque
```python
from collections import deque

dq = deque()
dq.append(1)            # dq: [1]
dq.appendleft(2)        # dq: [2, 1]
dq.appendleft(3)        # dq: [3, 2, 1]
dq.pop()                # output: 1, dq: [3, 2]
dq.popleft()            # output: 3, dq: [2]
dq.count(2)             # output: 1
dq.insert(1, 1)         # dq: [2, 1]
len(dq)                 # output: 2
```

## PriorityQueue
```python
from queue import PriorityQueue

q = PriorityQueue(maxsize = n)
q.put((score, item))
score, val = q.pop()
q.empty()                            # output: True
```

## Heap
```python
import heapq

nums = [1,2,3,4,5]
minH, maxH = [], []

# minHeap
for num in nums:
    heapq.heappush(minH, num)
 
# maxHeap
for num in nums:
    heapq.heappush(maxH, (-num, num))  # (priority, value)

sortKeyOut1, outputItem1 = heapq.heappop(items)
```

## DoublyLinkedList
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.prev, self.next = None, None

class LinkedList:
    def __init__(self):
        self.head, self.tail = None, None
   
    def append(self, node):
        if not self.tail:
            self.head, self.tail = node, node
            return
        node.prev = self.tail
        self.tail.next = node
        self.tail = node
    
    def remove(self, node):
        if self.head and self.head.val == node.val:
            self.head = self.head.next
        if self.tail and self.tail.val == node.val:
            self.tail = self.tail.prev
        if node.prev:
            node.prev.next = node.next
        if node.next:
            node.next.prev = node.prev
```

## Binary Search Tree
```python
# helper function
def printTree(node, level=0):
    if node != None:
        printTree(node.right, level + 1)
        print(' ' * 2 * level + '-', node.val)
        printTree(node.left, level + 1)

class Node:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None

class BST:
    def __init__(self):
        self.root = None

    def add(self, val):
        if not self.root:
            self.root = Node(val)
            return
        self._add(self.root, val)

    def _add(self, node, val):
        if not node:
            return Node(val)
        if node.val <= val:
            node.right = self._add(node.right, val)
        else:
            node.left = self._add(node.left, val)
        return node

    def search(self, val):
        return self._search(self.root, val)

    def _search(self, node, val):
        if not node:
            return False
        if node.val == val:
            return True
        if node.val < val:
            return self._search(node.right, val)
        return self._search(node.left, val)

bst = BST()
bst.add(11)
bst.add(2)
bst.add(10)
bst.add(5)
bst.add(13)
printTree(bst.root)
# output:
#   - 13
# - 11
#     - 10
#       - 5
#   - 2

print(bst.search(2))        # output: True
print(bst.search(7))        # output: False
```

## Trie
```python
class Trie:
    def __init__(self):
        self.head = Node(None)

    def insert(self, s):
        c_node = self.head
        for c in s:
            if c not in c_node.children:
                c_node.children[c] = Node(c)
            c_node = c_node.children[c]
        c_node.word = s

    def search(self, s):
        c_node = self.head
        for c in s:
            if c in c_node.children:
                c_node = c_node.children[c]
            else:
                return False
        if curr_node.word:
            return True
```
