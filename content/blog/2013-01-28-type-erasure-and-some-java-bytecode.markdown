---
author: alexchiri
date: 2013-01-28 05:00:00+00:00
draft: false
title: Type erasure and some Java bytecode
type: post
url: /2013/01/28/type-erasure-and-some-java-bytecode/
categories:
- Code & Tech
tags:
- java
- type-erasure
---

If you've worked with Java for a while, I'm sure you've heard about one of the things that Java does at compile time: type erasure. But you don't have to trust everybody by their word, you can check it by yourself!

As you know, when you "compile" your class, the .java file is transformed into a .class file, which is a binary file containing JVM operation codes (each operation is represented by a byte = bytecode). This .class file is interpreted by the JVM and later compiled into machine code at runtime by the Just In Time compiler.

A good way to see how Java treats internally all this ["syntactic sugar"](http://en.wikipedia.org/wiki/Syntactic_sugar) is to have a look at the bytecode. Fortunately, Java provides a tool for this, so you don't have to crack your skull with a HEX viewer: the _javap_ tool the JDK comes with.


### A simple class


Let's take the following simple class as our lab rat (no animals were hurt in this experiment):



And compile it (I use JDK 1.7.0_03) to get ASimpleClass.class file.


### javap magic


We're gonna use the javap tool to get two things: one, the constant pool and second, the class disassembled. I will not start explaining most of the things found in the following output because this would end up in huge article (yes, they can get even bigger). You can find out more by yourself by visiting the [opcode reference](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-6.html) from Oracle.

So, go on and run `javap -v ASimpleClass.class` and don't freak out when you see something like the output from this link: [ASimpleClass.class](https://gist.github.com/4648077)

The constant pool contains elements which are constant inside the class. The disassembled class opcode contains references to the constant pool for almost every operation. But you don't have to rush and see what the reference is, because javap puts it as a comment on the right side of the operation call.


### Java disassembled code


Let's focus a bit on the main method disassembled:



The first 3 lines are encountered each time we create a new instance of a class:

    
    <code>0: new           #2                  // class java/util/ArrayList
    3: dup           
    4: invokespecial #3                  // Method java/util/ArrayList."<init>":()V
    </code>


[new](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-6.html#jvms-6.5.new) allocates memory for the new instance, initializes instance variables and pushes the new reference in the operand stack, [dup](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-6.html#jvms-6.5.dup) duplicates the top value on the operand stack and pushes the duplicate onto the operand stack and finally [invokespecial](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-6.html#jvms-6.5.invokespecial) calls the method referenced at line #3 in the constant pool, in our case the _ArrayList_ constructor.

I guess you started to get the hang of it, you might not understand everything but the gist should be there.


### Type erasure


You might have noticed already that the _ArrayList_ reference doesn't have any generic and its _add_ method receives an _Object_ and not a String, as you can notice in the constant pool _NameAndType_ entry at line #48:

    
    <code>#48 = NameAndType        #67:#68        //  add:(Ljava/lang/Object;)Z
    </code>


But this doesn't mean that when the _Object_ instances are pulled out by the iterator, the JVM doesn't check its type to be _String_:

    
    <code>43: invokeinterface #9,  1            // InterfaceMethod java/util/Iterator.next:()Ljava/lang/Object;
    48: checkcast     #10                 // class java/lang/String
    </code>


invokeinterface calls the next() method and puts the result in the operand stack, which is checked afterwards by [checkcast](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-6.html#jvms-6.5.checkcast) to be a _String_.


### Other notes


It would be interesting to have a look at how the _for_ statement was treated (starting #27) and how the concatenation of the two _String_s ("Type" and "erasure") was made (#55:#71), but I don't want to spoil your geek fun and leave you to it!
