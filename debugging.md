# Debugging

Debugging your tweak is incredibly important, here are a few reasons why:

- Testing if the tweak even works. We can use Debugging methods to check if our hooks are working
- Fixing bugs in our code, for example in [SpotifyBlue](https://github.com/KodeyThomas/SpotifyBlue) there was a bug were Spotify would randomly open if connected to a Bluetooth device

Debugging can be used to isolate and fix the problem, as it can give us a good indication of where the bug is

# Debugging Methods

Debugging your tweak can be very simple and there are a plethora of ways to do this
I will cover my personal favourites and how to use them

# Logging

The majority of debugging methods use a thing called `logging`, this allows us to view certain `breakpoints` in our code where we get it too output to the system logs

# RemoteLog

This is a easy method that works cross platform and is easy to install and can be found [HERE](https://github.com/Muirey03/RemoteLog)
Just run the python script after it is set up and the logs should come flying in.

```objective-c
RLog(@"Test log: %@", someObject);
```
> RemoteLog supports all format specifiers of NSLog so if you know the syntax it should migrate easily

# NSLog

NSLog was built by Apple and the documentation can be found [HERE](https://developer.apple.com/documentation/foundation/1395275-nslog)

It can be used to easily check if a `variable` is changing to check if our `hook` and `methods` are working
properly

You can easily read the logs off a device using `console.app` on macOS when your iPhone is plugged in via USB

# AudioServicesPlaySystemSound

This is an alternative method at debugging but i find it works very well.

The simple premise is too play a sound if your code reached a certain point for example if an `if` statement was true

You can then use this to check if your code is running as intended or if it isn't

This is particularly helpful too check if your hook is working but your modified code isn't doing what
we want it too do, this can help us isolate the issue and lead to faster fixes

It is really simple to implement;

Add this to your makefile
```makefile
$(TWEAK_NAME)_FRAMEWORKS = AudioToolbox
```

Add this to whatever you are trying to debug;
```objective-c
AudioServicesPlaySystemSound(SystemSoundID);
```

Replace SystemSoundID with whatever system sound you want to play for example a SMS received is (1003)
A full list of SystemSoundID's can be found [HERE](https://github.com/TUNER88/iOSSystemSoundsLibrary)
