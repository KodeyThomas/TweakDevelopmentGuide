# Default Files in theos

So now we have 4 new files we can edit and I will do my best to explain every
one of them, so you have a complete understanding

> Any calls that *explicitly* state the tweak name we will either refer to in
> this guide by either

> TWEAK_NAME ,
> ExampleTweak


```bash
ExampleTweak.plist    Makefile    Tweak.x    control
```

# TWEAK_NAME.plist

This file, we wont need to edit as it simply contains the different bundleID's
incase you were targeting a different bundleID for your tweak

```PLIST
{ Filter = { Bundles = ( "com.apple.springboard" ); }; }
```

# Makefile

```makefile
INSTALL_TARGET_PROCESSES = SpringBoard

include $(THEOS)/makefiles/common.mk

TWEAK_NAME = ExampleTweak

ExampleTweak_FILES = Tweak.x
ExampleTweak_CFLAGS = -fobjc-arc

include $(THEOS_MAKE_PATH)/tweak.mk
```

> Additionally, please know that ExampleTweak_FILES can be replaced with $(TWEAK_NAME)_FILES
> If you see $(TWEAK_NAME) referenced this can be interchanged with our actual tweak name


Editors Note: You CAN use $(TWEAK_NAME) but it can cause some conflicts and its not recommended
the reason i chose to include it so people could 'copy paste' from the guide

It is HIGHLY recommended to use for example `ExampleTweak_FILES` instead, but i can't stop you
just be aware if you are getting issues with `$(TWEAK_NAME)` then use the traditional way


This File is crucial to setting your tweak to deploy properly

> When editing $(TWEAK_NAME) in this case the make file states it is
ExampleTweak. This is reflected in the name of the PLIST file so please rename
accordingly

There are several things we can add to this file to start off with, mainly

```makefile
ARCHS = arm64 arm64e
```

These are the two architectures we will compile our tweak for. At the time of
writing they are the current architectures used on iOS13

`arm64` - This is pre A12 devices. Anything released before 2018
`arm64e` - This is A12/A13 devices and is the current architecture

Luckily we don't have to do anything to compile for both of them as `theos` does
this for us

```makefile
THEOS_DEVICE_IP = YOUR_IPHONE_IP
```

Now if we add this too our `makefile` it makes it a hell of a load easier to
test our tweaks as it installs it too our device for us

Things to Note

- [SSH must be set up on your iPhone](https://www.iphonefaq.org/archives/971438)
- [It is advisable to set up SSH Keys so you don't have to type your password every-time](http://azizuysal.com/setting-up-ssh-public-key-authentication-for-iphone-remote-access/)
- If setting up SSH Keys don't include a key, as otherwise you would have to
type that key every time you tried to SSH into your phone
- [You Can SSH Over USB](https://iphonedevwiki.net/index.php/SSH_Over_USB) - This is a tutorial to set it up


If we want to add additional frameworks either Public or Private we need to add
them to our `makefile`

```makefile
$(TWEAK_NAME)_FRAMEWORKS =
$(TWEAK_NAME)_PRIVATE_FRAMEWORKS =
```

> Please be aware you can copy those two directly into the makefile as
$(TWEAK_NAME) is a bash variable

When we have finish with our tweak and want to package it for launch we can add this to our `makefile`

```makefile
FINAL_PACKAGE = 1
```

This will remove the build number from our tweak and just leave us with our version nummber

And that is it for our `makefile`

# control

```UTF-8
Package: com.kodeycodesstuff.exampletweak
Name: ExampleTweak
Depends: mobilesubstrate
Version: 0.0.1
Architecture: iphoneos-arm
Description: An awesome MobileSubstrate tweak!
Maintainer: Kodey Thomas
Author: Kodey Thomas
Section: Tweaks
```

Everything in `control` can be edited to our liking but the main things you will
want to edit are;

`Name` - Display name of the tweak in cydia

`Description` - The Description of the tweak as it appears in cydia

`Package` - BundleID of our tweak

`Version` - Version of our tweak its best to use [Semantic Versioning](https://semver.org)
as this will make it easier to understand when you update your tweak

# tweak.x

Now this is the bit we came here for, `tweak.x` will actually hold all of our
tweak code. You can add additional files of tweak code but we wont need too.

If you wanted to do this you would go into the `makefile` and edit

```makefile
ExampleTweak_FILES = Tweak.x anotherFile.x
```

Cool, so we now know exactly what every file does and we have our `makefile` all
configured.
