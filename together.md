# Putting It All Together

So now we have a `hook`, a `class`, and a `method`

So lets put what we have so far in `Tweak.x`

```objective-c
%hook SBVolumeControl

-(void)increaseVolume {
	%orig;
}

-(void)decreaseVolume {
	%orig;
}

%end
```

Before we do anything else we need to import the `header` as otherwise `theos` will have no clue what we are on about
we do this by the following code, because it is in the `SpringBoard` its automatically loaded so we don't have to worry
about it.

So right now we have code which essentially does nothing so lets modify it too do something

We wanted to add functionality to play haptic feedback.

Now we can use [Apple's Offical Documentation](https://developer.apple.com/documentation) to execute our modified code, as it is only obj-c

So lets search the website on how to play Haptic Feedback,

Now because we are doing `obj-c` programming just like any other language there are multiple methods on how to do this.

We are going to use the simplest one I know which is through the `AudioToolbox` framework.

> Any method you find on an Apple website in 'obj-c' will work as we are no longer worrying about tweak specifics but more about 'obj-c'

So lets add `AudioToolbox` to our frameworks in `makefile`

```makefile
$(TWEAK_NAME)_FRAMEWORKS = AudioToolbox
```

Because it is an additional framework we also need to link too the header file in the tweak

```objective-c
#import <AudioToolbox/AudioToolbox.h>
```

> This method of adding frameworks works for any public framework these can be found on the [Apple Development Website](https://developer.apple.com/documentation)

> If you want to add Private Frameworks such as `BluetoothManager.framework` a tutorial can be found [Here](privateframeworks.md)

In `obj-c` you can play system sounds by this line of code:

```objective-c
AudioServicesPlaySystemSound(SystemSoundID);
```

> Note, this can be found on Apples official documentation for AudioToolbox

For some reason you can play haptics with specific `SystemSoundID's` here is the list:
> To find the full list of SystemSounds click - [HERE](https://github.com/TUNER88/iOSSystemSoundsLibrary)

```objective-c
AudioServicesPlaySystemSound(1519); // light feedback
AudioServicesPlaySystemSound(1520); // medium feedback
AudioServicesPlaySystemSound(1521); // high feedback
```

Lets add this too our `code`

```objective-c
#import <AudioToolbox/AudioToolbox.h>

%hook SBVolumeControl

-(void)increaseVolume {
  %orig;
  AudioServicesPlaySystemSound(1521);
}

-(void)decreaseVolume {
  %orig;
  AudioServicesPlaySystemSound(1521);
}
%end
```

Done, our simple tweak is done

Lets compile it
