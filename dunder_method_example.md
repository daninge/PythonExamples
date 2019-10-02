Say we have a class to represent a Dog, that looks like the following:

``` python
class Dog(object):
    def __init__(self, height, weight):
        self.height = height
        self.weight = weight
```

Let's make two different Dog objects with the same height and weight:

``` python
dog1 = Dog(10, 4)
dog2 = Dog(10, 4)
```

Now let's say we want to be able to compare whether dog1 and dog2 have the same height and weight. 

We notice if use Python's '==' operator to compare the Dog objects, Python says dog1 and dog2 aren't the same.

This is because Python knows that dog1 and dog2 are different objects:

``` python
print(dog1 == dog2) # Prints False
print(dog1 == dog1) # Prints True
```
Python doesn't have any way of knowing that we want to consider two Dogs as equal iff they have the same weight and height, and not just if they are the exact same dog.

To get around this let's say we modify our Dog class to write an equals() method. This method will return True if the passed in Dog object has the same height and weight as the Dog object upon which the method is called.

For example we modify our Dog class to look like:

``` python
class Dog(object):

    def __init__(self, height, weight):
        self.height = height
        self.weight = weight

    def equals(self, another_dog):
        return (self.height == another_dog.height 
                and self.weight == another_dog.weight)
```

We can now check if two dogs have the same height and weight by doing the following:

``` python
dog1 = Dog(10, 4)
dog2 = Dog(10, 4)
dog3 = Dog(5, 3)

print(dog1.equals(dog2)) # This returns True
print(dog2.equals(dog1)) # This returns True
print(dog1.equals(dog3)) # This returns False
```

So this is good because we can now compare Dogs using our new equals method. However, purely for convenience, it would be nice if we could tell Python to just always use our custom equals method whenver we compare Dogs using the '==' operator.

This is where Dunder (double underscore) methods come in. These are special methods that we never call directly, but Python itself calls when evaluating an expression.

One of these methods is ```__eq__```. Python will call this function on one of the objects that you compare with the '==' operator and then return the result.

For example we can rename our equals() function to ```__eq__```:

``` python
class Dog(object):
    def __init__(self, height, weight):
        self.height = height
        self.weight = weight

    def __eq__(self, another_dog):
        return (self.height == another_dog.height 
                and self.weight == another_dog.weight)
```

We can now compare our Dog objects using Python's '==' operator and the correct result will be produced:

``` python
dog1 = Dog(10, 4)
dog2 = Dog(10, 4)

print(dog1 == dog2) # This returns True
print(dog2 == dog1) # This returns True

dog3 = Dog(5, 3)

print(dog1 == dog3) # This returns False

print(dog1.__eq__(dog3)) # This returns False. This is the equivalent of dog1 == dog3.
```



