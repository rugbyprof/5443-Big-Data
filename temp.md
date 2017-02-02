```python
"""
Name: Stephanie Nagel
Email: feorae@hotmail.complex
Assignment: Homework 1 - Lists and Dictionairies
Due Date: 1/31
"""

#Problem A: What would Python print? 

print('A:')
a = [1, 5, 4, 2, 3] 
print(a[0], a[-1])
# Prints: (1, 3)

a[4] = a[2] + a[-2]
print(a)
# Prints: [1, 5, 4, 2, 6]

print(len(a))
# Prints: 5

print(4 in a)
# Prints: True

a[1] = [a[1], a[0]]
print(a)
# Prints: [1, [5, 1], 4, 2, 6] where a[1] becomes a tuple

print

#Problem B: Write a function that removes all instances of an element from a list.

print('B:')
x = [3, 1, 2, 1, 5, 1, 1, 7]
def remove_all(i, lst):
  while i in x:
    x.remove(i)
remove_all(1, x)
print(x)
print

#Problem C: Write a function that takes in two values, x and y, and a list, and adds as many y's to the end of the list as there are x's. Do not use the built-in function count.

print('C:')
lst = [1, 2, 4, 2, 1]
def add_this_many(x, y, lst):
  for i in lst:
    if i == x:
      lst.append(y)
add_this_many(1,5,lst)
print(lst)
print

#Problem D: What would Python print?

print('D:')
a = [3, 1, 4, 2, 5, 3]
print(a[:4])
# Prints: [3, 1, 4, 2]

print(a)
# Prints: [3, 1, 4, 2, 5, 3]

print(a[1::2])
# Prints: [1, 2, 3]

print(a[:])
# Prints: [3, 1, 4, 2, 5, 3]

print(a[4:2])
# Prints: []

print(a[1:-2])
# Prints: [1, 4, 2]

print(a[::-1])
# Prints: [3, 5, 2, 4, 1, 3]
print

#Problem E: Let's reverse Python lists in place, meaning mutate the passed in list itself, instead of returning a new list. Why is the "in place" solution preferred?
print('E:')
x = [3, 2, 4, 5, 1]

print('Hard way:')
def reverse(lst):
    hiInd = len(lst) - 1
    revNum = len(lst)/2
    for i in range(0, revNum):  
        temp = lst[hiInd]
        lst[hiInd] = lst[i]
        lst[i] = temp
        hiInd -= 1
reverse(x)
print(x)
print
print('Easy way:')
x.reverse()
print(x)
print

#In place is probably easier to keep track of since it won't need to be assigned a new address

#Problem F: Write a function that rotates the elements of a list to the right by k. The function will return a new list.
print('F:')
x = [1, 2, 3, 4, 5]
def rotate(lst, k):
     return (lst[-k:] + lst[:-k]) #Negative used to push values to the right
y = rotate(x,3)
print(y)
print

#Problem H: What would Python print?
print('H:')
superbowls = {'joe montana': 4, 'tom brady':3, 'joe flacco': 0}
superbowls['peyton manning'] = 1
superbowls['joe flacco'] = 1

print('colin kaepernick' in superbowls)
#Prints: False

print(len(superbowls))
#Prints: 4

print(superbowls['peyton manning'] == superbowls['joe montana'])
#Prints: False

superbowls[('eli manning', 'giants')] = 2
print(superbowls)
#Prints: {'joe flacco': 1, ('eli manning', 'giants'): 2, 'joe montana': 4, 'peyton manning': 1, 'tom brady': 3}

superbowls[3] = 'cat'
print(superbowls)
#Prints: {3: 'cat', 'peyton manning': 1, ('eli manning', 'giants'): 2, 'joe flacco': 1, 'joe montana': 4, 'tom brady': 3}


superbowls[('eli manning', 'giants')] =  superbowls['joe montana'] + superbowls['peyton manning']
print(superbowls)
#Prints: {3: 'cat', 'peyton manning': 1, ('eli manning', 'giants'): 5, 'joe flacco': 1, 'joe montana': 4, 'tom brady': 3}

superbowls[('steelers', '49ers')] = 11
print(superbowls)
#Prints: {3: 'cat', 'peyton manning': 1, ('steelers', '49ers'): 11, ('eli manning', 'giants'): 5, 'joe flacco': 1, 'joe montana': 4, 'tom brady': 3}
print

#Problem I: Given a dictionary replace all occurrences of x as the value with y.

#So lost on this one


#Problem J: Given a (non-nested) dictionary delete all occurences of a value.
print('J:')
d = {1:2, 2:3, 3:2, 4:3}
def rm(d, x):
  filter(lambda x: x != 2, d) #It worked and then it didn't -____-
rm(d, 2)
print d

```
