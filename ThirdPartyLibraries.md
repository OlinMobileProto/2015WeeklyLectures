# Third Party Libraries

Third party libraries are created as shortcuts for things that might be a bit arduous to do with built in libraries and classes. They save a lot of time and energy by generating code for you.

#### Otto Event Bus
[Event Bus](http://square.github.io/otto/) is a library that allows for communication between fragments. It essentially replaces your need for a singleton or storage within the activity to carry over between fragments.

To use Event Bus, you need to add the following dependency to your gradle file:
``` Java
compile 'com.squareup:otto:1.3.8'
```
Create a bus in your Application class:
``` Java
public class BaseApplication extends Application{
    private static Bus mEventBus;

    public static Bus getEventBus() {
        return mEventBus;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        mEventBus = new Bus(ThreadEnforcer.ANY);
    }
}
```
The ThreadEnforcer.ANY input just allows the bus to work on any thread instead of only allowing it to run on the main thread. This is not necessary, but can be included for best practice's sake. Next you should create a custom event:

``` Java
public class CustomEvent {
    public String message;

    public CustomEvent(String message) {
        this.message = message;
    }
}
```

Now create methods to catch bus events (make sure to add the @Subscribe annotation):
``` Java
    @Subscribe
    public void onCustomEvent(CustomEvent event) {
        //do something with your event!
    }
```

Wherever you add a subscribe method, you will need to include the following line in the overarching class's onCreate method in order to register the class with your bus:
``` Java
BaseApplication.getEventBus().register(this);
```

All you have to do now is create events by calling this method from anywhere in your code:
``` Java
BaseApplication.getEventBus().post(new TestEvent("test message"));
```


#### ButterKnife

[ButterKnife](https://github.com/JakeWharton/butterknife) is essentially an automatic view injector with some additional features. It heavily simplifies XML-Java interfacing, such that you might never have to use findViewById() again! Here are some basic usages:

```
class MainActivity extends Activity {
  @Bind(R.id.save_button) Button saveButton;
  @Bind(R.id.guest_list) ListView guestList;
  @Bind(R.id.guest_edit) EditText guestEdit;
  
  @OnClick(R.id.save_button)
  public void save(View view) {
    // function call to save guests to list
}

  @OnItemSelected(R.id.guest_list)
  void onItemSelected(int position) {
     // fuction call to create dialog box for editing and deleting
    }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ButterKnife.bind(this);
  }
}
```

Above is some similar functionality to what you worked on in Lab 1. Think of the @Bind annotation as a replacement for findViewById (which is exactly the code it generates). We have a button with an on click listener and a list with an on item clicked listener, but significantly more clean and concise than what you would have to write without ButterKnife. They are also already portioned into their own methods, although as you guys know, these should likely not be in your MainActivity class. Notice that you do need to add a line to the onCreate of the classes in which you use the library or it will not work. The only thing left to do to use the library is add this line to your build.gradle dependencies:

```
compile 'com.jakewharton:butterknife:7.0.1'
```
