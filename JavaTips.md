### Java highlights knowing Python

It is likely that the language you have most experience with is Python. Knowing Python, here are some points you will most likely be confused about

#### Everything is a class:

In Java, no variables exist outside of classes. This means that even for a simple program to print "Hello world" (which in Python is just `print("Hello world")`), the code would look like the following:

``` Java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("Hello, World");
    }

}
```

This section of code creates a class (HelloWorld), and prints "Hello, world" in its *main* function. The *main* function is the code that is run. However in Android development, you're unlikely to see any *main* functions, as the system handles that for you. 

#### Primitives and other data types

There are many, many classes you need to use when developing for Android. The following classes are primitives (and you should know what they all are from Python).

``` Java
byte
short
int
long
float
double
boolean
char
```

"String" is a Java class that represents a string. In some cases, the "String" class also behaves like a primitive. 

In java, all non-primitive classes (including classes you create), should be capitalized on the first letter. All instances of any class should be lowercase on the first letter. So, "String" is a class, and "string" is an instance of that class. 

#### Variable Initialization:

Variables in Java are strictly typed meaning they are assigned a type and have to stay that way they also need to be initialized with that type.

##### Python:

stringVariable = “Hello”

##### Java:

1. String stringVariable = new String(“Hello”)

or

2. String stringVariable = “Hello”

For most objects, you must use the *new* syntax in example 1. Only primitive types, including "String"s, int, long, boolean can be initialized by the syntax in example 2.

#### Method declaration:

``` Java
scope [static] returnType methodName(Type1 var1, Type2 var2) {
}
```

What each keyword means:

1. scope means which other classes can access this function. Usual values are public and private. "public" means that any other class can call this function. This should always be used with a few exceptions. "private" means that the function can only be called from inside this class. For more information, [see here](http://stackoverflow.com/questions/215497/in-java-whats-the-difference-between-public-default-protected-and-private)

2. the static keywork is optional. "static" means that it is a class function. You don't call it on an instance of the class, you call it on the class itself. You call it with `Classname.method()` instead of `classInstance.method()`. 

3. returnType is the type that the function returns. You must declare this. If the function doesn't return a variable, insert "void" here. 

4. Each input variable must have its type declared also.

An example of a method follows:

``` Java
public String myMethod(String var1, ArrayList var2) {
)
```

#### Inheritance

In Java you use the keyword "extends" to declare the super type. For example:

``` Java
public class MountainBike extends Bicycle {
```

The class "MountainBike" is a subclass of "Bicycle". 

In Java, you use the "implements" keyword to declare that a class implements the functions declared in an "interface". An example:

``` Java
public interface Relatable {
    public int isLargerThan(Relatable other);
}

public class Rectangle implements Relatable {

	...

	public int isLargerThan(Relatable other) {
		return (other.area < this.area);
	}
}
```

The Relatable is the interface. It doesn't actually implement the functions it declares. Rather, the function is implemented in the Rectangle class. This is useful because you can have many classes that you know will have the same function. For example if I create a class Triangle that also implements Relatable, I can compare any shape that implements Relatable without needing to know which specific shape it is.

For more information, [read here](http://www.tutorialspoint.com/java/java_interfaces.htm)

#### Things you might see you have never seen in python:

##### this

"this" is equivalent to "self" in Python. "this" refers to the current instance. 

##### the word static:

"static", as explained above, simply means that the method or variable belongs to the class and not an instance of the class. [Read here](http://stackoverflow.com/questions/2649213/in-laymans-terms-what-does-static-mean-in-java)

##### Casting:

Casting is the process of converting an object to one of its subclasses. For example, the function getActivity() always returns a variable of type Activity. However, you usually have already subclassed it, so you can cast it to your type. 

castedObject = (String)otherVariable

[Read here](http://stackoverflow.com/questions/5289393/casting-variables-in-java)





