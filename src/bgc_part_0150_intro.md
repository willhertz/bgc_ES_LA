<!-- Beej's guide to C

# vim: ts=4:sw=4:nosi:et:tw=72
-->

# Hello, World!

## What to Expect from C

> _"Where do these stairs go?"_<br>
> _"They go up."_
>
> ---Ray Stantz and Peter Venkman, Ghostbusters

C is a low-level language.

It didn't used to be. Back in the day when people carved punch cards out
of granite, C was an incredible way to be free of the drudgery of
lower-level languages like [flw[assembly|Assembly_language]].

But now in these modern times, current-generation languages offer all
kinds of features that didn't exist in 1972 when C was invented. This
means C is a pretty basic language with not a lot of features. It can do
_anything_, but it can make you work for it.

So why would we even use it today?

* As a learning tool: not only is C a venerable piece of computing
  history, but it is connected to the [flw[bare metal|Bare_machine]] in
  a way that present-day languages are not. When you learn C, you learn
  about how software interfaces with computer memory at a low level.
  There are no seatbelts. You'll write software that crashes, I assure
  you. And that's all part of the fun!

* As a useful tool: C still is used for certain applications, such as
  building [flw[operating systems|Operating_system]] or in [flw[embedded
  systems|Embedded_system]]. (Though the
  [flw[Rust|Rust_(programming_language)]] programming language is eyeing
  both these fields!)

If you're familiar with another language, a lot of things about C are
easy. C inspired many other languages, and you'll see bits of it in Go,
Rust, Swift, Python, JavaScript, Java, and all kinds of other languages.
Those parts will be familiar.

The one thing about C that hangs people up is _pointers_. Virtually
everything else is familiar, but pointers are the weird one. The concept
behind pointers is likely one you already know, but C forces you to be
explicit about it, using operators you've likely never seen before.

It's especially insidious because once you [flw[_grok_|Grok]] pointers,
they're suddenly easy. But up until that moment, they're slippery eels.

Everything else in C is just memorizing another way (or sometimes the
same way!) of doing something you've done already. Pointers are the
weird bit.

