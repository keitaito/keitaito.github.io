---
layout: post
title:  "Exploring Compiler Options"
date:   2017-01-02
categories: blog
---

I have been re-learning C language recently with [Learn C the Hard Way](https://learncodethehardway.org/c/).
Today, I was working with a Makefile. It has `CFLGS` options code like this:
```Makefile
CFLAGS=-g -O2 -Wall -Wextra -Isrc -rdynamic -DNDEBUG $(OPTFLAGS)
```
When I ran `make`, I got an error:
```sh
clang: warning: argument unused during compilation: '-rdynamic'
```
It is a pretty trivial warning, but I decided to dig in the warning to solve it.

---

### What is `-rdynamic` option?

First, I googled the `-rdynamic` option, which is the cause of the warning.
[According to GNU GCC's online docs](https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html),

`-rdynamic`
> Pass the flag -export-dynamic to the ELF linker, on targets that support it. This instructs the linker to add all symbols, not only used ones, to the dynamic symbol table. This option is needed for some uses of dlopen or to allow obtaining backtraces from within a program.

So, it seems the `-rdynamic` options is one for linker. Ok, next, what is `-export-dynamic` option then?

### What is `-export-dynamic` option?
[According to GNU's manuals](ftp://ftp.gnu.org/old-gnu/Manuals/ld-2.9.1/html_node/ld_3.html),

`--export-dynamic`
> When creating a dynamically linked executable, add all symbols to the dynamic symbol table. The dynamic symbol table is the set of symbols which are visible from dynamic objects at run time. If you do not use this option, the dynamic symbol table will normally contain only those symbols which are referenced by some dynamic object mentioned in the link. If you use dlopen to load a dynamic object which needs to refer back to the symbols defined by the program, rather than some other dynamic object, then you will probably need to use this option when linking the program itself.

Ok, I'd say this option can be used when I use `dlopen` function.

---

### Why the warning is thrown?

Probably, my guess is on my machine, which is macOS Sierra Version 10.12.2, the used compiler is LLVM. I found a question related to this warning on stackoverflow:

[What is clang's equivalent to -rdynamic gcc flag?](http://stackoverflow.com/questions/21279036/what-is-clangs-equivalent-to-rdynamic-gcc-flag)

So, the solution is `-Wl,-export_dynamic`. However, after fixing this, another warning is thrown.
```sh
clang: warning: -Wl,-export_dynamic: 'linker' input unused
```
(BTW, [Any difference between “-Wl,option” and “-Xlinker option” syntax for gcc](http://stackoverflow.com/questions/7221141/any-difference-between-wl-option-and-xlinker-option-syntax-for-gcc))

To fix the warning, I found this question: [how to suppress “linker file unused” when compiling](http://stackoverflow.com/questions/9728564/how-to-suppress-linker-file-unused-when-compiling). So, the solution is not to pass linker options here. `¯\_(ツ)_/¯`


### Conclusion

There're soooooo many LLVM/Clang compiler options.

---

##### Note to myself
The following are what I should check more. I will do them sometime later.
- What is ELF Linker?
- What is dynamic symbol table?
- What is symbol?
- Why does an option sometimes have single dash and double dashes?
