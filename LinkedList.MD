#### Question-1

Reverse a linkedlist

#### Solution-1

_Iterative Solution_

```PY
def get_reversedList_iterative(head):
    if head == None or head.next == None:
        return head

    rev_head = None
    while head != None:
        temp = head
        head = head.next
        temp.next = None
        if rev_head == None:
            rev_head = temp
        else:
            temp.next = rev_head
            rev_head = temp

    return rev_head
```

_Recursive Solution_

```PY
rev_head = None
def get_reversed_list(head):
    if head == None:
        return None

    if head.next == None:
        if rev_head == None:
            rev_head = head
        return head

    headNext = get_reversed_list(head.next)

    if headNext:
        headNext.next = head
        head.next = None

        return head
```

#### Question-2

Delete duplicates from unsorted/sorted linkedlist

#### Solution-2

Use a set to keep track of the seen element. Delete the element if seen before in the set.

#### Question-3

Merge Sort in linkedList

#### Solution-3

```py
# Initialize new node
def getNode(value):
    return Node(value)

# Conquer function
def merge(lbHead, lbTail, rbHead, rbTail):
    if lbHead == None and rbHead == None:
        return None

    if lbHead == None or rbHead == None:
        return lbHead or rbHead , lbTail or rbTail

    result_head = None
    result_tail = None
    while lbHead != None and rbHead != None:
        data1 = lbHead.data
        data2 = rbHead.data
        if data1 < data2:
            newNode = getNode(data1)
            lbHead = lbHead.next
        elif data1 == data2:
            newNode = getNode(data1)
            lbHead = lbHead.next
        else:
            newNode = getNode(data2)
            rbHead = rbHead.next

        if result_head == None:
            result_head = result_tail = newNode
        else:
            result_tail.next = newNode
            result_tail = newNode

    if lbHead != None:
        while lbHead != None:
            data1 = lbHead.data
            lbHead = lbHead.next
            newNode = getNode(data1)
            result_tail.next = newNode
            result_tail = newNode

    elif rbHead != None:
        while rbHead != None:
            data2 = rbHead.data
            rbHead = rbHead.next
            newNode = getNode(data2)
            result_tail.next = newNode
            result_tail = newNode

    return result_head, result_tail

# Divider function
def get_sorted(head):
    if head == None or head.next == None:
        return head, head

    total_length = 0
    start_head = head
    while start_head != None:
        total_length += 1
        start_head = start_head.next

    mid = total_length // 2
    lHead = None
    rHead = None
    temp = head
    while mid > 1:
        mid -=1
        temp = temp.next

    lHead = head
    rHead = temp.next
    temp.next = None

    lbHead, lbTail = get_sorted(lHead)
    rbHead, rbTail = get_sorted(rHead)
    finalHead, finalTail = merge(lbHead, lbTail, rbHead, rbTail)

    return finalHead, finalTail

# Driver function
def mergeSort(head):
    head_ptr, tail_ptr = get_sorted(head)
    return head_ptr
```

#### Question-4

Given two numbers, num1, and num2, represented by linked lists. The task is to return the head of the linked list that represents the sum of these two numbers.

#### Solution-4

The idea is same as we add two numbers manually. Put all the elements of two linkedlist in two different stacks. pull one-one from each stack add and create new node to store the result.

