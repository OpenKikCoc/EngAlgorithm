## Lists

### 1 Remove Even Integers from List

#### S1: doing it 'by hand'

```python
def remove_even(lst):
    odds = []  # Create a new empty list
    for c in lst:  # Iterate over input list
        # use the modulus symbol（'%'） to check if the item in the list is NOT even
        if c % 2 != 0:
            odds.append(c)  # If c isn't even, then append it to the empty list
    return odds  # Return the new list


print(remove_even([3, 2, 41, 3, 34]))
```

- Iterate over input list: 迭代输入列表
- ’%’ is the modulus symbol: 模数 符号

##### Time Complexity

Since the entire list has to be iterated over, this solution is in *O*(*n*) time.



#### S2: using list comprehension(列表表达式)

> With list comprehension, checking a condition and appending to the new list can all be done in one line. The code for it starts and ends with a ‘[’ and ends with a ‘]’.

```python
def remove_even(lst):
    # List comprehension to iterate aover List and add to new list if not even
	return [c for c in lst if c % 2 != 0]


print(remove_even([3, 2, 41, 3, 34]))
```

##### Time Complexity

The time complexity of this solution is also *O(n)*, since only the syntax has changed while the algorithm still iterates over all elements of the list.



### 2 Merge Two Sorted Lists

#### S1: Creating a new List

```python
# Merge list1 and list2 and return resulted list
def merge_lists(lst1, lst2):
    n, m = len(lst1), len(lst2)
    arr = []
    # initialize two variables to zero to store the current index of each list
    p1, p2 = 0, 0  
    # Traverse both lists and insert smaller value from arr1 or arr2 into result list,
    # and then increment that lists index
    # If a list is completely traversed, while other one is left then just copy all the remaining elements into result list
    while p1 < n and p2 < m:
        if lst1[p1] <= lst2[p2]:
            arr.append(lst1[p1])
            p1 += 1
        else:
            arr.append(lst2[p2])
            p2 += 1
    while p1 < n:
        arr.append(lst1[p1])
        p1 += 1
    while p2 < m:
        arr.append(lst2[p2])
        p2 += 1
    return arr


print(merge_lists([4, 5, 6], [-2, -1, 0, 7]))
```

- The solution above is a more intuitive way to solve this problem. Start by creating a new empty list. This list will be filled with all the elements of both lists in sorted order and returned. Then initialize two variables to zero to store the current index of each list. Then compare the elements of the two given lists at the current index of each, append the smaller one to the new list and increment the index of that list by 1. Repeat until the end of one of the lists is reached and append the other list to the merged list.

##### Time Complexity

The time complexity for this algorithm is *O*(*n*+*m*) where *n* and *m* are the lengths of the lists. This is because both lists are iterated over at least once.



#### S2: Merging in Place

```python
def merge_arrays(lst1, lst2):
    ind1 = 0  # Creating 2 new variable to track the 'current index'
    ind2 = 0
    # While both indeces are less than the length of their lists
    while ind1 < len(lst1) and ind2 < len(lst2):
        # If the current element of list1 is greater
        # than the current element of list2
        if(lst1[ind1] > lst2[ind2]):
            # insert list2's current index to list1
            lst1.insert(ind1, lst2[ind2])
            ind1 += 1  # increment indices
            ind2 += 1
        else:
            ind1 += 1

    if ind2 < len(lst2):  # Append whatever is left of list2 to list1
        lst1.extend(lst2[ind2:])
    return lst1


print(merge_arrays([4, 5, 6], [-2, -1, 0, 7]))
```

##### Time Complexity

Since both lists are traversed in this solution as well, the time complexity is O*(*m*(*n*+*m*)) where n and m are the lengths of the lists. Both lists are not traversed separately so we cannot say that complexity is *(m+n)*. The shorter of the two lengths is traversed in the while loop. Also, the insert function gets called when the if-condition is true. In the worst-case, the second list has all the elements that are smaller than the elements of the first list. In this case, the complexity will be *O(mn)*.

However, the extra space used in solution#1 is reduced to *O*(*m*) in solution#2. Thus, it makes this a tradeoff between space and time.



### 3 Find two nums added to ‘k’

#### S1: use a Dictionary

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        my_dict = collections.defaultdict(int)
        n = len(nums)
        for i in range(n):
            #  Check for value in dictionary, if found return 
            if target - nums[i] in my_dict:   
                return [i, my_dict[target - nums[i]]]
            # else, then insert the element into a dictionary. This takes O(1) as constant time insertion.
            else:
                my_dict[nums[i]] = i
```

##### Time Complexity

Each lookup is a constant time operation. Overall the running time of this approach is *O*(*n*).



#### S2: Binary Search, Brute Force

pass



### 4 List of Products of all Elements

> Given a list, modify it so that each index stores the product of all elements in the list except the element at the index itself.

> product：【乘和】Twenty-two is the product of elven and two. 

S: Optimizing the number of multiplications

```python
def find_product(lst):
    n = len(lst)
    # create a new empty list to restore the result
    B = [0] * n
    # get values starting from left
    p = 1
    for i in range(n):
        B[i] = p
        p *= lst[i]
    # get values starting from right,
    p = 1 
    for i in range(n-1, -1, -1):
        B[i] *= p
        p *= lst[i]
    return B
```

- The algorithm for this solution is to first create a new empty list to restore products of  all  elments to the left of each element. Then multiply each element in the input list to the product of all the elements to the right of the list by traversing it in reverse as done.



##### Time Complexity

Since this algorithm only traverses over the list twice, it’s in linear time, *O*(*n*).



### Question

Q1: in 2, why S2’s time complexity isO(nm)?

