## Fragments

### Transition to Fragments in Activity

``` Java
    public void transitionToFragment(Fragment fragment) {
        FragmentManager fm = getSupportFragmentManager();
        FragmentTransaction transaction = fm.beginTransaction();
        transaction.replace(R.id.container, fragment);
        transaction.commit();
    }
```

In this case, container must be the id of a FrameLayout. The FrameLayout is all that should reside in the Activity's XML, as here:

``` XML
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:ignore="MergeRootFrame" />
```

### Get the Activity

From any Fragment, you can call `getActivity()` to get the current Activity. 
