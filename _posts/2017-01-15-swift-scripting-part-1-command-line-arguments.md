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


---
Why `CommandLine` enum is defined as an enum, not a struct?
