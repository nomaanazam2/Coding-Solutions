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
my_set = set()

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

## Collections Library

1. Deque: Uses DLL internally
2. OrderedDict: It is a dictionary with mentained order of insertion
3. `deque`: uses doubly linked list (DLL) internally
4. Heap (Priority Queue): using heapq module
5.

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

# Traversal - Forward
for item in reversed(dq):
    print(item)
```
