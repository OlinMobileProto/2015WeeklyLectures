## Android best practices

###Strings for display/string.xml file

Android convention is that there is an xml file known as string.xml that should be used to store all strings you wish to use for DISPLAY in your application. This is so that it is easy to find the name of text you wish to change and you can easily support new languages by adding additional string.xml files. Values in the string.xml file should be references in other display xml files.

String.xml is located in app/res/values

####To add a value to string.xml:

```XML
<string name="add_button">Text to show</string>
``` 
We can either add that line to the string.xml file manually or...

Android Studio has a shortcut to do this. On strings that should be in strings.xml such as this line in an xml file: 
```
android:text="Hi"
``` 
Hit Alt + Enter and Select Extract String. A dialog will pop up and simply naming the resource will properly setup the string 

####Referencing a value in the string.xml file :

In XML file:

```
android:text="@string/add_button"
```



####String resource naming conventions:

The resource name of a string defined in string.xml should be written in lowercase snake case. meaning words should look like add_grocery_button

The same thing should be done for dimensions in the file dimens.xml. The purpose of this is so you can set different dimensions for radically different screen sizes.

### Java Naming Conventions

####ClassNames:

Camelcase, with capital first letter

```Java
public MyExampleClass {
}
```

####Instance Names:

An instance of a class should be named in camelcase with a relevant and helpful name.

Example:
```Java
ArrayList<String> phoneNumberList = new ArrayList<String>();
```


####Method Names:

Method names should be done in camelcase with a descriptive name.

A method that removes anitem from a grocery list in an app should be called somethin like
```Java
public boolean deleteEntryFromGroceryList() {
}
```



####Strings in java code:

It is good java practice to define strings at either the top of a class or in a separate String constants final. 
Say for example in some method you have a map of parameters that you need to add to in order for a request to a service to work. Java code to do that could look like

```Java
HashMap<String, String> params = new HashMap<String, String>();
params.put("searchable","yes");
params.put("region","US");
```

However, it is not good practice to write those strings at that location. What should be done is either define the strings at the top of the class like so:

```Java
public class ExampleActivity {
private static final String SEARCHABLE_PARAM = “searchable”;
private static final String REGION_PARAM = “region”;
private static final String SEARCABLE_VALUE = “yes”;
private static final String REGION_VALUE = “US”;
```

and then reference them in code tlike this:

```Java
params.put(SEARCHABLE_PARAM,SEARCHABLE_VALUE);
```
The alternative is to have a separate file where all of these constants are stored. For example:
```Java
public class ServiceConstants { 
private static final String SEARCHABLE_PARAM = “searchable”;
private static final String REGION_PARAM = “region”;
private static final String SEARCABLE_VALUE = “yes”;
private static final String REGION_VALUE = “US”;
}
```

and then reference them in code 
like so
```Java
params.put(ServiceConstants.SEARCHABLE_PARAM, ServiceConstants.SEARCHABLE_VALUE);
```