# More Java Concepts

### Variable Scope and Access Modifiers

When you create a variable, depending on where its created it can be used by a variety of different classes. The three main areas we will focus on are, class scope, method scope, and loop scope. Class\_var, method\_var, and Loop\_var are defined in the scopes from above. Class scope means that are able to be accessed from anywhere within the class. Method scope means that they are able to be accessed from only within that method. Loop scope, means that the loop variable can only be accessed from within the loop. The snippet below defines a class variable class\_var, a method variable method\_var and a loop variable loop\_var.

``` Java
public class BaseApplication{
    public class_var;
    public void doStuff() {
        int method_var = 20;
        for(int loop_var=0;loop_var<method_var;loop_var++)
        {
           Systen.out.println("Loop_var "+loop_var);
        }
    }
}
```
In general, a pair of curly braces defines a new scope and a variable defined within the braces can **usually** be accessed anywhere within these braces.

There are four access modifiers we will be discussing, public, private, protected, and default. A public method/variable is accessible by any class and should be used with reason rather than as a default. Private method/variable is accessible by only the class it is created in, while a protected method/variable is accessible by the class that created it and any subclass of that class. If you compile a variable without any of those modifiers, it will use the default modifier, which is package protected.In that case, only classes within the package can access. 

### Interfaces
An Interface is a collection of related abstract methods. Imagine a 5 or so different television classes, each with its own dimensions and brand. However, every television has to have a common set of methods, such as turnOn(), turnOff(), changeChannel() etc. An easy way of creating a level of compatibility between these televisions is to define an interface that holds all these basic accessibility methods as abstract methods. An abstract method does not have a body but defines return type and input variables. By implementing an interface, you are saying that this class will have all the methods of the interface as non-abstract methods. An example is shown below with an OnClickListener interface.
``` Java
public class BaseApplication implements OnClickListener{
    @Override
    public void onCreate(Bundle savedInstanceState){
        //Do Stuff Here
    }
    
    @Override
	public void onClick(View v) { 
	    //Do Stuff Here
	}
}
```

### Inheritance and Polymorphism
Inheritance is when you create a class that extends from another class. In this class the extended class is called the parent, or superclass, and the created class is called the child, or subclass. A subclass has access to all of the protected and public methods/variables of the superclass and can create new methods or override superclass methods. This allows to you use a heirarchy of classes in order to prevent implementing identical code multiple times. Polymorphism is a case of inheritance where you parent reference in order to refer to a child class object. An example is shown below:

```Java
public class Bicycle {
    //Variables
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        //Constructor
    }
    //Methods
}
public class MountainBike extends Bicycle {
    //Private MountainBike Variables
    public MountainBike(int startCadence, int startSpeed, int startGear, String suspensionType){
        super(startCadence, startSpeed, startGear);
        //Constructor
    }
    //MountainBike Methods
}
public class RoadBike extends Bicycle {
    //Private RoadBike Variables
    public RoadBike(int startCadence, int startSpeed, int startGear, int newTireWidth){
        super(startCadence, startSpeed, startGear);
        //Constructor
    }
    //RoadBike Methods
}

public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03;

    bike01 = new Bicycle(20, 10, 1);
    bike02 = new MountainBike(20, 10, 5, "Dual");
    bike03 = new RoadBike(40, 20, 8, 23);

    bike01.printDescription();
    bike02.printDescription();
    bike03.printDescription();
  }
}
```

In this example, we create 3 different bicycles, but reference each as a Bicycle(parent) rather than as their individual children. This may seem useless but actually hides a very powerful concept. By overriding the parent method in the children, and describing each of the created bikes as the parent class, we are able to call printDescription() without having to know the exact subclass we are using. Some more concrete and familiar examples of this are the x.toString() operator and the + operator.

### Static vs Final
Methods, variables, and classes can all be either static, final or both. Static variables are tied to classes, rather than a particular instance of the class and can only be initialized once. Static methods, much like static variables are tied to classe not instances and can only access static data unless it creates an instance of a class. Static methods are also unable to use the *this* or *super* keywords. Static classes can only exist in nested form, as top level static classes do not exist in java. A nested static class is a class that has no references to the outside class; a static class can contain both instance and static methods. One common static item is the main method, which must be static so the application can call it before anything has been initialized. The final keyword is used generally to prevent a method, variable, or class from being modified later. A final variable can only be initiazlied once, while a final method cannot be overridden by a subclass and a final class can be subclassed. Many of the standard java library classes are final, such as java.lang.String.


