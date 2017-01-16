---
layout: post
title:  "Swift Scripting Part 1: Command Line Arguments and Using Foundation"
date:   2017-01-15
categories: blog
---

You can use Swift as scripting language as well as compiled language. For example:

{% gist 808825984d066690e4ec68f4b1d74f66 %}

To run this file, execute the command `swift <file-name>` in Terminal (you need to be in the same directory where the swift file that you want to run exists).

```bash
$ swift HelloWorld.swift
Hello, world!
```

When you use a command line program, you often pass in arguments to the program. You can pass in arguments to a Swift program too. But, the program-side, how can you use the passed arguments? The answer is to use [`CommandLine` enum](https://developer.apple.com/reference/swift/commandline).

{% gist 067a8f3452b6247f97915b5eb80dce0a %}

`CommandLine` enum is a simple small enum that has only type properties. You can access to arguments with them.

- `argc` is a type property that returns the count of the passed arguments. The first argument is always the name of the program, that is the file name here, that is `argc` always return at least `1`.
- `arguments` is a type property that returns an array of String type that contains arguments as String type.

Let's run `HelloWorld2.swift` file with no argument, and with some arguments.

```bash
$ swift HelloWorld.swift
Hello, world!
No arguments are passed.
HelloWorld.swift

$ swift HelloWorld.swift foo bar baz
Hello, world!
Arguments are passed.
HelloWorld.swift
foo
bar
baz
```

Awesome! Do you want to use Foundation framework with scripting? Of course you can use it. Just add a line `import Foundation` as same as a Xcode project.

{% gist 04fc589b292d00f3a06b4a5b2d1a07bc %}

```bash
$ swift HelloWorld.swift foo bar baz
Hello, world!
Arguments are passed.
HelloWorld.swift
foo
bar
baz
2017-01-16 07:31:41 +0000
```

You can now print out the current date! Let's do something more interesting. How about using [`FileManager` class](https://developer.apple.com/reference/foundation/filemanager) to explore your computer? Let's check your home directory!

- `homeDirectoryForCurrentUser` is an instance property returns the current user's home directory URL.
- `contentsOfDirectory(atPath:)` is an instance method returns an array of String type that contains file names under the passed directory path.

{% gist 151a48bf651b053adbbba468158f2316 %}

- `contentsOfDirectory(atPath:)` is a throwing method. You need to add `try` keyword to call it, and you can use `do-catch` to call `try`.
- You can get a path string from a URL object's `path` instance property.

Cool, you would get the contents in Terminal when you run it.

```bash
$ swift HelloWorld.swift foo bar baz
HelloWorld.swift:26:30: error: 'homeDirectoryForCurrentUser' is only available on OS X 10.12 or newer
let homeDirURL = fileManager.homeDirectoryForCurrentUser
                             ^
HelloWorld.swift:26:30: note: add 'if #available' version check
let homeDirURL = fileManager.homeDirectoryForCurrentUser
                             ^
```

Whaaaaat. When I got the above error when running the Swift file, and you? You too right? After a while debugging, I got why the error is thrown. When you get an error, always read the returned error description, which I didn't 😭

```
error: 'homeDirectoryForCurrentUser' is only available on OS X 10.12 or newer
```

This means that `homeDirectoryForCurrentUser` method is a machine environment dependent method. It is only available on macOS (OS X) 10.12. It means this method is NOT available on Linux environment, for example.

```
note: add 'if #available' version check
```

### Availability condition

A solution is, as the above note says, add an available condition before calling the method. The condition checks the current environment. The method will be invoked since I run this Swift file on my Mac.

{% gist cf1850835b7be57eb81f1447323d2ad7 %}

Let's run the Swift file.

```bash
$ swift HelloWorld.swift foo bar baz
Hello, world!
Arguments are passed.
HelloWorld.swift
foo
bar
baz
2017-01-16 08:13:20 +0000
.atom
.bash_history
.bash_profile
# Many dot files.
.subversion
.Trash
.viminfo
Desktop
dev
Documents
Downloads
Library
Movies
Music
Pictures
Public
```

You are now able to print out the home directory contents here!

### Using -target option

Another solution is using `-target` option with swift command. When you check `swift --help`:

```bash
$ swift --help
  -target <value>        Generate code for the given target
```

With this option, you can tell the Swift (compiler maybe?) which the environment is used. To try this option out, remove or comment out the `if #available` condition check, then run the following command.

```bash
$ swift -target x86_64-macosx10.12 HelloWorld.swift foo bar baz
# You will get the same result above.
```

It works, but it would not be a good idea probably, since it just skipped the availability check, then force the Swift compiler to believe the current environment is the passed one. If it's not true, the program won't be run, I guess.

## Conclusion

- Use `CommandLine` enum to access to arguments.
- Use `import Foundation` to access to awesome Foundation APIs.
- Use `if #available` condition check.
- Use Swift Scripting, because it's super fun!

## Reference

The links to the awesome reference resources.

- [KrakenDev by Hector Matos](https://krakendev.io/blog/scripting-in-swift)
- [Swift Scripting talk video by Ayaka Nonaka at Realm website](https://realm.io/news/swift-scripting/)
- [Command Line Programs on macOS Tutorial by Jean-Pierre Distler at Ray Wenderlich](https://www.raywenderlich.com/128039/command-line-programs-macos-tutorial)

---
<br>
I will check out the following later.

- What is the star mark in `if #available(macOS 10.12, *)`? [The Swift programming guide says:](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html)

> The * argument is required and specifies that on any other platform, the body of the code block guarded by the availability condition executes on the minimum deployment target specified by your target.

- Why is `CommandLine` enum defined as an enum, not a struct?
