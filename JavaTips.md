### Java highlights knowing Python

It is likely that the language you have most experience with is Python. Knowing Python, here are some points you will most likely be confused about


#### Variable Initialization:

Variables in Java are strictly typed meaning they are assigned a type and have to stay that way they also need to be initialized with that type.

##### Python:

stringVariable = “Hello”

##### Java:

1. String stringVariable = “Hello”

or

2. String stringVariable = new String(“Hello”)

Most times when you create a new object you need to use the syntax in example 2. Certain types, like Strings, longs, ints can be initialized by the syntax in  example 1.

#### Method declaration:

public String myMethod(String var1, ArrayList var2) {
)

##### Breakdown of syntax:

public - any java class may call this method, there is also protected and private. Breakdown of each one
http://stackoverflow.com/questions/215497/in-java-whats-the-difference-between-public-default-protected-and-private

String - return type of the method. Can be void if no return

Arguments must be typed. Indicating what type is expected as an argument

#### Things you might see you have never seen in python:

##### the word static:

http://stackoverflow.com/questions/2649213/in-laymans-terms-what-does-static-mean-in-java

##### Casting:

castedObject = (String)otherVariable
http://stackoverflow.com/questions/5289393/casting-variables-in-java



