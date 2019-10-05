# Implement a Binary Search in Python #

<details><summary><b>TL:DR... Iterative Solution</b></summary>

```python
def itr_bin_search(list, val):
    # define the start and end of the Binary Search range
    start = 0
    end = len(list) - 1

    # continue searching if the end of the search range is greater than the beginning
    while end >= start:
        
        # find the mid-point of the current search range
        mid = (start + end) // 2

        # if the mid-point is equal to the value, return it
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

<details><summary><b>TL:DR... Recursive Solution</b></summary>

```python
def rec_bin_search(list, val, start, end):
    # continue searching if the end of the search range is greater than the beginning
    if end >= start:
        
        # find the mid-point of the current search range
        mid = (start + end) // 2
     
        # if the mid-point is equal to the value, return it
        if list[mid] == val:
            return "The value is located at index " + str(mid)

        # if the mid-point is greater than the value, redo the search with the end now equal to the previous element before the current mid-point in the list
        elif list[mid] > val:
            new_start = start
            new_end = mid - 1
        
        # if the mid-point is less than the value, redo the search with the start now equal to the following element after the current mid-point in the list   
        else:
            new_start = mid + 1
            new_end = end
     
        # recursively call rec_bin_search with the new start and end points
        return rec_bin_search(list, val, new_start, new_end)
    
    # if the value does not exist in the list, return -1
    else:
        return -1
```
</details>

<br>

Binary Search is a common algorithmic interview question.  When searching with traditional iterative methods, such as nested For Loops in a linear search, there can be many instances when the same two values are being compared, over and over again. We can avoid this, and speed things up using a Binary Search.

Binary Search will take the mid-point of a sorted list, and compare the value that we are looking for against that mid-point.  If the mid-point is greater than the value, then we know that our value, if it exists in our list, will be to the left of the mid-point.  Conversely, if our value is greater than the mid-point, and it exists in our list, we know it will be to the right of the mid-point in out sorted list.

<br>

### Example ###

Given this value and this list: 

<br>

`val = 8, list = [1,2,3,4,5,6,7,8,9]`

<br>

First, Binary Search finds the current mid-point:

<br>

`mid_point = 5`

<br>

Binary Search will then compare our value with our mid-point:

<br>

`is val ( > or = or < ) 5?` --> `val > 5`

<br>

Binary Search now knows that our value is greater than `5`, so it will repeat its search process starting again at the next element in our list, `6`, and find the mid-point between `6` and the end of our list `9`.

<br>

`mid_point = 7`

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

# Iterative Binary Search #

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

    # continue the search unless the start-point passes the end-point

        # find the mid-point of the current search range

        # if the mid-point is equal to the value, return it

        # elif the mid-point is greater than the value

            # redefine the end-point as the element before the mid-point, search again

        # else the mid-point is less than the value, 

            # redefine the start-point as the element after the mid-point, search again
    
    # if the value does not exist in the list, return -1

```
<br>

Ok. That is a lot of pseudocode. Let us go slowly and tackle each item line by line.

<br>

## Define the Function ##


Since this function is an iterative implementation of Binary Search, lets call the function `itr_bin_search`.  We will give it the parameters `list` and `val` for the given list and value respectively.

```python
def itr_bin_search(list, val):
```

Easiest step of the implementation :)

<br>

## Define a Start-Point and an End-Point ##


We need to tell our function which index to begin our Binary Search from, and which index to end at.  Seems intuitive to call these points `start` and `end`.  Since we want to begin our first Binary Search with the whole `list`, we will set the value of `start` to `0` and the value of `end` to `len(list) - 1`.

Remember: `len(list)` will give us the total number of elements inside of the list, but since lists are zero-indexed, we have to subtract `1` from `len(list)` to access the final element in `list`

```python
def itr_bin_search(list, val):
    start = 0
    end = len(list) - 1
```

Great.  Now our Binary Search will begin with the entire list.

<br>

## Continue the Search / While Loop ##


In most circumstances, if you know how many iterations a loop needs to complete its task, it is best practice to write a For Loop. However, when you do not know how many times a loop needs to repeat to finish its task, a While Loop is the best approach.

```python
def itr_bin_search(list, val):
    start = 0
    end = len(list) - 1

    while end >= start:
```

As our search range becomes smaller and smaller while looking for `val`, if at any point, the end-point becomes less than our start-point, we will not be able to find the mid-point anymore, and we should break out of our loop.

<br>

## Find and Test the Current Mid-Point  ##


We are going to combine the next two pseudocode elements together for brevity.  Our program will find the mid-point, test it to see if it equals our given value, and if it does, return it.

```python
def itr_bin_search(list, val):
    start = 0
    end = len(list) - 1
    
    while end >= start:

        mid = start + end // 2

        if mid == val:
            return "The value is located at index " + str(mid)
```

Note, `//` is <a href="https://www.w3schools.com/python/python_operators.asp"><b>floor division</b></a>.  This will divide the two ints, and round down if the result is a float.  By adding together the `start` and `end` indexes and floor dividing by `2`, we are given the index of the mid-point, which is what we were looking for.

Further, if the mid-point, `mid` is equal to our value `val` then our search is complete and we should return the index `mid`.

<br>

## Elif and Else Statements / Winnowing the Binary Search ##


The next two statements will allow our program to zero in on the location of `val` in `list` (*assuming that it exists in `list`*)

