#### List of non-premitive DS supported in Vanilla Python

1. List: `list()`

```PY
fruits = ['apple', 'banana', 'cherry']
numbers = [1, 2, 3, 4, 5]
mixed = ['apple', 1, 3.14, True]
my_list = []

# ADD
# ---
# Add a single element at end
my_list.append(10)

# Add multiple elements
my_list = my_list + [20, 30, 40]

# Insert an element at a specific index
my_list.insert(2, 2024)

# DELETE
# ------
# Remove the first occurrence of a specific value
my_list.remove(2024)

# Remove an element at a specific index using pop()
# DEFAULT: Last element
removed_element = my_list.pop(2)


# SEARCH
# ------
# Find the index of the first occurrence of a value
index = my_list.index(2024)

# Find the value using index
value = my_list[2]


# UPDATE
# ------
# Update a single element
my_list[1] = 25

# Update a range of elements (slice)
my_list[2:4] = [35, 45]
```

2. Dictionary: `dict()`

```PY
student = {
    'name': 'John Doe',
    'age': 21,
    'major': 'Computer Science'
}
my_dict = {}

# ADD
# ---
my_dict["key"] = "value"

# DELETE
# ------
value = my_dict.pop('key')

# SEARCH
# ------
# Find a value using direct key access
value = my_dict['key']

# Safely find a value using get() with a default value
value = my_dict.get('key', 'NOT FOUND')

# Get keys, values or items
keys = my_dict.keys()
values = my_dict.values()
items = my_dict.items()

# UPDATE
# ------
my_dict['key'] = 'New Value'
```

3. Set: `set()` uses `HashTable` internally

```PY
unique_numbers = {1, 2, 3, 4, 5}
fruits = {'apple', 'banana', 'cherry'}
my_set = set() # my_set =  set([1, 2, 2, 2, 3, 5, 5])

# ADD
# ---
# Add a single element using add()
my_set.add(10)

# REMOVE
# ------
# Remove a specific element using remove()
my_set.remove(30)

# SEARCH
# ------
# Check if an element exists using in
exists = 20 in my_set

# UPDATE
# ------
my_set.remove(10)  # Remove existing element
my_set.add(70)     # Add a new element

print(set1 | set2)  # Union: {1, 2, 3, 4, 5}
print(set1 & set2)  # Intersection: {3}
print(set1 - set2)  # Difference: {1, 2}
print(set1 ^ set2)  # Symmetric Difference: {1, 2, 4, 5}
```

**Time Complexity**

1. `List:` Uses dynamic array internally

   | Operations          | Average Case | Worst Case |
   | ------------------- | :----------: | :--------: |
   | Access an element   |     O(1)     |    O(1)    |
   | Insert at Beginning |     O(n)     |    O(n)    |
   | Insert in Middle    |     O(n)     |    O(n)    |
   | Insert at End       |     O(1)     |    O(1)    |
   | Delete at Beginning |     O(n)     |    O(n)    |
   | Delete at Middle    |     O(n)     |    O(n)    |
   | Delete at End       |     O(1)     |    O(1)    |
   | Update single value |     O(1)     |    O(1)    |

2. `Dictionary:` Uses HasTable Internally

   | Operations          | Average Case | Worst Case |
   | ------------------- | :----------: | :--------: |
   | Access using key    |     O(1)     |    O(n)    |
   | Insert an item      |     O(1)     |    O(n)    |
   | Delete an Item      |     O(1)     |    O(n)    |
   | Update single value |     O(1)     |    O(n)    |
   | Search an element   |     O(1)     |    O(n)    |

3. `Set:` Uses HashTable internally

   | Operations          | Average Case | Worst Case |
   | ------------------- | :----------: | :--------: |
   | Access an element   |     O(1)     |    O(n)    |
   | Insert an item      |     O(1)     |    O(n)    |
   | Delete an Item      |     O(1)     |    O(n)    |
   | Update single value |     O(1)     |    O(n)    |
   | Search an element   |     O(1)     |    O(n)    |

## Important Other Data Structures

#### Doube Ended Queue - `deque`

It uses doubly linked list internally. It provides O(1) time complexity for append and pop operations from both ends. \
Deques are thread-safe for appends and pops from either end. It behaves correctly when accessed or modified concurrently by multiple threads. \
It is optimized for fast fixed-size operations. That is, where the number of elements in the deque is kept relatively constant (e.g. Sliding window).

**Use Case**

1.  Sliding window
2.  Circular buffer
3.  Queue, Stack implementation

```PY
from collections import deque

# Create a deque
d = deque(['a', 'b', 'c']) # OR deque()

# Append elements
d.append('d')       # Append at Right-end
d.appendleft('z')   # Append at Left-end
d.insert(2, 2024)   # insert value at given index

# Remove elements
d.pop()         # Removes from Right-end
d.popleft()     # Removes from Left-end
d.remove(2024)     # Remove first occurance of the value

# Search
# search a first occurance value and return its index
index = d.index(2024)

# search value within range of given indexes and return the position
index = d.index(2024, 1, 7)

# Rotate to right or left
d.rotate(2) # Rotate to Right by 2
d.rotate(-2) # Rotate to Left by 2

# Traversal - Forward
for item in d:
    print(item)

# Traversal - Backward
for item in reversed(dq):
    print(item)
```

#### Heap Queue - `heapq`

It provides an implementation of the heap queue algorithm, also known as the priority queue algorithm. The heapq module provides functions to work with heaps, primarily for managing a min-heap. You can create a max-heap by negating the values before inserting them.

**Use Case**

1. Priority Queues: Manage tasks based on their priority
2. Order Statistics: Quickly find the smallest or largest elements
3. Merging Sorted Lists: Merge multiple sorted lists into a single sorted list.

```PY
import heapq

numbers = [5, 7, 9, 1, 3]
heapq.heapify(numbers)      # Min-Heap
print(numbers)  # Output: [1, 3, 9, 7, 5]

# Insert Element into heap
heapq.heappush(numbers, 4)
print(numbers)  # Output: [1, 3, 4, 7, 5, 9]

# Pop smalles element from Heap
smallest = heapq.heappop(numbers)
print(smallest)  # Output: 1
print(numbers)   # Output: [3, 5, 4, 7, 9]

# Insert an element and then pop smallest element
smallest = heapq.heappushpop(numbers, 2)
print(smallest)  # Output: 2
print(numbers)   # Output: [3, 5, 4, 7, 9]

# Find k largest or k smallest elements
k = 3
k_largestList = heapq.nlargest(k, numbers)
print(k_largestList)  # Output: [9, 7, 6]

k_smallestList = heapq.nsmallest(k, numbers)
print(k_smallestList)  # Output: [4, 5, 6]


# Merging two sorted list
list1 = [1, 3, 5, 7]
list2 = [2, 4, 6, 8]

merged = list(heapq.merge(list1, list2))
print(merged)  # Output: [1, 2, 3, 4, 5, 6, 7, 8]

# heapif based on second element [[1,2], [3, 5], [6,5], [4,7]]
data = [[1, 2], [3, 5], [6, 5], [4, 7]]
heap = [(item[1], item) for item in data]
heapq.heapify(heap)

priority, item = heapq.heappop(heap)
print(item)
```
