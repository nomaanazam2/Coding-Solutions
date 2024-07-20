#### Question-1

Given a positive integer N, print count of set bits in it and return the count.

Input: 6 (110)
OUTPUT: 2

#### Solution-1

Add remainders (when divided by 2) if remainder is 1.

```PY
def setBits(N):
    setBit_count = 0
    while N > 0:
        rem = N%2
        N = N//2
        if rem == 1:
            setBit_count +=1
    return setBit_count
```

#### Question-2

Given an array A containing 2*N+2 positive numbers, out of which 2*N numbers exist in pairs whereas the other two number occur exactly once and are distinct. Find the other two numbers. Return in increasing order.

#### Solution-2

Using set() in python, add element to set if not seen else remove the element from set().

```PY
def singleNumber(nums):
    seen_set = set()
    for i in range(len(nums)):
        if nums[i] in seen_set:
            seen_set.remove(nums[i])
        else:
            seen_set.add(nums[i])

    result = list(seen_set)     # convert set to List
    result.sort()
    return result
```

Using bit manipulation.

1. Find xor of all the element (say xor_value) this will result in xor of two unique element.
2. Find the index of rightmost set bit of xor_value.
3. Divide the elements into two groups based on the element bit at the given index is set or unset. This will saperate the two non repeating element into two groups.
4. take xor of two groups saperately

```PY
# used to find the index of rightmost set bit
def get_bitIndex(n):
    bitIndex = 0
    while xor_val >0:
        if xor_val %2 == 1:
            break
        else:
            bitIndex +=1
            # shifting the number to right by 1 is equalent to integrer dividing number by 2
            xor_val = xor_val >> 1

    return bitIndex

def singleNumber(nums):
    xor_val = 0
    # Taking XOR of all the element
    for i in range(len(nums)):
        xor_val = xor_val ^ nums[i]

    # Finding the rightmost setbit Index
    bitIndex = get_bitIndex(xor_val)

    set_xor = 0
    unset_xor = 0
    # Dividing into two groups and taking XOR
    for i in range(len(nums)):
        # Shifting the element by bitIndex amount and then checking the unit place bit.
        rightShift_rem = (nums[i] >> bitIndex)%2
        if rightShift_rem == 1:
            set_xor = set_xor ^ nums[i]
        else:
            unset_xor = unset_xor ^ nums[i]
    if set_xor < unset_xor:
        return [set_xor, unset_xor]
    else:
        return [unset_xor, set_xor]
```

#### Question-3

You are given two numbers A and B. The task is to count the number of bits needed to be flipped to convert A to B.

#### Solution-3

1. Take XOR of given two numbers (say `xor_val`).
2. Find number of set bits in `xor_val`

```PY
def countBitsFlip(a,b):
    xor_val = a ^ b
    count =0
    while xor_val > 0:
        rem = xor_val % 2
        if rem ==1:
            count +=1
        # Rightshift by 1 == Integer divide by 2
        xor_val = xor_val >> 1
    return count
```

#### Question-4

You are given a number N. Find the total count of set bits for all numbers from 1 to N(both inclusive).

- Expected Time Completexity: O(log(n))
- Expected Space Complexity: O(1)

#### Solution-4

Add the digits in vertial orders of bit from Left to Right.
At each vertial do the following.

1. Get `block_size` (For digit length = 4, block sizes will be 8, 4, 2, 1)
2. Get `total_complete_block`
3. Get `leftover_block_size`
4. ```PY
   If total_complete_block is ODD:
        sum = block_size * (total_complete_block // 2) + leftover_block_size
   else:
        sum = block_size * (total_complete_block // 2)
   ```

```PY
def get_digitLength(n):
    count = 0
    while n>0:
        count +=1
        n = n>>1
    return count

def countSetBits(n):
    total_digits = get_digitLength(n)
    total_sum = 0

    while total_digits > 0:
        skip_after = 2**(total_digits-1)
        total_complete_block = (n + 1) // skip_after
        left_remainder = (n + 1) % skip_after
        total_sum = total_sum + (total_complete_block // 2) * skip_after

        if total_complete_block % 2 != 0:
            total_sum += left_remainder
        total_digits -= 1

    return total_sum
```

