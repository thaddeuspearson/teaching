# Sum all the numbers in a multi-dimensional list in Python

<details><summary><b>TL;DR... Give me the code already!</b></summary>

```python
def multi_dim_list_sum(lst):
    sum = 0

    # iterate through the list
    for item in lst:

        # test the item to see if it is an array
        if type(item) == type([]):
            
            # call the multi_dim_sum_list function recursively
            sum += multi_dim_sum_list(item)

        else:

            # if the item is an int, add it to the sum
            sum += item
    
    # return the sum
    return sum
```
</details>

<br>


Summing all of the numbers in a multi-dimensional list (or array) is a very common coding challenge.  It is highly prevalent because it is an excellent use case to demonstrate the concept of recursion.  Consider the following code challenge:


<br>

```
You are given a list. This list will only contain numbers (ints), or more lists. Write a function that adds up all of the numbers existing within the parent list.
```
<br>


Sounds easy enough, but this one is *tricky*. Let's break down this problem with some pseudocode. 


<br>

```python
# define the function that accepts a list

    # store a total or sum

    # iterate through the list:

        # if the current item is a list:
            
            # handle the list

        # else: add the current item to the sum

    # return the sum

```
<br>


Cool. We have our to-do list, let's do it one step at a time!


<br>

## Define a Function That Accepts a List


This is a pretty simple task. Let's name the function `multi_dim_list_sum` and lets give it the parameter `lst`


```python
def multi_dim_list_sum(lst):
```

Easy peasy.


<br>

## Store a Total or Sum


If we are going to add up numbers, then we will need a total.  Since we are adding, let's create a variable called `sum` and start it at 0.


```python
def multi_dim_list_sum(lst):
    sum = 0
```

Our `sum` is defined within the scope of the function, and it will keep track of the grand total.


<br>

## Iterate Through the List


We will need to look at each element (`elem`) inside the list one at a time. This is an excellent opportunity to use a `for` loop.


```python
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
```

Excellent. We are looking at each `elem` one at a time. Here is some more info on <a href="https://www.w3schools.com/python/python_for_loops.asp">python for loops</a>


<br>

## If the Current Item is a List:


In this coding challenge, each `elem` inside of our list will either be a number or another list. we will need to write an `if` statement to test if the current element is a list.


```python
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
        if type(elem) == type([]):
```

Let's unpack this one a bit. This statement uses python's <a href="https://www.geeksforgeeks.org/type-isinstance-python/">type method</a>.  This will evaluate what data type is passed into it. In our function, we are comparing the `type` of the current element `elem` to see if it is <a href="https://dbader.org/blog/difference-between-is-and-equals-in-python">strictly equal</a> `==` to the type of an empty list `[]`.  If this statement returns true, our function will step inside of the `if` statement. **Note, the "is" operator would also work in this instance, because we are comparing the type of both.**


<br>

## Else: Add the Current Item to the Sum


I am skipping the next step for a second to complete our `if/else` statement.  We will come back to what happens inside the if statement in a moment.


In the case that the current element is a number, we want to add it to our `sum`. We are given the fact that the `elem` is definately a number, because if it were a list, our program would have stepped inside of our if statement.  So let's add our number to our `sum`!


```python
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
        if type(elem) == type([]):
            # We will get to this part soon
        else:
            sum += elem
```


So our function has determined that the current element is a number, and it has added it to our `sum`. Our function is starting to look pretty good!


<br>

## Return the Sum


Since we are at the end of our function already, let's finish things up by returning our `sum` when our `for` loop returns.


```python
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
        if type(elem) == type([]):
            # We will get to this part soon
        else:
            sum += elem
    
    return sum
```

Awesome.  Now our function returns our `sum` when it is done going through our initial list and adding each number to the `sum`. Take note, we placed the indentation for the `return` statement in line with the `for` loop, because we want the entire `for` loop to finish, *before* we `return` our `sum`.


<br>

## Handle the List


Alright, now let's backtrack, and handle the case when the `elem` is a list, and not a number.


