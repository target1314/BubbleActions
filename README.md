#BubbleActions [ ![Download](https://api.bintray.com/packages/samthompson/maven/bubble-actions/images/download.svg) ](https://bintray.com/samthompson/maven/bubble-actions/_latestVersion) 

Inspired by the Pinterest Android app, `BubbleActions` make it easy to perform actions 
on ui elements by simply dragging your finger.

##Screenshots
1 | 2 | 3
--- | --- | --- 
![1](http://i.imgur.com/jbI6Bay.gif) | ![2](http://i.imgur.com/YEtNBmn.gif)  | ![3](http://i.imgur.com/BKllyFY.gif)


##Requirements and dependencies
`BubbleActions` works with api level 11 and higher. It also is dependent on appcompat-v7.


##Gradle
In your top-level `build.gradle`:
```groovy
repositories {
        jcenter()
}
```

In your project-level `build.gradle`:
```groovy
compile 'me.samthompson:bubble-actions:1.3.0'
```


##Samples

####Building BubbleActions
`BubbleActions` are built using a [fluent interface](https://en.wikipedia.org/wiki/Fluent_interface) 
(similar to SnackBar) and supports adding up to 5 actions. You can build `BubbleActions` like this:
```java
BubbleActions.on(myView)
        .addAction("Star", R.drawable.bubble_star, new Callback() {
            @Override
            public void doAction() {
                    Toast.makeText(v.getContext(), "Star pressed!", Toast.LENGTH_SHORT).show();
                }
            })
        // ... add more actions ...
        .show();
```
Every action in BubbleActions has 3 parts:

1. an action name that will be displayed above the bubble,
2. a drawable for the bubble itself, and
3. a callback that will be executed on the main thread when the user lifts their finger over that action.

####Basic example
In the activity we set a long click listener to show the `BubbleActions`:
```java
findViewById(R.id.my_view).setOnLongClickListener(new View.OnLongClickListener() {
        @Override
        public boolean onLongClick(final View v) {
            BubbleActions.on(v)
                    .addAction("Star", R.drawable.bubble_star, new Callback() {
                        @Override
                        public void doAction() {
                            Toast.makeText(v.getContext(), "Star pressed!", Toast.LENGTH_SHORT).show();
                        }
                    })
                    .addAction("Share", R.drawable.bubble_share, new Callback() {
                        @Override
                        public void doAction() {
                            Toast.makeText(v.getContext(), "Share pressed!", Toast.LENGTH_SHORT).show();
                        }
                    })
                    .addAction("Hide", R.drawable.bubble_hide, new Callback() {
                        @Override
                        public void doAction() {
                            Toast.makeText(v.getContext(), "Hide pressed!", Toast.LENGTH_SHORT).show();
                        }
                    })
                    .show();
        }
    });
```

####Kotlin example
Here's the same example as above, translated to Kotlin:
```kotlin
val textView = findViewById(R.id.text_view);
textView.setOnLongClickListener {
    BubbleActions.on(textView)
            .addAction("Star", R.drawable.bubble_star, {
                Toast.makeText(textView.context, "Star pressed!", Toast.LENGTH_SHORT).show()
            })
            .addAction("Share", R.drawable.bubble_share, {
                Toast.makeText(textView.context, "Share pressed!", Toast.LENGTH_SHORT).show()
            })
            .addAction("Hide", R.drawable.bubble_hide, {
                Toast.makeText(textView.context, "Hide pressed!", Toast.LENGTH_SHORT).show()
            })
            .show()
    true
}
```

####Using a menu resource
You can also use a menu resource to build BubbleActions. Here's the same example using a menu resource:
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:id="@+id/action_star"
        android:icon="@drawable/bubble_star"
        android:title="Star" />

    <item android:id="@+id/action_share"
        android:icon="@drawable/bubble_share"
        android:title="Share" />

    <item android:id="@+id/action_hide"
        android:icon="@drawable/bubble_hide"
        android:title="Hide" />

</menu>
```

Note that each menu item must have an id, icon, and a title. Submenus are not supported.
```java
findViewById(R.id.text_view).setOnLongClickListener(new View.OnLongClickListener() {
            @Override
            public boolean onLongClick(final View v) {
                BubbleActions.on(v)
                        .fromMenu(R.menu.menu_actions, new MenuCallback() {
                            @Override
                            public void doAction(int itemId) {
                                switch (itemId) {
                                    case R.id.action_star:
                                        Toast.makeText(v.getContext(), "Star pressed!", Toast.LENGTH_SHORT).show();
                                        break;
                                    case R.id.action_share:
                                        Toast.makeText(v.getContext(), "Share pressed!", Toast.LENGTH_SHORT).show();
                                        break;
                                    case R.id.action_hide:
                                        Toast.makeText(v.getContext(), "Hide pressed!", Toast.LENGTH_SHORT).show();
                                        break;
                                }
                            }
                        })
                        .show();
                return true;
            }
        });
```

####Changing the font
Use a custom font? Have no fear! You can configure the typeface of the bubble actions by using `withTypeface` when
you build your `BubbleActions`:
```
BubbleActions.on(myView)
    .withTypeface(/* your fancy typeface */)
    // ... add actions ...
```

####Changing the indicator
The default indicator is a semi-transparent circle that appears where the last down touch event occurred before
showing the `BubbleActions`. You can change this indicator by using the `withIndicator` method 
when you build your `BubbleActions`:
```
BubbleActions.on(myView).withIndicator(R.drawable.my_fancy_indicator)
    // ... add actions ...
```

####Setting animation duration and interpolator
You can also customize the animation speed and the animation interpolator 
of the bubbles by using `withDuration` and `withInterpolator`:
```
BubbleActions.on(myView)
    .withDuration(/* your custom duration */)
    .withInterpolator(/* your fancy interpolator */)
    // ... add actions ...
```

##License
```
Copyright 2015 Sam Thompson

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
dependencies {
	        implementation 'com.github.target1314:BubbleActions:1.3.0'
	}