So get ready for a rollicking adventure as close to the core of the
computer as you can get without assembly, in the most influential
computer language of all time^[I know someone will fight me on that,
but it's gotta be at least in the top three, right?]. Hang on!


## Hello, World!

This is the canonical example of a C program. Everyone uses it. (Note
that the numbers to the left are for reader reference only, and are not
part of the source code.)

``` {.c .numberLines}
/* Hello world program */

#include <stdio.h>

int main(void)
{
    printf("Hello, World!\n");  // Actually do the work here

    return 0;
}
```

We're going to don our long-sleeved heavy-duty rubber gloves, grab a
scalpel, and rip into this thing to see what makes it tick. So, scrub
up, because here we go. Cutting very gently...

Let's get the easy thing out of the way: anything between the digraphs
`/*` and `*/` is a comment and will be completely ignored by the
compiler. Same goes for anything on a line after a `//`. This allows you
to leave messages to yourself and others, so that when you come back and
read your code in the distant future, you'll know what the heck it was
you were trying to do. Believe me, you will forget; it happens.

Now, what is this `#include`? GROSS! Well, it tells the C Preprocessor
to pull the contents of another file and insert it into the code right
_there_.

Wait---what's a C Preprocessor? Good question. There are two stages
(well, technically there are more than two, but hey, let's pretend there
are two and have a good laugh) to compilation: the preprocessor and the
compiler. Anything that starts with pound sign, or "octothorpe", (`#`)
is something the preprocessor operates on before the compiler even gets
started. Common _preprocessor directives_, as they're called, are
`#include` and `#define`. More on that later.

Before we go on, why would I even begin to bother pointing out that a
pound sign is called an octothorpe? The answer is simple: I think the
word octothorpe is so excellently funny, I have to gratuitously spread
its name around whenever I get the opportunity. Octothorpe. Octothorpe,
octothorpe, octothorpe.

So _anyway_. After the C preprocessor has finished preprocessing
everything, the results are ready for the compiler to take them and
produce [flw[assembly code|Assembly_language]], [flw[machine
code|Machine_code]], or whatever it's about to do. Don't worry about the
technical details of compilation for now; just know that your source
runs through the preprocessor, then the output of that runs through the
compiler, then that produces an executable for you to run. Octothorpe.

What about the rest of the line? What's `<stdio.h>`? That is what is
known as a _header file_. It's the dot-h at the end that gives it away.
In fact it's the "Standard I/O" (stdio) header file that you will grow
to know and love. It contains preprocessor directives and function
prototypes (more on that later) for common input and output needs. For
our demo program, we're outputting the string "Hello, World!", so we in
particular need the function prototype for the `printf()` function from
this header file. Basically, if we tried to use `printf()` without
`#include <stdio.h>`, the compiler would have complained to us about it.

How did I know I needed to `#include <stdio.h>` for `printf()`? Answer:
it's in the documentation. If you're on a Unix system, `man printf` and
it'll tell you right at the top of the man page what header files are
required. Or see the reference section in this book. `:-)`

Holy moly. That was all to cover the first line! But, let's face it, it
has been completely dissected. No mystery shall remain!

So take a breather...look back over the sample code. Only a couple easy
lines to go.

Welcome back from your break! I know you didn't really take a break; I
was just humoring you.

The next line is `main()`. This is the definition of the function
`main()`; everything between the squirrelly braces (`{` and `}`) is part
of the function definition.

How do you call a different function, anyway? The answer lies in the
`printf()` line, but we'll get to that in a minute.

Now, the main function is a special one in many ways, but one way stands
above the rest: it is the function that will be called automatically
when your program starts executing. Nothing of yours gets called before
`main()`. In the case of our example, this works fine since all we want
to do is print a line and exit.

Oh, that's another thing: once the program executes past the end of
`main()`, down there at the closing squirrelly brace, the program will
exit, and you'll be back at your command prompt.

So now we know that that program has brought in a header file,
`stdio.h`, and declared a `main()` function that will execute when the
program is started. What are the goodies in `main()`?

I am so happy you asked. Really! We only have the one goodie: a call to
the function `printf()`. You can tell this is a function call and not a
function definition in a number of ways, but one indicator is the lack
of squirrelly braces after it. And you end the function call with a
semicolon so the compiler knows it's the end of the expression. You'll
be putting semicolons after most everything, as you'll see.

You're passing one parameter to the function `printf()`: a string to be
printed when you call it. Oh, yeah---we're calling a function! We rock!
Wait, wait---don't get cocky. What's that crazy `\n` at the end of the
string? Well, most characters in the string look just like they are
stored. But there are certain characters that you can't print on screen
well that are embedded as two-character backslash codes. One of the most
popular is `\n` (read "backslash-N") that corresponds to the _newline_
character. This is the character that causing further printing to
continue on the next line instead of the current. It's like hitting
return at the end of the line.

So copy that code into a file called `hello.c` and build it. On a
Unix-like platform (e.g. Linux, BSD, Mac, or WSL), you'll build with a
command like so:

```
gcc -o hello hello.c
```

(This means "compile `hello.c`, and output an executable called
`hello`".)

After that's done, you should have a file called `hello` that you can
run with this command:

```
./hello
```

(The leading `./` tells the shell to "run from the current directory".)

And see what happens:

```
Hello, World! 
```

It's done and tested! Ship it!

## Compilation

Let's talk a bit more about how to build C programs, and what happens
behind the scenes there.

Like other languages, C has _source code_. But, depending on what
language you're coming from, you might never have had to _compile_ your
source code into an _executable_.

Compilation is the process of taking your C source code and turning it
into a program that your operating system can execute.

JavaScript and Python devs aren't used to a separate compilation step at
all--though behind the scenes it's happening! Python compiles your
source code into something called _bytecode_ that the Python virtual
machine can execute. Java devs are used to compilation, but that
produces bytecode for the Java Virtual Machine.

When compiling C, _machine code_ is generated. This is the 1s and 0s
that can be executed directly by the CPU.

> Languages that typically aren't compiled are called _interpreted_
> languages. But as we mentioned with Java and Python, they also have a
> compilation step. And there's no rule saying that C can't be
> interpreted. (There are C interpreters out there!) In short, it's a
> bunch of gray areas. Compilation in general is just taking source code
> and turning it into another, more easily-executed form.

The C compiler is the program that does the compilation.

As we've already said, `gcc` is a compiler that's installed on a lot of
[flw[Unix-like operating systems|Unix]]. And it's commonly run from the
command line in a terminal, but not always. You can run it from your
IDE, as well.

But we'll do some command line examples here because there are too many
IDEs to cover. Search the Internet for your IDE and "how to compile C"
for more information.

So how do we do command line builds?

## Building with `gcc`

If you have a source file called `hello.c` in the current directory, you
can build that into a program called `hello` with this command typed in
a terminal:

```
gcc -o hello hello.c
```

The `-o` means "output to this file"^[If you don't give it an output
filename, it will export to a file called `a.out` by default---this
filename has its roots deep in Unix history.]. And there's `hello.c` at
the end, the name of the file we want to compile.

If your source is broken up into multiple files, you can compile them
all together (almost as if they were one file, but the rules are
actually more complex than that) by putting all the `.c` files on the
command line:

```
gcc -o awesomegame ui.c characters.c npc.c items.c
```

and they'll all get built together into a big executable.

That's enough to get started---later we'll talk details about multiple
source files, object files, and all kinds of fun stuff.