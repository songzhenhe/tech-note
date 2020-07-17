# Function

## zip() Function


``` python
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica", "Vicky")

x = zip(a, b)
```

``` python
name = [ "Manjeet", "Nikhil", "Shambhavi", "Astha" ] 
roll_no = [ 4, 1, 3, 2 ] 
marks = [ 40, 50, 60, 70 ] 
mapped = zip(name, roll_no, marks) 
# converting values to print as set 
mapped = set(mapped) 
# printing resultant values 
print ("The zipped result is : ",end="") 
print (mapped)

# output
The zipped result is : {('Shambhavi', 3, 60), ('Astha', 2, 70),
('Manjeet', 4, 40), ('Nikhil', 1, 50)}
```

``` python
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
zipped = zip(numbers, letters)
type(zipped)

# output
<class 'zip'>

# zip() function returns an iterator, use list() to consume the iterator
list(zipped)
# output
[(1, 'a'), (2, 'b'), (3, 'c')]
```