# Implement a Binary Search for a value in a sorted list of ints in Python

<details><summary><b>Iterative Solution</b></summary>

```python
def binsearch(list, val):
    # define the start and end of the Binary Search range
    start = 0
    end = len(list) - 1

    # continue searching if the end of the search range is greater than the beginning
    while end >= start:
        
        # find the mid-point of the current search range
        mid = (start + end) // 2

        # if the mid-point is the value, return it
        if list[mid] == val:
            return "The value is located at index " + str(mid)
        
        # if the mid-point is greater than the value, redo the search with the end now equal to the previous element before the current mid-point in the list
        elif list[mid] > val:
            end = mid - 1

        # if the mid-point is less than the value, redo the search with the start now equal to the following element after the current mid-point in the list   
        else:
            start = mid + 1

    # if the value does not exist in the list, return -1
    return -1
```
</details>

<br>

Binary Search is a common algorithmic interview question.  When searching with traditional iterative methods, such as nested For Loops, there can be many instances when the same two values are being compared, over and over again. We can avoid this, and speed things up using a Binary Search.

Binary Search will take the mid-point of a sorted list, and compare the value that we are looking for against that mid-point.  If the mid-point is greater than the value, then we know that our value, if it exists in our list, will be to the left of the mid-point.  Conversely, if our value is greater than the mid-point, and it exists in our list, we know it will be to the right of the mid-point in out sorted list.

<br>

**Example**

Given this value and this list: <br>
`val = 8, list = [1,2,3,4,5,6,7,8,9]`

<br>
First, Binary Search finds the current mid-point:

<br>

`mid-point = 5`

<br>
Binary Search will then compare our value with our mid-point:

<br>

`is val ( > or = or < ) 5?` --> `val > 5`

<br>
Binary Search now knows that our value is greater than 5, so it will repeat its search process starting again at the next element in our list, `6`, and find the mid-point between `6` and the end of our list `9`

<br>

`mid-point = 7`

<br>
In the instance like above, where the amount of elements Binary Search is comparing is even, it will round down, to ensure no elements are skipped.  Now Binary Search repeats its comparasion with the mid-point:

<br>

`is val ( > or = or < ) 7?` --> `val > 7` 

<br>
Just like before, Binary Search now knows that our value is greater than 7, so it will repeat its search process starting again at the next element in our list, which is `8`.  It finds the mid-point between `8` and `9` (which is 8.5) and rounds down to `8`.

<br>

`is val ( > or = or < ) 8?` --> `val = 8` 

<br>
Binary Search has found our element after 3 comparasions.  This is an extremely fast way to find an element, if it exists, in a sorted list.  Now lets get to coding!

<br>
<br>
```
You are given a list of ints, sorted from least to greatest. This list will only contain ints. 
Write a function that implements a Binary Search with an iterative approach.
```
<br>


As always, it is best to start by breaking the problem down in pseudocode.

<br>

```python

# define the function that accepts a list and a value

    # define a start-point and end-point of the search range

    # continue the search unless the end-point is not before the start-point

        # find the mid-point of the current search range

        # if the mid-point is equal to the value, return it

        # elif the mid-point is greater than the value

            # redefine the end-point to be the element immediately preceeding the current mid-point and search again

        # else the mid-point is less than the value, 

            # redefine the start-point to be the element immediately following the current mid-point and search again
    
    # if the value does not exist in the list, return -1

```
<br>

Ok. That is a lot of pseudocode. Let us go slowly and tackle each item individually.

<br>

## Define the Function ##


Since this function is an implementation of Binary Search, lets call the function `bin_search`.  We will give it the parameters `list` and `val` for the given list and value respectively.

```python
def bin_search(list, val):
```

Easiest step of the implementation :)

<br>

## Define a Start-Point and an End-Point ##


We need to tell our function which index to begin our Binary Search from, and which index to end at.  Seems intuitive to call these points `start` and `end`.  Since we want to begin our first Binary Search with the whole `list`, we will set the value of `start` to `0` and the value of `end` to `len(list) - 1`.

*Remember: `len(list)` will give us the total number of elements inside of the list, but since enumeration is zero-indexed, we have to subtract 1 from `len(list)` to access the final element in `list`*

```python
def bin_search(list, val):
    start = 0
    end = len(list) - 1
```

Great.  Now our Binary Search will begin with the entire list.

<br>

## Continue the Search / While Loop ##


In most circumstances, if you know how many iterations a loop needs to complete, it is best practice to write a For Loop. However, when you do not know how many times a loop needs to repeat to finish its task, a While Loop is the best approach.

```python
def bin_search(list, val):
    start = 0
    end = len(list) - 1

    while end >= start:
```

As our search range becomes smaller and smaller, while looking for `val`, if at any point, the end-point becomes less than our start-point, we will not be able to find the mid-point anymore, and we should break out of our loop.

<br>

## Find and Test the current Mid-Point  ##


We are going to combine the next two pseudocode elements together for brevity.  Our program will find the mid-point, test to see if it is our given value, and if it is, return it.

```python
def bin_search(list, val):
    start = 0
    end = len(list) - 1
    
    while end >= start:

        mid = start + end // 2

        if mid == val:
            return "The value is located at index " + str(mid)

   
```

Note, // is <a href="https://www.w3schools.com/python/python_operators.asp">floor division</a>.  This will divide the two ints, and round down if the result is a float.

<br>

## Elif and Else Statements / Winnowing the Binary Search ##


The next two statements are to allow our program to begin to zero in to the location of `val` in `list` *assuming that it exists in `list`, and that `list` is sorted from least to greatest*

If `mid` is greater than `val`, we know that `val` would be in the sublist to the left of the mid-point.  We then will redefine `end` to be the element that immediately preceeds `mid`, and run our search again.

Conversely, if `mid` is less than `val`, then `val` would have to exist in the sublist to the right of `mid`. We then will redefine `start` to be the element that immediately follows `mid`, and run our search again.


```python
def bin_search(list, val):
    start = 0
    end = len(list) - 1

    while end >= start:
        
        mid = start + end // 2

        if mid == val:
            return "The value is located at index " + str(mid)
        
        elif list[mid] > val:
            end = mid - 1
        
        else:
            start = mid + 1
```

The preceeding code will continue to loop through `list` until it reaches `val`, or our base case happens, and we break out of our While Loop.

<br>

## Finishing it Up ##


 If we break out of our loop, it means that `val` was not found in `list` and we need to return -1.

```python
def bin_search(list, val):
    start = 0
    end = len(list) - 1

    while end >= start:
        
        mid = start + end // 2

        if mid == val:
            return "The value is located at index " + str(mid)
        
        elif list[mid] > val:
            end = mid - 1
        
        else:
            start = mid + 1

    return -1
```

And that is our function!  Our function works on a list that is sorted in ascending order, but we could have just as easilly implemented it on a list that is in decending order.  what is most important to remember is that **Binary Search will only work if the list you are given is a sorted list**