```PY
def getNode(value):
        return Node(value)

def addTwoLists(num1, num2):
    if num1 == None or num2 == None:
        return num1 or num2
    stack1 = []
    stack2 = []

    temp = num1
    while temp != None:
        stack1.append(temp)
        temp = temp.next

    temp = num2
    while temp != None:
        stack2.append(temp)
        temp = temp.next


    carryOver = 0
    result_linkList = None
    while len(stack1) > 0 and len(stack2) > 0:
        curr_node1 = stack1.pop()
        curr_node2 = stack2.pop()

        origData_1 = curr_node1.data
        origData_2 = curr_node2.data
        newNode = getNode(0)

        newNode.data = (origData_1 + origData_2 + carryOver) % 10
        carryOver = (origData_1 + origData_2 + carryOver) // 10

        newNode.next = result_linkList
        result_linkList = newNode

    if len(stack1) > 0:
        while len(stack1) > 0 and carryOver > 0:
            curr_node1 = stack1.pop()
            origData_1 = curr_node1.data
            newNode = getNode(0)
            newNode.data = (origData_1 + carryOver) % 10
            carryOver = (origData_1 + carryOver) // 10
            newNode.next = result_linkList
            result_linkList = newNode

    elif len(stack2) > 0:
        while len(stack2) > 0 and carryOver > 0:
            curr_node2 = stack2.pop()
            origData_2 = curr_node2.data
            newNode = getNode(0)
            newNode.data = (origData_2 + carryOver) % 10
            carryOver = (origData_2 + carryOver) // 10
            newNode.next = result_linkList
            result_linkList = newNode

    if carryOver > 0:
        newNode = getNode(carryOver)
        newNode.next = result_linkList
        result_linkList = newNode

    return result_linkList
```

#### Question-5

Given two linked lists sorted in increasing order, create a new linked list representing the intersection of the two linked lists. The new linked list should be made with without changing the original lists.

#### Solution-5

To find the intersection of two sorted list. Use the same `merge sorted array logic` to get the result.

##### Question-6

Given two singly linked lists, return the point where two linked lists intersect.

![Alt](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700163/Web/Other/blobid1_1721764552.png)

#### Solution-6

1. Find the length difference between two linkedlist (say d).
2. Traverse the bigger linkedList upto d distance. now both the list has same length
3. Now traverse both the lists one by one the point were it meets is the common starting point.

```PY
def intersetPoint(head1,head2):
    if head1 == None or head2 == None:
        return -1

    start_head1 = head1
    length1 = 0
    while start_head1 != None:
        length1 +=1
        start_head1 = start_head1.next

    start_head2 = head2
    length2 = 0
    while start_head2 != None:
        length2 +=1
        start_head2 = start_head2.next


    diff = abs(length2 - length1)

    start_head1 = head1
    start_head2 = head2

    if length1 > length2:
        while diff > 0:
            diff -=1
            start_head1 = start_head1.next

    elif length2 > length1:
        while diff > 0:
            diff -= 1
            start_head2 = start_head2.next

    found_flag = False

    while start_head1 != None and start_head2 != None:
        if start_head1 == start_head2:
            return start_head1.data

        start_head1 = start_head1.next
        start_head2 = start_head2.next

    return -1
```

#### Question-7

Given a Circular linked list. The task is split into two Circular Linked lists. If there are an odd number of nodes in the given circular linked list then out of the resulting two halved lists, the first list should have one node more than the second list.

#### Solution-7

Use `Hare and tortoise Method` to solve the problem.

#### Question-8

Given an input stream A of n characters consisting only of lower case alphabets. While reading characters from the stream, you have to tell which character has appeared only once in the stream upto that point. If there are many characters that have appeared only once, you have to tell which one of them was the first one to appear. If there is no such character then append '#' to the answer.

```
EXAMPLE:
--------
Input: A = "aabc"
Output: "a#bb"
Explanation: For every ith character we will
consider the string from index 0 till index i first non
repeating character is as follow-
"a" - first non-repeating character is 'a'
"aa" - no non-repeating character so '#'
"aab" - first non-repeating character is 'b'
"aabc" - there are two non repeating characters 'b' and 'c',
first non-repeating character is 'b' because 'b' comes before
'c' in the stream.
```

#### Solution-8

1. Mentain the record of seen characters in a set to check if current character is seen before
2. mentain list of unique character (i.e. character seen first time) for every character get the first character from this list. if list is empty use `#` as character.

```PY
def FirstNonRepeating(self, A):
    is_seen = set()
    resultStr = ""

    seen_list = []
    for i in range(len(A)):
        character = None
        if A[i] not in is_seen:
            is_seen.add(A[i])
            seen_list.append(A[i])
        else:
            if A[i] in seen_list:
                seen_list.remove(A[i])

        if len(seen_list) > 0:
            character = seen_list[0]
        else:
            character = "#"

        resultStr += character

    return resultStr
```