So, if our program steps inside the if statement we just created, we know the current `elem` is a list. But we can't add a list to a number. We also know that the current list may have numbers inside of it, or it might have more lists inside of it. We don't know how many layers the lists within the list go. We need to test the current list to see if it has numbers or lists inside of it.


Wait a minute!  Isn't that what our function already does?  Doesn't it take a list, look through it, and see if the current `elem` is a number or a list?  What if we could call our function again and test this current element (which is a list) and see if there are any more lists inside of it?  We can absolutely do that. This is called recursion.  Let's study this for a second.

<br>

## What is Recursion?

From <a href="https://https://www.geeksforgeeks.org/recursion/">GeeksforGeeks</a>:


> The process in which a function calls itself directly or indirectly is called recursion and the corresponding function is called as recursive function.

or more simply put:

> A function that calls itself.


We are going to call our function, within our function.  Because of our if statement, this recursion will only happen in our function if the current `elem` we are evaluating is a list.  When our function finda a list, it will re-call itself with the list that it found! 


```python
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
        if type(elem) == type([]):
            sum += multi_dim_list_sum(elem)
        else:
            sum += elem
    
    return sum
```

We are calling a new instance of our function `multi_dim_list_sum([3, 4])`, within our original function `multi_dim_list_sum(test_list)`, with the current element `[3, 4]`, which is a list `type([3, 4])` ====> `class 'list'`, and we are adding that to our `sum`. This might also need a little unpacking.  


You might be thinking, but Thaddeus, how can I add a function to a sum (which is a number)?!  Let's consider for a moment, what does our function *return?*


...a sum, right?  


Yes.  Our function returns a sum.  Which is a number!  We can add numbers to other numbers. Let's break this down in some code. 


```python
# here is our function
def multi_dim_list_sum(lst):
    sum = 0

    for elem in lst:
        if type(elem) == type([]):
            sum += multi_dim_list_sum(elem)
        else:
            sum += elem
    
    return sum

# here is our test_list
test_list = [1, 2,[3, 4]]

# here is us calling our function
multi_dim_list_sum(test_list)

# first, our function iterates through our list, and the first elem in test_list (test_list[0]) is 1. Because 1 is a number and not a list, we hit our else statement:
    else:
        sum += 1

# now sum = 1, and we move on to our next elem in our test_list (test_list[1]), which is 2. Because 2 is a number and not a list, we hit our else statement again:
    else:
        sum += 2

# now sum = 3, and we move on to the third elem in test_list (test_list[2]) which is [3, 4]. Because our third elem is a list, we hit our if statement:
    if type(elem) == type([]):
        sum += multi_dim_list_sum([3, 4])

# here is where the recursion happens. Our original function "pauses" and our original sum variable is "saved" at 3. We begin to run this new instance of our function, with our new list, [3 , 4] and a new sum starting at 0. Our new instance starts with the first elem of our new list, which is 3. Since 3 is a number, it hits our else statement, and adds 3 to our new sum:
    else:
        sum += 3

# our new instance moves on to the second elem in our new list, which is 4.  We hit our else statement, and add 4 to our new sum:
    else:
        sum += 4

# we are now at the end of our for loop. Our new instance is ready to return our new sum, which is 7, back to our original function. Our original function now takes that return value, "unpauses" itself, and evaluates the original if statement. 
    if type(elem) == type([]):
        sum += 7

# our sum is now 10 and we are finished with our original for loop.  Our function now returns the sum, which is 10.

    print(return sum) =====> 10

```
<br>


What is really cool about our function is that it will handle any amount of lists within a list, provided that the only thing any of these lists contain are eithermore lists or numbers.


For example, it would be able to evaluate this crazy list:


<br>

```python

crazy_list = [2, 7, [2, [2 , 3]], 4, [[1, [3, [[[[8]]]], 6], 6], 2], 4]

multi_dim_list_sum(crazy_list) ====> 50

```
<br>


And that is how you sum a multi dimensional list in python with recursion! If you would like to see some python recursion in action, check out <a href="https://www.youtube.com/watch?v=wMNrSM5RFMc">this video.</a>