#### Question-5

Given a non-negative integer n. The task is to check if it is a power of 2.

#### Solution-5

Check if square of length of digits of number n is equal to given number

```PY
def isPowerofTwo(n):
    total_digits = 0
    temp_no = n
    while temp_no > 0:
        total_digits += 1
        temp_no = temp_no >> 1
    exp_sqrNo = 2**(total_digits - 1)
    if exp_sqrNo == n:
        return True
    else:
        return False
```

check if you find any remainder when divided by 2 untill number becomes 1

```PY
def isPowerofTwo(n):
    if n == 0:
        return False

    while n>1:
        if n%2 != 0:
            return False
        n = n >> 1

    return True
```

#### Question-6

Given a number N having only one ‘1’ and all other ’0’s in its binary representation, find position of the only set bit. If there are 0 or more than 1 set bit the answer should be -1. Position of set bit '1' should be counted starting with 1 from LSB side in binary representation of the number.

#### Solution-6

For this to happen number should be perfect square. If it is so then index would be equal to length of digit

```PY
def findPosition(N):
    if N == 0:
        return -1

    index=1
    while N > 1:
        # This means number is not perfect square it will have more than 1 ones
        if N % 2 != 0:
            return -1
        index +=1
        N = N >> 1
    return index
```

#### Question-7

Given two numbers X and Y, and a range [L, R] where 1 <= L <= R <= 32. You have to copy the set bits of 'Y' in the range L to R in 'X'. Return this modified X.

Input : x = 10, y = 13, l = 2, r = 3 \
Output : x = 14

Binary representation of 10 is 1010 and
that of y is 1101. There is one set bit
in y at 3'rd position (in given range).
After we copy this bit to x, x becomes 1110
which is binary representation of 14.

#### Solution-7

1. Iterate through every digit of Y.
2. If a digit is a set bit and lie in the range [l, r] position. do the following
   1. Get perfect square number of current digit position (this will have only one '1' at the current digit position)
   2. ```PY
      # Check if this postion if x is set or unset
      If (x >> (position - 1)) % 2 == 0:
        x =  x ^ (perfect_square_number)
      ```

```PY
def setSetBit(x, y, l, r):
    position = 0
    final_number = x
    while y >0:
        binary_digit = y % 2
        position +=1

        if position >= l and position <= r and binary_digit == 1:
            sq_number = 2**(position - 1)
            if (x >> (position - 1)) % 2 == 0:
                final_number = final_number ^ sq_number

        y = y >>1

    return final_number
```

#### Question-8

Calculate multiplication of two number without using \*, / and pow()

#### Solution-8

Logic is same as we multiply numbers \
Example

```
    1011
    1001
--------------------
    1011
   0000
  0000
 1011
--------------------
1011 + (1011 << 3)
--------------------
```

```PY
def Multiply_bitwise(n1, n2):
    digit_index = 0
    temp_n = n1
    result = 0
    while temp_n > 0:
        curr_bit = temp_n % 2
        if curr_bit == 1:
            result = result + (n2 << digit_index)
        digit_index += 1
        temp_n = temp_n >> 1
    return result
```

#### Question-9

Given two integers say a and b. Find the quotient after dividing a by b without using multiplication, division, and mod operator.

#### Solution-9

Using mathematical formula

$$a/b =(e^{ln(|a/b|)}) = (e^{ln(|a|)}) - (e^{ln(|b|)}) $$

```PY
def divide(dividend, divisor):
    ans = math.exp(math.log(abs(dividend)) - math.log(abs(divisor)))

    return math.floor(ans)
```

**Approach-2:** \
Keep subtracting the divisor from the dividend until the dividend becomes less than the divisor. The dividend becomes the remainder, and the number of times subtraction is done becomes the quotient.
