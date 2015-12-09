## Activities vs. Fragments

The basics of android apps revolve around the MVC pattern where we define the model, view and controller as such:

Model: What to display

View: How to display

Controller: How the user interacts with the display

Every app you build will start with one activity, where more complex apps should be composed of many activities and fragment. In the MVC hierarchy, an Activity functions as a wrapper for the view and controller, containing inflators for screen display while also helping create elements of the controller.
Fragments, which were added in API 11, were originally designed for use in tablets but their use as reusable building blocks of apps is important for all handheld devices. Creating general and well-thought out fragments can make your lives much easier in the long run. Take the example of a news application (taken from http://developer.android.com/guide/components/fragments.html#Design):

![alt text](http://developer.android.com/images/fundamentals/fragments.png "Fragments Example")
 
In this case, creating a multiple fragments inside of the activity helps remove the stress of having to update the entire activity every time another item is selected. In the handset version, the benefits are not as immediately clear. However, by using the same fragments from the tablet version, we can make our application compatible with both with minimal work. This also applies to adding or modifying features in your app. By using modular fragments rather than a single activity for each page, changing part of the functionality of your app can be done by rewriting a single fragment, rather than having to potentially modify your entire activity.

## Lifecycle of an App:

An application begins by starting and Activity, which in turn inflates whatever fragments, buttons or other objects it contains using the proper XML files to determine location, size and more. This original activity persists for the entire lifecycle of the app. Any fragment or other activities created by the original activity or any of its children can be created and destroyed without affecting the original. There are some cases where the operating system and memory management will close activities to free up memory but you will probably not be dealing with these problems till later in the course. For more information: http://developer.android.com/reference/android/app/Activity.html#ActivityLifecycle 
