# Creating Our First Tweak

So we have `Theos` set up, and we understand the basics of `logos`

Now lets put that into practice and start our first tweak

# Creating The Base Files

So in our terminal, we need to go to the folder we want our tweak project files to be in

```bash
$THEOS/bin/nic.pl
```

Now it will give us a series of number and we want to press the one that says tweak next to it
(This changes every so often with new releases of `Theos` so just press the one that says tweak)

```bash
NIC 2.0 - New Instance Creator
------------------------------
  [1.] iphone/activator_event
  [2.] iphone/application_modern
  [3.] iphone/application_swift
  [4.] iphone/flipswitch_switch
  [5.] iphone/framework
  [6.] iphone/library
  [7.] iphone/preference_bundle_modern
  [8.] iphone/tool
  [9.] iphone/tool_swift
  [10.] iphone/tweak
  [11.] iphone/xpc_service
Choose a Template (required):
```

Now it is going to ask us for a project name

```bash
Project Name (required): ExampleTweak
```

Now it is going to ask us for a packageID (`BundleID`)
BundleID's are what iOS uses to separate and label tweaks and apps

It is common practice to put your Domain Name backwards then your tweak name

```bash
tech.kodeycodesstuff.exampletweak
```
However it does not matter whatever it is as long as it is `UNIQUE`

```bash
Package Name [com.yourcompany.exampletweak]: com.kodeycodesstuff.exampletweak
```

Then it will ask for `Author` just type in your name, it really doesn't
matter what you put there.

It will now ask you for a `MobileSubstrate BundleID` we do not need to worry
about this as our tweak will be hooking into the `SpringBoard` as most tweaks do

Now if you want your tweak to target a different application this is where you'd
put the bundleID of that app

```bash
For Example: com.apple.music
```

We do not need to worry about this, so leave it blank and press enter.

The next screen talks about apps to terminate when installed, we again don't
need to worry about this so leave it blank and press enter.

If you want to terminate an application this would be the space to do it
```bash
For Example: com.spotify.client
```  

Now, our tweak files are made. If we cd into our new directory we can see all
the new files that have been made

```bash
cd exampletweak
```

We are going to use ls to display all the files in that directory
```bash
ls
```

And here we can see the files that have been created
```bash
ExampleTweak.plist Makefile           Tweak.x            control
```

Next i'll explain what each of these files does and how we can use them
