# Logos In More Depth

As you would of learnt `logos` is the syntax we will use to make our lives a lot easier

However there is way more we can do with it

A full list of `logos` directives can be found [HERE](https://iphonedevwiki.net/index.php/Logos)

# %group

```objective-c
%group Groupname
```

`%group` can be used to execute code under certain conditions lets say depending on your iOS version

```objective-c
%group iOS13
%hook IOS8_SPECIFIC_CLASS
	// your code here
%end // end hook
%end // end group ios13

%group iOS12
%hook IOS12_SPECIFIC_CLASS
	// your code here
%end // end hook
%end // end group ios12
```

and too call upon the group we use `%init(groupName);`

in our example it would be `%init(iOS13);` or `%init(iOS12);`

> Groups can not be placed inside other groups

# %ctor

```objective-c
%ctor {
  // code here
}
```

This creates a anonymous constructor that we can run our code in

An anonymous constructor is an anonymous class such as it would be in `java`
