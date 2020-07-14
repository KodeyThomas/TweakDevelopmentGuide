# Hooks In Practice

So, we are ready to start making our tweak.

Sure we know what `hooks` are and how to properly syntax them but now its time
too use them in practise

Lets load up `Tweak.x` in our IDE of choice and remove the existing code
in there as we wont need any of it.

As you will remember a `hook` looks like this

```objective-c
%hook randomClass
-(void)aRandomMethod {
  %orig;
  // our modified code here
}
%end
```
> The `%orig` doesn't always need to come after the method but in this guide for simplicity we shall use it 

We now need to find a `class` to `hook` into and modify one of the `methods`

We can do this using [Limneos's Headers](https://developer.limneos.net/?ios=13.1.3)
This link will become very important as it is essentially our Wikipedia we can
refer too at any time.

Our `classes` are stored in `header` files, each one of apples frameworks have
several `header` files, because there are thousands of `classes` we use this
site to sort through them.

> One of the trickiest parts about Tweak Development is finding the right
header and the right classes to accomplish the specific task

In this Example Tweak we will be creating a Tweak that provides haptic feedback
to the user, so lets go and try and find the right `header` that will contain a
`class` that we can use to create our tweak.

Lets break it down a bit, into a small chart so we can understand what we want
our tweak to do.

I shall write our `tweak breakdown` in `pseudocode` this basically means it is
not real code but is easy to translate.

```pseudocode
if(VolumeButtonIsPressed) {
  PlayHapticFeedback
}
```

Now lets convert that `pseudocode` into something that looks more like obj-c

```pseudocode
#import <ourHeaderThatControlsVolume.h>
%hook classThatControlsVolumeFromOurHeader
-(void)ourMethodThatHappensWhenVolumeButtonIsPressed {
  %orig;
  PlayHapticFeedback;
}
```

> Please not the above code DOES NOT WORK it is just a simple breakdown so you
understand a little better

# Finding The Right Header

When we get onto [Limneos's Headers](https://developer.limneos.net/?ios=13.1.3)
We will see a few things, on the main homepage we will see a massive list of
frameworks. We will want to click on `SpringBoard` as that is the framework we
will be using during this example.

Now we are in the `SpringBoard` folder, this contains all the `header` files for
the `SpringBoard`.

We are going to want to search the list that is in front of us for `Volume`

```UTF-8
SBVolumeControl.h   
SBVolumeControlState.h   
SBVolumeHUDDomain.h   
SBVolumeHUDSettings.h   
SBVolumeHUDViewController.h   
SBVolumeHUDViewControllerDelegate.h   
SBVolumeHardwareButton.h   
SBVolumeHardwareButtonActions.h   
SBVolumePressBandit.h
```

> Note they are all stored in Alphabetical Order

Your next question is, well how do you what is the right one. Luckily of us
Apple names all of there `headers` in accordance to what they do.

> Note most headers relating to the SpringBoard usually start with 'SB'

So using common sense, we want to find a `header` that contains the methods for
Volume Control.

Our best guess it is `SBVolumeControl.h`

We have now found our `header` so we can now learn a bit more about `headers`