If `mid` is greater than `val`, we know that `val` would be in the sublist to the left of the mid-point.  We then will redefine `end` to be the element that immediately preceeds `mid`, and run our search again.

Conversely, if `mid` is less than `val`, then `val` would have to exist in the sublist to the right of `mid`. We then will redefine `start` to be the element that immediately follows `mid`, and run our search again.


```python
def itr_bin_search(list, val):
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

## Finishing It Up ##


 If we break out of our loop, it means that `val` was not found in `list` and we need to `return -1`.

```python
def itr_bin_search(list, val):
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

<br>

# Recursive Binary Search #

Another common implementation of Binary Search involves the use of Recursion.  Now that we understand how Binary Search works, let us solve the same problem with a Recursive solution.

<br>

```
You are given a list of ints, sorted from least to greatest. This list will only contain ints. 
Write a function that implements a Binary Search with a recursive approach.
```
<br>

Breaking it down in pseudocode.

<br>

```python

# define the function that accepts a list and a value, start-point, and end-point

    # continue the search unless the start-point passes the end-point

        # find the mid-point of the current search range

        # if the mid-point is equal to the value, return it

        # elif the mid-point is greater than the value
            
            # keep the new_start as the previous start
            # redefine the new end-point as the element before the mid-point   

        # else the mid-point is less than the value, 

            # redefine the new start-point as the element after the mid-point 
            # keep the new_end as the previous end

        # recursively call our function with the new start and end points

    # if the value does not exist in the list, return -1

```
<br>

The pseudocode is incredibly similar to the iterative approach.  This will help us understand the recursive implementation!

<br>

## Define the Function ##

Keeping with the theme, let us call this function `rec_bin_search`.  We will give it the parameters `list` and `val` just like before, however, in this approach, we will also pass `start` and `end` as parameters, rather than define them within the function.  Why we do this will become more clear as we move on.

```python
def rec_bin_search(list, val, start, end):
```

Off to a nice start!

<br>

## Continue the Search Base Case ##

In the iterative solution, this is where we built our While Loop and defined it's base case.  In the Recusive solution, we simply drop the While Loop, and replace it with an if statement.

```python
def rec_bin_search(list, val, start, end):
    if end >= start:
```
This will serve a similar purpose in that if the start point ever crosses the end point, we know that `val` does not exist in `list` and we should break out of our recursive loop.

<br>

## Find and Test the Mid-Point ##

This is identical to our iterative implementation. Don't forget about floor division `//`.

```python
def rec_bin_search(list, val, start, end):
    if end >= start:
        mid = (start + end) // 2
     
        if list[mid] == val:
            return "The value is located at index " + str(mid)
```
Moving right along :)

<br>

## Elif and Else Statements / Winnowing the Binary Search ## 

Just like before, our function needs to drill down to  our value, using the Binary Search process.  However, in each instance we will need to establish a `new_start` and a `new_end` because we are setting up our parameters for our recursive call.

If `mid` is greater than `val`, we know that `val` would be in the sublist to the left of the mid-point.  We then will define `new_start` to be equal to the previous `start` and `new_end` to be the index that immediately preceeds `mid`.

Conversely, if `mid` is less than `val`, then `val` would have to exist in the sublist to the right of `mid`. We then will define `new_start` to be equal to the index that immediately follows `mid` and define `new_end` to be equal to the previous `end`.


```python
def rec_bin_search(list, val, start, end):
    if end >= start:
        mid = (start + end) // 2
     
        if list[mid] == val:
            return "The value is located at index " + str(mid)

        elif list[mid] > val:
            new_start = start
            new_end = mid - 1
            
        else:
            new_start = mid + 1
            new_end = end
```
This is why we passed in the `start` and `end` parameters in the function definition of `rec_bin_search`.  We now have our new arguments to pass in to our recursive calls.

<br>

## Recursively Call Our Function ##

Recall that Recursion if a function that calls itself.  A few things that are necessary in every recursion:

  * a base case (*to break our recursive loop*)
  * a return statement (*to return our result back up the stack*)
  * an invocation with arguments (*if you don't call it, it won't recurse*)

```python
def rec_bin_search(lst, val, start, end):
    if end >= start:
        mid = (start + end) // 2
     
        if list[mid] == val:
            return "The value is located at index " + str(mid)

        elif lst[mid] > val:
            new_start = start
            new_end = mid - 1
            
        else:
            new_start = mid + 1
            new_end = end
     
        return rec_bin_search(lst, val, new_start, new_end)
```
We have our base case (*both if statements*), our return statement (*we return the recursive call*), and our invocation (*we call rec_bin_search with out new parameters*).  We are almost done!

<br>

## Finishing It Up


The last bit of business to attend to is if our function does not find `val` in `list`.  Just like before, we will `return -1` in this instance.

```python
def rec_bin_search(list, val, start, end):
    if end >= start:
        mid = (start + end) // 2
     
        if list[mid] == val:
            return "The value is located at index " + str(mid)

        elif list[mid] > val:
            new_start = start
            new_end = mid - 1
            
        else:
            new_start = mid + 1
            new_end = end
     
        return rec_bin_search(list, val, new_start, new_end)
  
    else:
        return -1

```
 
 <br>

 Boom.  A Recursive implementation of Binary Search in Python.  

 <br>

 For additional resources, check out <a href="https://www.geeksforgeeks.org/binary-search/"><b>Geeks for Geeks</b></a>.  They have implemented Binary Search in many different languages and have a few other links that elaborate on this algorithm.