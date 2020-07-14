# Logos Syntax

The syntax of Logos makes creating tweaks way easier. Logos helps us 'hook' into methods and allow us to run our own code on top of apples original code.

# How to Use Logos

Every hook in Logos needs to consist of four things

- `%hook`
- `A Method`
- `%orig`
- `%end`

You can compare the syntax of `logos` to `html`, they both need to be closed when you open a tag

```html
<body>
  Your Code here
</body>
```

Ok, so what does that actually look like

```objective-c
%hook RandomClass
-(void)aRandomMethod {
  %orig;
  // our added code here
}
%end
```
This may look complicated but I assure you it isn't. `logos` syntax is incredibly easy to learn

# Logos Specific Identifiers

In `logos` there are a few specific identifiers so its important to learn them all, for the sake of the Guide
I am only going to include the basic ones the rest are available here - [LINK](https://iphonedevwiki.net/index.php/Logos)


`%hook` - This hooks into a class and allows us to modify the code that runs

```objective-c
%hook RandomClass
```

`%end` - Just like in `<HTML>` we need to tell the complier we are finished with the hook

```objective-c
%hook RandomClass
%end
```

Now we need to add a method or a variable, I will talk more about them later in the guide
All you need to know right now is it is something from the original code that we can hook into and edit

```objective-c
%hook RandomClass
-(void)aRandomMethod {

}
```

`%orig` - This tells the complier to execute the original code

```objective-c
%hook RandomClass
-(void)aRandomMethod {
  %orig;
}
```

Now all we need to do is add our modified code

```objective-c
%hook RandomClass
-(void)aRandomMethod {
  %orig;
  // Here is where our code we want to run will be
}
```

That is `logos` syntax summed up
