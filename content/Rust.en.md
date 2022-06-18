---
title: "Rust Lang"
pre: ""
post: ""
alwaysopen: true
weight: 40
---
# Rust Language
![](https://upload.wikimedia.org/wikipedia/commons/d/d5/Rust_programming_language_black_logo.svg)
![](https://upload.wikimedia.org/wikipedia/commons/2/20/Rustacean-orig-noshadow.svg)

From Wikipedia;
```
Rust is a multi-paradigm, high-level, general-purpose programming language designed for performance and safety, especially safe concurrency. Rust is syntactically similar to C++, but can guarantee memory safety by using a borrow checker to validate references. Rust achieves memory safety without garbage collection, and reference counting is optional.

Rust was originally designed by Graydon Hoare at Mozilla Research[18], with contributions from Dave Herman, Brendan Eich, and others. The designers refined the language while writing the Servo experimental browser engine, and the Rust compiler. It has gained increasing use in industry, and Microsoft has been experimenting with the language for secure and safety-critical software components.

Rust has been voted the "most loved programming language" in the Stack Overflow Developer Survey every year since 2016, though only used by 7% of the respondents in the 2021 survey.
```

## Note from ShyanJMC
If you do not want (or if you can not) install Rust on your system for many reassons, you can use the official online interpreter;
https://play.rust-lang.org/


## History
From Wikipedia;
```
The language grew out of a personal project begun in 2006 by Mozilla employee Graydon Hoare, who stated that the project was possibly named after the rust family of fungi. Mozilla began sponsoring the project in 2009 and announced it in 2010. The same year, work shifted from the initial compiler (written in OCaml) to the LLVM-based self-hosting compiler written in Rust. Named rustc, it successfully compiled itself in 2011. 

The first numbered pre-alpha release of the Rust compiler occurred in January 2012. Rust 1.0, the first stable release, was released on May 15, 2015. Following 1.0, stable point releases are delivered every six weeks, while features are developed in nightly Rust with daily releases, then tested with beta releases that last six weeks. Every 2 to 3 years, a new Rust "Edition" is produced. This is to provide an easy reference point for changes due to the frequent nature of Rust's Train release schedule, as well as to provide a window to make breaking changes. Editions are largely compatible.

Along with conventional static typing, before version 0.4, Rust also supported typestates. The typestate system modeled assertions before and after program statements, through use of a special check statement. Discrepancies could be discovered at compile time, rather than at runtime, as might be the case with assertions in C or C++ code. The typestate concept was not unique to Rust, as it was first introduced in the language NIL. Typestates were removed because in practice they were little used, though the same functionality can be achieved by leveraging Rust's move semantics.

The object system style changed considerably within versions 0.2, 0.3, and 0.4 of Rust. Version 0.2 introduced classes for the first time, and version 0.3 added several features, including destructors and polymorphism through the use of interfaces. In Rust 0.4, traits were added as a means to provide inheritance; interfaces were unified with traits and removed as a separate feature. Classes were also removed and replaced by a combination of implementations and structured types.

Starting in Rust 0.9 and ending in Rust 0.11, Rust had two built-in pointer types: ~ and @, simplifying the core memory model. It reimplemented those pointer types in the standard library as Box and (the now removed) Gc. 

In January 2014, before the first stable release, Rust 1.0, the editor-in-chief of Dr. Dobb's, Andrew Binstock, commented on Rust's chances of becoming a competitor to C++ and to the other up-and-coming languages D, Go, and Nim (then Nimrod). According to Binstock, while Rust was "widely viewed as a remarkably elegant language", adoption slowed because it repeatedly changed between versions.

Rust has a foreign function interface (FFI) that can be called from, e.g., C language, and can call C. While calling C++ has historically been challenging (from any language), Rust has a library, CXX, to allow calling to or from C++, and "CXX has zero or negligible overhead."

In August 2020, Mozilla laid off 250 of its 1,000 employees worldwide as part of a corporate restructuring caused by the long-term impact of the COVID-19 pandemic. Among those laid off were most of the Rust team, while the Servo team was completely disbanded. The event raised concerns about the future of Rust.

In the following week, the Rust Core Team acknowledged the severe impact of the layoffs and announced that plans for a Rust foundation were underway. The first goal of the foundation would be taking ownership of all trademarks and domain names, and also take financial responsibility for their costs.

On February 8, 2021 the formation of the Rust Foundation was officially announced by its five founding companies (AWS, Huawei, Google, Microsoft, and Mozilla).

On April 6, 2021, Google announced support for Rust within Android Open Source Project as an alternative to C/C++.
```

## Components
- Cargo

Cargo is the package and dependency manager for Rust programms. Allow to download and install dependencies for your rust programs.

To create a new project;
```rust
cargo new [project_name]
```

To build the project;
```rust
cargo build [--release or not]
```

To build and run the project;
```rust
cargo run
```

To check the project;
```rust
cargo check
```

- Rustfmt

Rust Format is the core program that takes rust program as input and then replace spaces and tabulations to formatted code in complience of Rust style guide.

- Clippy

Clippy is the Rust's built-in tool to improve the performance and readability of code. Clippy have more than 400 rules at 2021.

- Rustc

Is the Rust's compiler. You can set arguments by default to rustc setting the variable; RUSTFLAGS . My actual arguments to each execution of rustc are;
```rust
export RUSTFLAGS="-C opt-level=2 -C debuginfo=0 -C lto -C target-cpu=native"
```

- Rustup

Is a toolchain (a set of tools) to install and use rust for differents targets (systems and architectures in which you will execute the program). Also is the best way to install and keep update rust, this is because is agnostic of operative system and do not need administration/root access to install rustc, cargo, etc-

To install rustup

```rust
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

To update rustup and your toolchain

```rust
rustup update
```

To uninstall

```rust
rustup self uninstall
```


## Theory
Rust as many others programming languages have;

- Compiler

Is the component that takes the code and transform it to machine code (binary code, bits (0 and 1) with specific format) with a specific strcuture (is not just read and execute the instructions, must be a specific structure ) and information. With those structures and additional informations, the CPU can work in an specific way and execute properly what developper indicated.

- Pre processor

Are options inside the code which indicate to the compiler some specific things to corroborate/do at compiling time.

- Variable

An variable is something like an "container", this is because can contains one type of information; number, strings or chars. Identify with a name [variable_name], the information stored in memory, so when you want access to that information you can do it using the variable's name as identifier.

The variables in Rust can be created with;
```rust
let [variable_name] = [value];
```

or if you want specift the type;
```rust
let [variable_name]: [type] = [value];
```

In Rust if a variable is intentionally unused in specific conditions, you must prefix it with an underscore; \_[variable]

- Structure

Is a collection of variables under the same structure outside specific function. Is used to group variables with the same purpose.

- Function

Is a piece of code that do an specific thing. Across many languages there are many ways to do it but in C,C++,Rust and others the way to do it is put the code between; { and }. The compiler also must know when a piece of code correspond to an function, so before the name must be the "fn" word.

For example;

```rust
fn [function_name] ( [arguments] ) -> [return_type] {
	[code];
	[code];
	[code];
}
```

The function can return to caller a value, for example; we execute some math operation and the return to caller is the result of it.

The function's part in which you declare the "fn" keyword, and the function name as arguments and return's types is called; signature.

- Method

Sometimes called "objects". Is similitar to functions but a method is used in the context of a struct, enum or trait). The methods have as first argument "self". As functions, the methods takes the function's return and works with it.

- Arguments

An argument is information passed to the program or function to work with it. 

You will see in the future that will be an argument called "&self" it means itself. Which is used when you create a method which is used to take another function's returns. 

- ASCII / UTF

ASCII and UTF are character (numbers, letters and symbols) encoding standard for electronic communication. UTF have 1,7,8,16 and 32 bits variants. Those standards use a combination of bits to represent many symbols as is possible. 

- Instruction

An instruction is an order to execute. Can execute anything thay language supports. 

But the true is this; each instruction that your code execute is really a function (or a macro).

- Comparations

A comparation in Rust can be only done between values of the same type. 

You can only compare variables, or values, of the same type. You can not compare a integer number with a string for example, just int with int, char with char and string with string. Yes, you should convert everything to ASCII table if you need compare but will provide you more challenges.

In Rust if you put in a comparation " _ " means "anything".

- Headers / Libraries

Every programming languge have header/libraries. They are collections of functions (and other informations) in one file that any developper can use in own code. For example; you can just use the standard library and you will not need to develop the information and standar to provide knowledge to rustc what is an int, char, etc.

- Socket

A socket is a special type of thing. Without considering the operative system in which you execute the program.A socket allow a program to communicate with anothers programs transfering information, this type of communication can be in local (Unix domain sockets, in wich the program can communicate with others in the same computer that is running) or trough internet (TCP/IP, UDP and others). Yes, the internet is based in clients and servers which interact trough internet sockets in their operative systems.

- Debug

The debugg is a process in which you take XX program and analyze how works (with the help of specific symbols inside the program) to find and fix issues.
The process allow also to find ways for hacking and cracking it. Always release programs to others without debug symbols.

- File extensions

Rust programs and libs have the ".rs" extension.

- Namespaces and objects

A name is an alias for signs. A sign allow to identify a specific resource to specific object. If many objects have the same functions, calls and/or interfaces, the namespace can allow to track them to specific object.

Ok, a namespace track a thing to a specific object, but what is a object? 
In general and trying to include all paradigms; An object is a piece of thing which have an interface (the way in which interact with others objects). Inside the object there are many pieces of information which can or not depends of the external environment outside the object. That information inside the object can be properties and atributes.

That explenation works for programming, operative systems, data bases, networking, contianers, virtualization, etc. Each of them have specifics application of an object.

- Array

An array is a collection of elements (all with the same type) under the same name, but each element have their own memory position.

- Pointer

A pointer is it. A pointer to something (RAM information, over variables, etc).

- Crate 

In Rust, a create will group related functionality together in a scope so the functionality is easy to share between multiple projects. This is what in another languajes are called "headers" and/or "libraries".

In a Cargo project, the librarie crate is in; "src/lib.rs"

The difference is; In Rust even "main.rs" (the future binary) is a create.

In Rust you can find the central repository for crates in;
https://crates.io/

- Module

As a create is group of functionality, the module is the code group. A module constains one or more functions. 

So a create can group many modules as developers want, and each module have related (in the objetive) functions. But there is a very important thing; a module can have two type of code; a private code (in which only the module or module's function will can use it) or public (in which you can call it from your external code).

- Iterator

"Iterating" is the action of process and work with each element in a series, and an iterator is just the way to do it.

-

## Cargo project's structure

When you create a new project with cargo (the recomended way to use rust projects) with "cargo new [project_name]" there are some things you need to know about;

- You can integrate git with cargo adding argument; -\-vcs=git
- The "Cargo.toml" file is the project's configuration file which constains the project's name, version, edition and the same information for all dependencies.
- In src/ directory (or folder, is the same thing with differents name) you must put your program's files and your headers / libs (crates). By default there is file; main.rs.
- If just exist "main.rs", the crate root will be it. If exist "lib.rs" the crate root file will be it.
- In target/ directory you will find the executable program based in two things;
     - The target (CPU architecture and operative system); is not the same compile for AArch64 using x86 than compile for BSD using Linux, each compilation will have the respective folder. My reccomendation is always compile for your specific CPU if you will not distirbute the binary file.
     - If is a release or debug; just for internal use is reccomended use debug release, for release to public must be used "release" because with it will apply optimizations and the final executable will be smaller.

## Libraries

You will can not do much without the respectives standard libraries. In Rust you can use libraries with; "use".
A library is a compilation of functions, structs and other code. All inside same file, so you can access many functions and features from another files:

```rust
use [library]::[specific_function_or_information];
```

If you do not specify the function or information to import from that library, the whole lib will be imported.

By default, as minimium, you will need:
```rust
use std::io;
```

At this point you know (with the above example) you have an lib called "std" (abrevation of "standard") and you are importing from it a colection of features from "io".

If you

## Variables
As we said before, a variable is a container wich store specific type of information. 

By default, rust compiler interpreter the information that will been assigned to variable and format the variable to that type. If you want specify the type of variable the syntax is this;
```rust
let [variable_name]: [type] ;
```

In Rust by default when a variable is created is inmutable (which means that will not change over time) so if you created the variable but then you need change the value, you have two options;

- Shadow it; this means that you will declarate again the variable wich overwrite the old with a new value.
```rust
let var1 = 5;
[operations];
let var1 = 3;
``` 
- Set as mutable; is not the best solution, but if you know that the variable's value will change over time after "let" specify "mut":
```rust
let mut [variable_name];
```

## Types
Ther are many values types which you can use in your code;
### Numbers
There are two numbers types in Rust; integers (know as numbers without fractional part. ), and numbers with decimals (know as "float").
  - The size of this types (what is the higher value that  can contains) depends of the number of bits to use for store and represent it.
  - The integer numbers are represented as "iX" and float numbers as "fX". The letter "X" is the number of bits to use (8,16,32,64 and 128 bits are available), floats just can use 32 or 64 bits (at 2021 the speed in 64 bits is the same or higher than 32 bits, so use 64 bits).

```rust
let intvar1: i64 = 32000;
let floatvar2: f64 = 32.0001;
```

or if you do not specify the types you can just assign the value.

  - Both (int and float) can be signed (which means that can be positive or negative) or unsigned (which means that can be just positive). Integers and floats signed are reprented as "iX" and "fX" respectly. Unsgined ints are represented as "uX".
  - Integers can be represented as decimals (by default), hexadecimal (0x[XXXXX]), octals (0o[XXX]), binaries (0b[XXXXX]) and as a byte (u8 only) (b'X').


Numbers also have one good feature; tuples. A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a fixed length: once declared, they cannot grow or shrink in size.

```rust
let variable1: (i32,i64,i8) = (128,32000,233);
```

But if you try to impress in screen variable1 you will can not, that is because Rust compiler do not know what value are you referencing. Because of that Rust implements another good feature to assign a variable to each value of tuple:
```rust
let variable1: (i32,i64,i8) = (128,32000,123);
let (x,y,z) = variable1;
```
With above example, we create a tuple with one integer 32 bits type (the number 128), one integer 64 bits type (the number 32000) and one integer 8 bits type (the number 123). Then we create 3 new variables (x,y and z) in which we assign the values in order (x -> 128, y -> 32000 and z -> 123). This process is called; destructuring.

But also tuples have the advantage to index parts, so using dot (".") you can use specifics parts of a tuple. Remember, in langagues (or most of them) the tuples, arrays and lists starts in zero (because is based in the position change number);
```rust
let variable1: (i32,i64,i8) = (128,32000,123);
let x = variable1.0;
```
With abose X variable will have value 128. If the number was 1, X had 32000.

### Symbols
Symbols can be single letters (know as "char") and a strig of characters (know as "string"). Technically and internally Rust calls letters as "grapheme clusters".
  - When is a character, the same must be inside single quotation marks 'X'.
  - When is a string, the same must be inside double quotation marks "XXXX".
  - The strings are represented as "str" in their most primitive way and "String" as the most modern, the difference is a "str" type is inmutable sequence of UTF-8 bytes and "String" is a mutable sequence. Both are dynamic (this means that you can assign directly without considering the input leght ). So you must use "str" when you use an input string which will not change over time and you must use "String" when you need store an input string which will/can change over time. 

Note; instead of many other langs, in Rust you can not index words in a String.

  The differences between "str" and "String" is;
  1. String is growable, can grow over time.
  2. String is mutable, "str" not.
  3. String is owned, see "Ownership" chapter.
  4. String support "UTF-8" encoding, which since 2012 you want it. So, not always a variable's lenght in memory will be equal at words numbers, because of that (about UTF-8 encoding and how store letters and symbols in memory) you can not index words in a string variable. Rust provides different ways of interpreting the raw string data that computers store so that each program can choose the interpretation it needs, no matter what human language the data is in, so be carefull if you store data in a string variable as bytes, scalar values or graphene clusters because you must  read in the same way to read properly the data.

Some of the functions in Strings are;
  1. "String::new()" : Create a new empty string variable.
  2. "String::from(XX)" : Create a new string variable from XX.
  3. ".push_str(XX)" : Append "XX" to an existing string variable.
  4. V1 + V2 : You can append V2 string variable to the V1's string variable end. But "V1" and "V2" will not be longer under score if not used by reference, see "Ownership" chapter. This operator use the "add" method, but use "str" as V2, so be carefull because "str" and "String" are not the same and can cause problems.
  5. "format!("{} {} {} {}", V1,V2,V3,VN) : Is the same that "+". Works equals than "println!" but instead print in stdout, store it in one variable as returns. The return's type is String. One thing about this option not take the ownership.
  6. ".to_string" : Convert a string to string format value.

  - Booleans; true or false.

While tuples can be only intergers, list of array types can be of any types but just one type for all elements.
```rust
let list1 = [1,2,3,4,5,6];
let list2 = ['a','b','c','d','e','f'];
let list3 = ["Hello","World","Rust","rules!"];
```
At the rest, tuples and arrays lists works in the same way.
As the above example; remember, chars go with simples quotation marks and strings with double.

But what about if you have a tuple with 35 equals types? You can specify it with 2 declarations;
```rust
let variable1: [i32; 5] = [1,2,3,4,5];
```
As you can see there are many differences; instead () for type, you specify with [], the number of that type is separeted with ";" and the list go with [] instead of ().
And what about if you have 345 values of the same type? Well, same as before but now with values instead of
```rust
let array5 = [34; 320000];
```
With above example, array5 is a variable with 320000 values. Each values of those 320000 have "34" as value.

Each value inside a variable is indexed in the variable, in the same way as tuples. First value (left to right) have position zero (0), the next have position one (1), etc. But in this case, the access is not with "." (dot), is with "[X]":
```rust
let array6 = ["Hello"," ","World"," ","How"," ","are"," ","you","?"];
let variable7 = array6[0];
```
With the above example, we have a variable called "array6" which have 10 positions (from 0 to 9. Remember, arrays and tuples start from zero). As "variable7" is taked the value of array6's position zero, the value is "Hello", if the array was "1" so the value is " " (space), and if was "9" so the value is "?".

### Pointers
As we said in the Theory section, a pointer is that; a pointer to something. That "something" can be anything that exist; some information into RAM, other variables, etc.

For example;

```rust
fn main() {
    let information = "Hello World".to_string();
let variable1 = &information;
println!("{}",variable1);

}
```

The above code will create a variable called "information" which contains the string "Hello World" passed as it properly by ".to_string()" function. This last allow a string to be printed in screen.

Then the variable "variable1" is a pointer; because is doing reference to "information" RAM memory with the symbol; & 

So "variable1" will be poiting to "information". When the second change, the first too.

In the above code "variable1" poting to "information" is taking as information to "Hello World".

There are many ways to use pointers, but it is the simplest.

### Slice

Is more used in functions' returns, the slice is specified with; “?” and means that you do not know exactly what you will return. Is very usefull when you get some general information (like a String) and you do not know what specifically you will return.

Example;

```rust
fn function1() -> ? {
	[code];
	[return_known]
}
```

### Structs

A struct, or structure is a type which allows you to group variables inside one logical domain. Instead like tuples, in structures you need declarate the variables which will contains the values.

Each variable inside the struct is called field. A structure without files is called unit-like struct

Syntax;

```rust
struct [struct_name] {
	[variable1]: [type],
	[variable2]: [type],
	[variableN]: [type],
}
```

To access to modify or read the values, first you need to create a variable. That variable will have the ownership of that struct, and trough that variable you will access to the structure. When you create that variable, you must not assign a type, as value must be [struct_name] and then you will specify trough { ...} the each component’s value.

But if that variable was declareted before you can use this syntax to read/write (if that variable is mutable, of course); [variable_name].[struct_component]

For example;

```rust
struct User{
    email: String,
    age: u32,
}

fn main() {
    let mut var1_structure = User{
        email: String::from("shyanjm_protonmail.com"),
        age: 0,
    };
    var1_structure.age = 43;
    println!("Struct User from instance var1_structure: {} {}", var1_structure.email, var1_structure.age);
}
```

As you can see, there are a few differences when using structs:

- The values are assigned with : not with equal =.
- When you initialize the struct, you must init all variables, even if you will be provide them the right value before.
- Using the dot . you can access the data without problems if the variable was declarated before (even if are others structs).
- You can not impress directly a struct, this is because Rust will not known how to formatt it.

And if you want return a struct, just put the struct’s name as return type. But you can not pass a struct directly, you must pass the compoents.

If you integrate a struct into a function, and if the argument’s name are exactly the same than the fields you can just put the name and Rust will assign directly the value (this is called; Init shortland). But in my opinion, is just a word, so put the names because is one the best practices you can do; make your code easy to read for others without matter the expertise level.

Another time-saving thing that you can do is assign, with a copy operation, the rest of variables from struct A to struct B. As I said before, in my opinion is best writte more but make the code more easy to read and understand than save a few lines of code, but here the syntax;

```rust
let user2 = User {
	email: String::from("another@example.com"),
	..user1
};
```

That code will create an instance from User struct initing the email field and doing a MOVE operation from the rest user1’s fields so they are not longer available in user1 struct. For this part go to “Ownership” section.

Also as with structs you can create customs types using the primitives (integers, floats, etc) but remember, do not assign the struct as type, the struct assigned as value is the type self. With it as the same way we saw before you can group the types in tuples, the syntax is;

```rust
struct [struct_name]([type],..,..);
```

for example;

```rust
struct Position3d(i64,i64,i64);

let position1 = Position3d(64,32,0);
```

There are some points about struct tuples that you need have in consideration when you work with they;

- A struct tuple can not be passed as argument/parameter to another.
- You can still access to each part of the tuple normally as any tuple with dot . or as array.

## Functions
The first function you will see is "main".
```rust
fn main(){
	[code];
}
```
That function is where your program start. An function will not be execute unless is called inside "main".

If you come from C,C++ and others you know that every function after "main" will produce an error when try to compile and because of that you must use prototypes to fix it. In Rust this is not necesarry, you can put every function you want after "main".

You will see that inside "main" function there is "println!". The "!" indicate that is not a function, is a macro (we will see in the future).

Functions have this syntax;
```rust
fn [function_name]( [arguments] ) -> [Return_type] {
	[code];
	[code];
	...
}
```
With above example;
- [function_name]

     This is the function's name, you use it to know how to call it and where is called.

- [arguments]

     Arguments are the options that you pass to the program.

- [Return_type]

     A function can return to caller a value. This value can be anything recognized as a type in Rust . 


Inside Rust the return is specified into the function's code with word "return" or with just puting a variable or value. So that value will be returned to the variable or function who called it. Instead of the rest of the code, the return goes without the semicolon ";" at the end of line.

From StackOverflow;

> You can omit the return keyword only if the returned value is the last expression in the function block, otherwise you need to explicitly use return

If the argument is specified like this;
```rust
&[String]
```

Means that the argument is a array of strings, you can access directly as an array.

There are a list of common functions and macros.

### println!
Is used to impress in screen. The syntax is;

```rust
println!(" [text] {}", variable_X);
```

The [text] is the string text you want to impress in screen. 

The "{}" indicate to Rust that there must be the "variable_x" value, to in execution time will replace {} with the value of variable_x. You can add many {} and variables as you want.

"Println!" print the message to stdout.

### eprintln!
Works in the same way than "println!" but prints the message to stderr.

### String
This library allocated in standard rust returns an string.

There are many ways to store and use strings into variables.

- To create an empty string into a variable:
```rust
let [variable_name] = String::new();
```

- To store an string into a variable:
```rust
let [variable_name] = "[TEXT]".to_string();
```
or
```rust
let [variable_name] = String::from("[TEXT]");
```
or even
```rust
let [variable_name]: String = "[TEXT]".into();
```

This last line "into" will transform [TEXT] into String, because is the text type.

- To append a string into another string variable:
```rust
[variable_name].push_str([TEXT_OR_STRING_VARIABLE]);
```

or 
```rust
[variable_1] + [variable_2]
```

or
```rust
[variable_to_store] = format!(".... {} {} {} {} ...", var1, var2, var3, varn);
```

- To convert from string to char:
```rust
[string_variable].chars()
```
is a good choice use this with an iteration.

- To iterate over each letter:
```rust
for X in [string_variable].chars() {
    .....
}
```

### .to_lowercase()
This function do what name indicate, transform some String into equivalent to lowercase.

The syntax is;
```rust
[str_or_string_variable].to_lowercase()
```

### .contains(XXXX)
This method/function takes the input and process if have "XXXX". The input can be "str", String, char, or slice of chars.

Returns "True" as '()' if is right or "False" if nothing was found.

The syntax is;
```rust
let strings = "hello world".to_string();
let return1 = assert!(strings.contains("world"));
```

### .lines()
This method/function takes the imput and create an iteration over each line (you can set the newline in a string with "\n"). You can go to the next line with ".next()" and if you go the end of line the return will be "None".

The syntax is;
```rust
let text = "foo\r\nbar\n\nbaz\n";
let mut lines = text.lines();

assert_eq!(Some("foo"), lines.next());
assert_eq!(Some("bar"), lines.next());
assert_eq!(Some(""), lines.next());
assert_eq!(Some("baz"), lines.next());

assert_eq!(None, lines.next());
```

### io::stdin()
As you can see in the name, the function is "stdin" from the lib "io".
This function takes the input and process it inside a struct (in a global buffer), so can be handled properly into a variable.

The syntax is;

```rust
let [mut_or_not] [variable_name] = io::stdin();
```

or if you have a previously mutable variable formatted as a string type:

```rust
let [mut_or_not] [variable2_name] = stdin.read_line(&mut [variable_name])?;
```
We need create a new variable because "stdin" has a return value that must be stored in someplace, unless you use "expect".
Because the imput is stored inside a global buffer, you can force the lock of that buffer so your thread is the only who can access and read/write on it. With this you use a explicit synchorinization;
```rust
let stdin = io::stdin();
let mut [var1_name] = stdin.lock();
[var1_name].read_line(&mut [variable_name])?;
```

### Expect()
This is an special object.
Is used if you want print on screen something when the previous function goes to an error.

```rust
[previous_function_or_variable].expect("[TEXT]");
```
With above example if for some reason the first function goes to error will be passes to "expect" and will impress [TEXT].

Have in consideration this; "expect" takes "str" as input, so you can not pass a string directly, you need convert it first. That "str" return of the previous function,object,variable or method is an "Err" return. Take it; is not a normal return, the type is "Err".

### read_line( [variable] ) and read_line_prompt(msg: &str)
This object works with "stdin()" because reads a line (pay attention to it, a line) and store it in [variable] which must be a variable formatted as string.
```rust
stdin().read_line(&mut [variable]);
```

You can use the variation; read_line_prompt(msg: &str).

That function shows to user the string passes as argument ( the text beetwen double quotas ) before call to read_line to store the input.

### parse()
As many functions, this is one of the most helpfull objects in Rust.

Syntax;
```rust
[variable_target]: [new_type] = [variable1].[another_object_or_not].parse()
```

Parse will transform a string slice from [variable1] into another type, generally into the variable's target type.

I'm sure to say that you will use this method a lot.

### trim()
This is a very helpfull object.

Syntax;
```rust
[variable].[trim_function];
```

- "trim()" removes the leading and trailing whitespaces and tabulations in a string.
- "trim_start()" only removes the leading whitespaces and tabulations in a string.
   - note

     trim_left was deprecated and replaced with "trim_start".

- "trim_end()" only removes trailing whitespaces and tabulations in a string.
   - note

      trim_right was deprecated and replaced with "trim_end".

- "trim_matches('[X]')" removes the pattern [X] from leading and trailing possitions in a string.
- "trim_start_matches('[X]')" removes the pattern [X] from leading possitions in a string.
- "trim_end_matches('[X]')" removes the pattern [X] from trailing possitions in a string.

### strip
Strips from strings the [XXXX] pattern. Obviusly the return is an string to passed variable.

Syntax;
```rust
[variable].[strip_function];
```

- "strip_prefix("[XXXX]") " removes the pattern [XXXXX] from leading possitions in a string.
- "strip_suffix("[XXXX]") " removes the pattern [XXXXX] from trailing possitions in a string.

### is_ascii()
Checks if the string has ASCII values. Returns a boolean type.

Syntax;
```rust
[variable].is_ascii();
```

### len()

Returns the numbers of bytes of variable size. Pay attention; "numbers of bytes", NOT "number of chars/etc" (yes, in ASCII table each value use 1 byte but it will not be like this for ever). Returns interger.

Syntax;
```rust
[variable].len();
```

### is_empty()
Check if the variable has not information inside. Returns a boolean type.

Syntax;
```rust
[variable].is_empty();
```

### as_bytes()
Transforms each character into byte equivalent. Returns integer type.

Syntax;
```rust
[variable].as_bytes();
[variable].as_bytes_mut();
```

### Assert
Assert is a macros family to compare one or two things. The only common behaviour is they found that do not match with expected result, will call panic! and finish the program.

This apply not only for common variables and types, also for returns.

- To check if something's returns is 'True';
```rust
assert!([thing], [message_to_show_if_panic], [variables_if_panic_message_have_variables]);
```

- To check if two things are equal;
```rust
assert_eq!([thing_1],[thing_2],[message_to_show_if_panic], [variables_if_panic_message_have_variables]);
```

"[thing_1]" is called by rust "left" and "[thing_2]" is called by rust "right".

- To check if two things are not equal;
```rust
assert_ne!([thing_1],[thing_2],[message_to_show_if_panic], [variables_if_panic_message_have_variables]);
```

"[thing_1]" is called by rust "left" and "[thing_2]" is called by rust "right".

### Contains
Contains functions returns true if XXX is in the value. 

There are many implementations and crates to try under scope depending the scenario and the target variable;
1. std::slice::contains
2. std:str::contains
3. std::option::Option::contains

Etc.


## Control Flow; if, else, else if, loop, while and for 

There are many ways to control the program's flow, all those ways are with a conditional comparation; if this is [something] to this other, do this, if not do this.

### if, else and else if
"if" statement is what you think. If the condition is right do the code inside "{}" if not continue. This statement can work with numbers, strings and any rust standard type.

The condition can be within "()" but probably rust's compiler will tell you to delete them, this is because will try that you avoid it if they are not needed.

For example to comparate two numbers;

```rust
fn main() {
    let var1 = 45;
    let var2 = 300;
    if var1 < var2{
        println!("{} is lower than {}",var1,var2);
    }
}
```

The above code will test if "var1" (with value 45) is lower than "var2" (with value 300), if that condition is true will execute the code whitin "{}", in this case print in screen.

The "if" statement can not just work with numbers, as I said before; can works with any rust standard type.

In the condition you can use any function, even their returns;

```rust
fn main() {
    let var1 = "Hello World";
    if var1.is_empty() != true {
        println!("{} is not empty",var1);
    }
}
```

The above code will create a variable with string "Hello World", then will test if "var1" is empty.

If the if's return is "true" will not execute something, but if is not (that means "!=") true will execute the code whithin "{}".

But, what if you want do a test and take more than one action considering the condition's returns? Easy;

```rust
if [condition] {
	[code_to_execute_if_condition_true];
}
else if [second_condition]{
	[code_to_execute_if_the_first_condition_was_false_but_this_second_is_true];
}
else {
	[code_to_execute_if_all_conditions_are_false];
}
```

You can use as many "else if" you need.
As you can think, all condition's returns are bool type (True or False).

Here some of if, while, for and else operations (remember that you can use normal opterations, not just aritmetic);
- a < b

If a is lower than b.

- a > b

If a is granten than b.

- a == b

If a is equal to b. Do not confuse with a single equal; "=" which is an assigner, not a comparation.

- a

Check if a is equal to "True" (the boolean value).

- !a

Check if a is equal to "False" (the boolean value).

```rust
fn main() {
    let var1 = "Hello World";
    if !(var1.is_empty()) {
        println!("{} is not empty",var1);
    }
}
```

The above code is the same than before, but replacing " != True" with the smallest way.

As "if" is an expression, you can use it to control returns;

```rust
fn main() {
    let var1 = "Hello World";
    let vreturn1 = if !(var1.is_empty()) {
       5 
    } else {
        1
    };
}
```

With above code, vreturn1 variable will have value 5 if the return of  evaluation; var1.is_empty() is false, otherwise will have value 1. If you use "if", "else if" and/or "else" to assign values as returns to variables, remember you MUST use the same values' types in each arm of "if", "else if" and "else" expressions, so consider it when you create your programs.


### Repetition with loops; loop, for and while

- Loop

'Loop' tells to rust to execute something until that process is stopped explicitly.

Syntax;
```rust
fn main() {
    let mut x: i64 = 10;
    loop {
        println!("this is a loop");
        x = x +1;
	if x == 13 {
		break;
	}
    }
}
```
With above command rust create a variable called "x" of type; interger 64 bits, assigned with value "10". 
Then execute the flow in "loop" printing "this is a loop" and adds one to it (because of that the "x" variable have "mut" word). Then evaluate if "x" is equal to 13, if is break the loop using the function "break".

If you specify an argument in "break" will works as return value, for example;
```rust
[code];
break x +1;
}
```

If you need create/use a loop with conditional access, there are better options like; while and for.

- While

'While' use (as the name sugest) a conditional test to know if execute the loop code or not.

Syntax;
```rust
while [condition] {
	[code_to_execute_if_condition_works];
}
```

For example;
```rust
fn main() {
    let mut x: i64 = 10;
    
    while x < 13 {
        x += 1;
        println!("{}",x);
    }
    println!("Ended while loop");
}
```

The above code will create a mutable variable of interger 64 bits type called "x" with value 10. Then will execute the code inside while block if the condition ( x < 13 ) is true, adding one to x and then printing the value. When the loop finish will print "Ended while loop".

While is good when you do not need works with variable values in fixed sizes (like use variables in arrays and tuples), but if you need it the better option is "for".

- For

"For" is a special case, this is because works different depending of the language ("for" in C,C++ is not same in Rust, Python, etc). Rust's "for" iterate in someting (commonly; a variable) and in each interation will execute the code inside "{}".

Syntax;
```rust
for [new_variable] for [variable_with_information] {
	[code_to_execute];
}
```

For example;
```rust
fn main() {
    let var1 = [1,2,3,4,5,6];
    for iteration1 in var1 {
        println!("{}",iteration1);
    }
}
```

The above code will create an inmutable variable with an array of six values; 1,2,3,4,5 and 6.

Then will execute the "for" loop; will create a new variable called "iteration1". That new variable ("iteration1") will have each value of "var1" in order; will take "1" as value and then will execute the code inside "{}", then will take as value "2" and will execute again the code, and it to finish with the last value (in this case "6") and the execution of code. Take in consideration that can be or not in order the information retrived, but if you use the "rev" family functions and macros (for example, there are a lot more ) the information retrived will be different.

## First code 
Now with your knowledge about Rust, we will do a program to convert Celcius to Fahrenheit;

As 1°C are 33.8° F the convertion is simple;

```rust
use std::io;

fn f_t_c_fn(user_input: String){    
    let mut user_input2: String = String::new();
    let f_t_c: f64 = 33.8;
    let mut is_number: f64;
    
    println!("Insert number to convert;");
    io::stdin().read_line(&mut user_input2).expect("Error taking imput.");
    is_number = user_input2.trim().parse().expect("Error. Is not a number.");         
    
    if (user_input.trim() == "C".to_string() || user_input.trim() == "Celsius".to_string()){
        println!("{} to Fahrenheit; {}",is_number, is_number + f_t_c);
    }
    
    else if (user_input.trim() == "F".to_string() || user_input.trim() == "Fahrenheit".to_string()){
        println!("{} to Celsius; {}",is_number, is_number - f_t_c);
    }
    
    else {
        println!("Valid options were not selected.");
    }
}

fn main() {
    let mut user_input = String::new();
    
    println!("Convert from Celsius to Fahrenheit (C/Celsius), or from Fahrenheit to Celsius (F/Fahrenheit)?");
    io::stdin().read_line(&mut user_input).expect("Error taking input.");
    
    f_t_c_fn(user_input);
}
```

The above program is simple but uses all knowledge acquired to now. First import the create; InputOutput from standard library. 

Then create a function called "f_t_c_fn" which takes as argument "user_input" with "String" type (I use the same argument's name as the variable that I pass to the function, but is not neccessary).

In the "f_t_c_fn" function, create an mutable variable called "user_input2" with "string" type assigning as value an empty string. Then create two float 64bits variables called "f_t_c" and "is_number".

Ask the user to imput values reading line from standard imput/otput, saving the values in the mutable variable "user_input2". If the imput values fails, show the error "Error taking imput.".

The good code and objects use is here; the "user_input2" will passed to "trim" object, the result will passed to "parse" object, the result of it will passed to "is_number" variable. Remember, that variable is 64bits float, so if the convertion (by "parse") was done properly, the result is assigned to "is_number", if there is an error with the convertion is passed to "expect".

Then start the comparation, and in my opinion take this carefully (not because you must read this with care, because you must understand why I wrotte it) and with very attention. We start a comparation with “if” and we include all the comparations inside “()” because we are not just doing one comparation; we are doing two comparations). First we delete all possible spaces at the start and end of “user_input” to check if is equal (remember, two ==, one = is for assign values) to “C”, but “C” or werever other alphabetycal value can not be compared directly with an string so after the string we pass it to “.to_string” call object to do the convertion properly. Then is specified the “or” exclusive condtion with “||” (“and” is “&&") to check the same but with “Celsius” string.

Take in consideration this about “or” and “and” conditionals in “if”/“else if”; when you use “or” || with two or more conditionals, is enogh that just one be true to execute the code inside if’s “{}”. When you use “and” && with two or more conditionals, all of them MUST be true in each one to execute the code.

Then, if the conditionals are true show in screen two variables; first user_input and then “user_input +/- f_t_C” depending of user’s selection.

So when the program execute, takes the user input and pass it to “f_t_C_fn” function and do the properly operations.

## Ownership

### RAM management

Take the RAM as an stack;

```
|--------------|
|    Value 5   |
|--------------|
|    Value 4   |
|--------------|
|    Value 3   |
|--------------|
|    Value 2   |
|--------------|
|    Value 1   |
|--------------|
```

The stack size depends a lot things; the OS, how the CPU configure the RAM’s frames, the CPU’s architecture, etc.

The sstack stores values in the way; “first in, last out” or “last in, first out”. So the first value “Value 1” is below “Value 2” and so on, if you want retrive a value from stack, you must start from upper to lower, so if you want the “Value 3” you must frist move 4 and 5 to another place before take 3.

Adding values to the stack is called “push” and retrive is called “pop”.

The “push” action store values in stack’s top, and the “pop” action retrive values from stack’s top.

In Rust’s webpage is explained in a perfect way;
```
All data stored on the stack must have a known, fixed size. Data with an unknown size at compile time or a size that might change must be stored on the heap instead. The heap is less organized: when you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer, which is the address of that location. This process is called allocating on the heap and is sometimes abbreviated as just allocating. Pushing values onto the stack is not considered allocating. Because the pointer is a known, fixed size, you can store the pointer on the stack, but when you want the actual data, you must follow the pointer.

Pushing to the stack is faster than allocating on the heap because the allocator never has to search for a place to store new data; that location is always at the top of the stack. Comparatively, allocating space on the heap requires more work, because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.

Accessing data in the heap is slower than accessing data on the stack because you have to follow a pointer to get there. Contemporary processors are faster if they jump around less in memory. 
```
When your code calls a function, the values passed into the function (including, potentially, pointers to data on the heap) and the function’s local variables get pushed onto the stack. When the function is over, those values get popped off the stack.

Keeping track of what parts of code are using what data on the heap, minimizing the amount of duplicate data on the heap, and cleaning up unused data on the heap so you don’t run out of space are all problems that ownership addresses. Once you understand ownership, you won’t need to think about the stack and the heap very often, but knowing that managing heap data is why ownership exists can help explain why it works the way it does.

### Ownership rules

In Rust there are three rules about the ownership;

    Each value in Rust has a variable that’s called its owner.
    There can only be one owner at a time.
    When the owner goes out of scope, the value will be dropped.

### Memory

In all programming languages, the data stored and managed by the programm must be in memory. Here there are two possible options;

   - The programmer is the responsible to request memory and free the unused memory.

   - The language have a garbare collector (GC) which analyze the program’s memory and release the unsued memory.

Well Rust is more like the first, the programmer is the responsible to request data allocation in memory and release when it is not used. In Rust as many other languages the more common way to do it is using functions. But, generally, all programming languages works in the same way when is about stack and heap.

Rust as other languages, have a method to control the information. Supose you have this code;

```rust
fn function1(){
	let mut var1 = String::from("Hello ");
	var1.push_str(" World.");
}

fn function2(){
	let mut var1 = String::from("How are you?");
	println!("{}",var1);
}
```

In above code we have a variable called “var1” one in function1 and the other in function2, when (in function1) the code block ends, the memory allocated in stack to storage “Hello World.” is relased and cleaned, so when “function2” create a variable with the same name and different value in stack, the other information will not crash with this new one.

Rust execute a call ‘drop’ when a code block ends.

This is the more basic thing about ownership in Rust; each variable and value is valid (and stored in RAM) until the code block ends. But it will not work if you are using an external variable (like a normal external variable, functions' arguments or struct for example). So remember; modulate your code in functions as you need do differents things, only pass data into one function using structs, functions' arguments or external variables ONLY and ONLY if you really need that data and DO NOT return data outside the function if you REALLY do not need it, and also if you have a variable “x” which contains information to only “y” function, do not create that variable at “main” function (a habit from C or C++ from Universities generally), create it inside that “y” function so the Rust’s ownership can work properly.
Variable scope

Let us say we have this piece of code:

```rust
let var1 = String::from("Hello World.");
let var2 = var1;
```

We have a variable called “var1” which contains in memory the value; “Hello World.” but, unless you maybe are thinking, the variable have not that value directly into stack. In var1’s stack is only the information about a poiter (which points, as the name said, to the heap location where the complete information is stored, in this case “Hello World."), the size integer (which contains in bytes the size of data allocated into the heap) and the capacity integer (which contains in bytes the max size that the variable can store into the heap using the pointer).


### Variable scope and memory management

Let us say we have this piece of code:

```rust
let var1 = String::from("Hello World.");
let var2 = var1;
```
We have a variable called “var1” which contains in memory the value; “Hello World.” but, unless you maybe are thinking, the variable have not that value directly into stack. In var1’s stack is only the information about a poiter (which points, as the name said, to the heap location where the complete information is stored, in this case “Hello World."), the size integer (which contains in bytes the size of data allocated into the heap) and the capacity integer (which contains in bytes the max size that the variable can store into the heap using the pointer).

![](rust-trpl04-01.svg)

Copyright Rust Learn Book

So when we assign “var1” to “var2” we only are copping that identifiers; the pointer, the size and the capacity. The pointer in both cases are pointing to the same heap location, this can create a huge issues, just for say two; two or more variables modifing at the same time the values and if one goes out of scope, what happen with that data? Goes or not out of scope?. To avoid that issues and a lot more, Rust goes out of scope “var1” even if the block code doesn’t ended, so the only valid variable is “var2”. Take this very carefully because is important.

![](rust-trpl04-04.svg)

Copyright Rust Learn Book

To review; one variable when is using the ‘String’ type have three identifiers values; a pointer to the heap’s data, an interger with the size in bytes of heap’s data and an integer with the capacity to store heap’s data. If you assign one variable to another ( variable2 = variable1) you only are coping that idenfiers, and as there are two or more pointers pointing to the same heap’s location, Rust to avoid security issues invalid the first variable (variable1) going out of scope and memory, so only the last (variable2) will be the valid.

This action (coping identifiers and invaliding the first variable after the copy) is known as ‘move’ and ‘borrowed’. And this only happens in operations that involve the heap (such as the ‘String’ type). In integers, floats, booleans, chars and tuples (only if have those types of values, if have String type will not) has the size is known at compiling time, the information will be to stack, not to heap, because of that there are not identifiers, just data. So you can assign the same variable to anothers as you need, in operations ivolving stack you certainly will be coping the data (in Rust this is defined as; implement Copy trait).

If you have a variable which uses heap (for example, as we said before, ‘String’ types) and you really need copy the idenfiers and the heap’s data, you can use the object “.clone” or function “clone_from()”.

Now we must cover one variable’s scope topic; the functions arguments.

As we said before when we explained what is a function, the arguments are just variables that after you use into the function’s code. But, now we know how that ownership works in Rust, what happen with the ownership of arguments?

When you declarate a function and specify the arguments and arguments' types you have two options; specify with or without ‘&’ into the variable’s type when you create a function.

The ‘&’ indicate the use the memory alocation of that argument. When you pass a variable and was not specified the ‘&’ as reference, there are two options; Rust will copy the value (if is an integer, floats, boolean, char or compatible tuple) but if the variable works with the heap (as String type) the ownership of that variable will be moved to the new function so that resource will be reserved until that function release it (as a return) and if that resource was not returned it will not be longer available because will be dropped (remember ownership). If you pass as reference, and works with the variable modifing the value assigned, the original variable will be modified too but you need declarate it in specific with “& mut” after the name and before the type.

Example:
```rust
fn main() {
    let var1: f64 = 4.89;
    let var2: u64 = 5555;
    let var3: String = String::from("Hello World");
    let mut var4: String = String::from("Mutable argument");
    
    function1(var1,var2,var3, &mut var4);
    println!("var1: {}, var2: {}, var3: {}", var1,var2,var3);
}

fn function1(var1: f64, var2: u64, var3: String, var4: &mut String){
    var4.push_str(". And this second part was appended.");
    println!("var1: {}, var2: {}, var3: {}, var4: {}", var1,var2,var3,var4);
}
```

If you try to execute the above code you will get this type of error; “borrow of moved value: var3 " that is because as we say before because the size of integers, floats, booleans and chars are known at compiling time, ‘var1’ and ‘var2’ will be copied when are passed as arguments to ‘function1’ but as ‘var3’ and ‘var4’ are Strings and are not size known at compiling time, the ownership will be passed to ‘function1’ so if you not return ‘var3’ ‘main’ will have not the ownership back and ‘var3’ will be dropped when ‘function1’ ends. With ‘var4’ as was passed as reference (remember; &) and mutable will be not problem because remember; when is passed as reference the ownership is not moved.

So each time you pass the ownership of a variable because you are passing it as argument without ‘&’ as reference, you must return it to return the ownership. And the right way to do the above code is;

```rust
fn main() {
    let var1: f64 = 4.89;
    let var2: u64 = 5555;
    let var3: String = String::from("Hello World");
    let mut var4: String = String::from("Mutable argument");
    
    let var5 = function1(var1,var2,var3, &mut var4);
    println!("var1: {}, var2: {}, var5 (ex-var3): {}", var1,var2,var5);
}

fn function1(var1: f64, var2: u64, var3: String, var4: &mut String) -> String{
    var4.push_str(". And this second part was appended.");
    println!("var1: {}, var2: {}, var3: {}, var4: {}", var1,var2,var3,var4);
    
    var3
}
```

When you return a variable, or a value which is the same, the ownership change from the function to the function who call him, because you are doing a ‘move’ operation. Using the above code; as we returned the ownership of ‘var3’, when is returned it the ‘var3’ original is not still available with it ID (identifier) because was moved out of ‘main’ when was passed to ‘function1’ so we need save it in a new variable; ‘var5’.

Take carefull with one restriction to mutable arguments and variables; you can only assign one mutable variable to another, as Rust Learn Book says;

you can have only one mutable reference to a particular piece of data at a time.

This can be disturbing for new people, but this is very helpfull to avoid that two or more pieces of code change at the same time the same information.

But; (yes, ownership in Rust is not simple) you can assign the same variable as reference to two or more pieces of code if they are referenced. Think that as when you are using reference you are creating a pointer to that variable’s RAM.

For example, this code is right:

```rust
fn main() {
    let var3: String = String::from("Hello World");
    let mut var4: String = String::from("Mutable argument");
    let var5 = function1(var3, &mut var4);
    println!("var5: {}",var5);
}

fn function1(var3: String, var4: &mut String) -> String{
    var4.push_str(". And this second part was appended.");
    let var6 = &var4;
    let var7 = &var4;
    println!("var6: {}, \n var7:{}", var6,var7);
    var3
}
```

As you can see in the code, we are passing two arguments to function1; var3 and var4. var3 is passed normally, so we must return to retrive var3’s ownership to main, var4 is not necessary to return because was passed as mutable and by reference so ownership remains in main and because it (var4) was passed so, we can create two new variables; var6 and var7 referencing them to var4, this is because both variables are not overlaping in scope.

### Memory scope and pointers

From Rust Learn Book this excelent explaination;

```
In languages with pointers, it’s easy to erroneously create a dangling pointer, a pointer that references a location in memory that may have been given to someone else, by freeing some memory while preserving a pointer to that memory. In Rust, by contrast, the compiler guarantees that references will never be dangling references: if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.
```

So, if you use data and a pointer pointing to it, and the data is dropped, Rust will drop also the pointer.
#### Note from ShyanJMC

You can create as many sub ownerships inside any code as you want (to even restrict to memory level the ownership by yourself) using brackets; { and }

## Second Code
With everything that we saw before, we will re-implement the Celsius to Fah convert but know more detailed.

One consideration; the most technical implementation sometimes is not the best. Always choose the simplicity instead of try to show your technical skills, why? Because yes, you can programming a very technical and good implementation but maybe you are using 5x or 10 more CPUs cycles instead of less and it in IOT (Internet Of things, a marketing name for embedded devices with low resources) is a VERY HUGE error. If you will implement very technical things, use matematical algoritms with they to enhance the performance.

This example use verything described before but as I said before this example use a lot of unnecessary things, the first code is more eficient in resources.

```rust
use std::io;

struct Values {
    fahrenheit: f64,
    number_input: String,
}

fn f_t_c_fn(input: &String) -> String {
    let mut instance = Values {
        fahrenheit: 33.8,
        number_input: String::new(),
    };
    let mut is_number: f64 = 0.0;
    let (mut temporal, mut message) = (String::from(""), String::from(""));
    
    println!("Insert number to convert;");
    io::stdin().read_line(&mut instance.number_input).expect("Error taking imput.");
    is_number = instance.number_input.trim().parse().expect("Error. Is not a number.");         
    
    if (input.trim() == "C".to_string() || input.trim() == "Celsius".to_string()){
        temporal = (is_number + instance.fahrenheit).to_string();
        temporal
    }
    
    else if (input.trim() == "F".to_string() || input.trim() == "Fahrenheit".to_string()){
        temporal = (is_number - instance.fahrenheit).to_string();
        temporal
    }
    
    else {
        message.push_str("Valid options were not selected.");
        message
    }
}

fn main() {
    let (mut retur,mut input) = (String::from(""),String::from(""));
    
    println!("Convert from Celsius to Fahrenheit (C/Celsius), or from Fahrenheit to Celsius (F/Fahrenheit)?");
    io::stdin().read_line(&mut input).expect("Error taking input.");
    
    retur = f_t_c_fn(&input);
    println!("You selected {} \n{}",input,retur);
}
```

We import the “io” module from “std” (standard) crate.

Then we create a new type called ‘Value’ which have to variables, one of float 64 bits type and the other as a string, this new type is created as a struct.

- Starting from main:
We start creating two mutable variables, both are iniatialized as Strings without values. Then we print in screen a message and then, in the next line, we call the function stdin from io module, the input from standard input we pass to read_line function which reads it and store it into the mutable function “input”, if it fails print the message from expect function.

Then we call “f_t_c_fn” function passing as reference the argument/parameter variable “input” so the ownership of that variable do not change and it will be valid even when “f_t_c_fn” ends. The return of that function is stored into “retur” mutable variable. At the end prints the input’s and retur’s values.

- Passing to f_t_c_fn function:

As we said before, main function passed “input” variable as reference, this is because if you see the function’s header you will see that we specified use the parameter with name “input” as String type and as reference, with a return of String.

Then at the code’s body we create a new mutable variable called “instance” with the struct’s type ‘Value’ initializing it with value ‘33.8’ to fahrenheit variable and as all variables must be initialized when you create a struct’s instance, we init the string variable with an empty string for “number_input” variable.

Then we create three variables, one of float 64 bits type initialized with value “0.0” (is recommended init every variable) and the next two are initialized as empty strings. Next we print in screen and request user to input value storing it in the before created struct (the variable “instance”) where we store the value inside the string variable of he (variable; number_input) with the respective error message from “expect”. Then, we take the field “number_input” from “instance” variable and pass it to trim to delete spaces and tabulations, then it is passed to parse to convert it to “is_number” type (becuase of that these operation is assigned as return value to it) with a message assigned to “expect” is fails that converse, so with this we know if really the input is a number or not.

Then we compare the passed by reference variable “input” (deleting possibles spaces and tabulations with “trim”) to strings “C”,“Celsius”,“F” and “Fahrenheit” (becuase of that are passed to “.to_string” to convert it to that) because the first is it, so we must convert those too to do properly.

If is equal to some of the operations, we add the addition of the number imput more/less (depending of the operation) the fahrenheit number and then we convert it to string to return then that variable as string.

As I said before, the first code is best to do this simple program, because with the same information works better and with more performance. Remember; not always the most technical program is the best. As KISS philosophy says; Keep it simple, stupid.

## The next step; an intermediate Rust level
From now I will change some things about this wiki, from now you must know;

- I will not write the complete code of the program, from now you must know everything what you saw before, I will just write the functional code.
- With the above, I recommed to you review everything. In special about ownership.
- As intermediate level, from now you will see; methods, modules, crates, vectors, traits, lifetime and files.

## Debug mode

'debug' in informatic means; see what is happening in RAM (memory) so I can understand what is the issue and fix it.

Rust works a lot with environment variables, so to enable/disable debug in rustc and cargo (which use rustc to compile) you must set;
```rust
RUST_BACKTRACE=[0/1];
```

Set to zero for disable and one to enable it. 

Please, not enable debug if you are compiling to release the binary because you will have enabled it into the binary.

## Method
Before we saw how to create a struct’s instance and then change the values, but now we will see how to associate a function to it to modify in a better way.

Suppose that you implement a function to modify a struct’s instance passing it by reference (to not change the ownership) and if you not passed it by reference, storing the return into a new variable to keep working with it. In this case, you will write a lot of unnecessary code, remember the first words in this sentence “implement”. When you implement a function associated directly to a struct (and to owner variable, of course) you are doing it; an implementation.

So, Rust have a very usefull thing to modify it without doing a lot of unnecessary things; implementations.

The implementation works with;

- structs
- enums
- traits

Have this particular things;

- ALWAYS the first argument/parameter is “&self” which represents the struct’s/enums'/traits' instance. Of course, as you probably know, using just “&self” will obligate you to only return values, but if you want modify the instance’s fields remember use “&mut self”. 
- always go outside functions, like structs, enums and/or traits.

Syntax;

```rust
[struct_enum_or_trait];

impl [struct's_enum's_or_trait's_name] {
	fn [function_name](&self, [rest_of_parameters] -> [return] {
		[code]
	}
}
```

Then when you call it, you must have the variable instance initliazed with the respective struct, enum or trait and then do; [variable_instance].[function_name]

Here an example about a fundation who stored the mankind knowledge and are using the ancestral Rust to create their programs (of course some counts are arbitrary);

```rust
struct Library_knowledge {
    books: f64,
    stories: u64,
    unfinished: f64,
    finished: f64,
    average: f64,
}

impl Library_knowledge {
    fn create_inventary(&mut self){
        self.average = (self.unfinished + self.finished)/2.0;
    }
    
    fn stories_counts(&self) -> f64 {
        self.books.floor()
    }
}

fn main(){
    let mut var1 = Library_knowledge{
        books: 285.0,
        stories: 150,
        unfinished: 20.3,
        finished: 179.7,
        average: 0.0,
    };
    var1.create_inventary();
    println!("Average: {}, Stories counts: {}", var1.average, var1.stories_counts());
}
```

## Enums type
Enums are a special type of structs in which you can create your own type and values, this allows to group many new types into the same enum but the variable can not be all enum's types, you must specify one. Is an object, because of that you can not set your custom value directly must be assigned.

The syntax when you create and assign the enum is;
```rust
enum [enum_name]{
	[type_1](primitive_type),
	[type_n](primitive_type),
}

let [variable] = [Enum_name]::[type_n];

```
The main feature of enums is that each enum's type can hold or not any primitive value (chars, strings, intergers, floats, etc) specifing it as type.

For example;
```rust
enum IPAdrr {
        V4(String),
        V6(String),
        Port(u64),
}

fn main() {
	let var1 = IPAdrr::V6;
	let var2 = IPAdrr::V4(String::from("10.0.0.1"));
	let var3 = IPAdrr::Port(443);
}
```
With above code we are creating a new type called 'IPAdrr' with tree possibles types; V4 (which allows Strings values) , V6 (which allows Strings values too) and Port (which allows integer 64 bits values). The first variable is "var1" have the type "V6" without value, the second "var2" have the type "V4" with string value ("10.0.0.1") and the last variable "var3" have the type "Port" with integer 64bits value "443".

But enums can hold more than one primitive type:
```rust
enum Address {
        Web(String, String, u32),
}

fn main(){
    let var1 = Address::Web(String::from("http3"),String::from("http://kernel.org"),443);
}
```
With above example, we are creating a variable called "var1" of Address's Web type with three values; two strings and one integer unsigned 32 bits.

As with structs you can link enums with others enums, this is because when you create your subtype, at compilation and execution time will be as another types:
```rust
enum Address {
    Web(HttpProtocol, String, u32),
}

enum HttpProtocol {
    Http(u32),
}

fn main(){
    let var1 = Address::Web(HttpProtocol::Http(3),String::from("http://kernel.org"),443);
}
```
With above we are creating a new enum called "HttpProtocol" with custom type "Http" which allows possibles values as unsigned interger 32 bits. Then we configure that in "Web" type (in Address enum) the first argument must be a value from "HttpProtocol" enum.

As you are creating a new type with [enum_name] as name, you must specify it in the variable's type when you need use it in function's arguments:
```rust
fn [function]([var_name]: [enum_name]) ....
```

Also you can use "impl" (implements) in eums. The syntax is the same as in structs (remember the keyword "&self" into the function's argument).

### Option

As enums only allows set one type per variable and can use "impl" as structs, is the best option to work the function's and object's returns to evalute if it is something or nothing. For "nothing" we means the "NULL" type of C,C++. Rust have not the "NULL" type for security reasons.

From Rust's book:
```
The problem with null values is that if you try to use a null value as a not-null value, you’ll get an error of some kind. Because this null or not-null property is pervasive, it’s extremely easy to make this kind of error.

However, the concept that null is trying to express is still a useful one: a null is a value that is currently invalid or absent for some reason.
```

So to avoid the use of NULL types the Option enum works doing that comparation. Enum Option is in the standard library.
```rust
enum Option<T> {
    None,
    Some(T),
}
```
"T" means "any type". "None" is used when the value is equal to NULL and "Some" when exist a value. 

So the new type that are we creating here is bidirectional. This is because when you assign a value to "Some" by "T" will impact directly in "Option" converting the value to; "Option<T>" type. For example (from Rust book);
```rust
let some_number = Some(5);
let some_string = Some("a string");

let absent_number: Option<i32> = None;
```
With above code "some_number" is type "Option<i32>" (i64 in some architectures), "some_string" is type "Option<&str>" and "absent_number" is type "Option<i32>" but do not have any value so is initialized as "None" (equivalent to C as NULL). So the first two variables are valid because contains values but the last not.

What adventages privde the use of Option<T>:
- You will avoid security issues and logical issues about use void variables (None in Rust, NULL in C/C++) in operations with valid variables (variables with Some in rust).
- You will avoid security isues and logical issues about use Option<T> variables with T variables. Remember "T" and "Option<T>" are different types.

With the last point; how do you cast (convert) from "Option<T>" to "T" ? With "match" operator, the Option's "if".

As a type, of course you can work with them in the same way with the rest.

### Match
Match operator check if variable is "Some(T)" or "None" and the type of "T" to execute the options properly.

Is the specific operator to compare "Options<T>".
 
Syntax;
```rust
[variable_x]: Option<[variable_E_and_type]>;

match [variable_x] {
	None => [Code_or_return],
	Some[variable_E] => [Code_or_return],

	[Others_comparations] => [Code_or_return],
	...

	_ => [Code_or_return],
}
```
The match's process is; match takes the variable_x's value (or type if is not a variable but also type if is) and start the comparations;
- Is the variable_x's value empty (None) ? If is execute the code or provide the return specified in [Code_or_return].
- Is the variable_x's type the same as Some[variable_E]? If is execute the code or provide the return specified in [Code_or_return].
- And then also can do another comparations like; is variable_x's type or value equal to Z? If is execute the code or provide the return specified in [Code_or_return]. 
- At least with " _ " you are saying "ok, if nothing match with [variable_x] go here" and then execute the code or provide the return specified in [Code_or_return].

ShyanJMC's Notes:
- If you return some value in any of the match's arms, the rest of returns match the same type. You can not return different types, even if are in differents arms.
- In 90% of cases you will can not use an object directly like " Some("string".to_string()) " because directly operation's returns in "Some"'s operations are not allowed. You must use variables.
- If you use match with some enum's variable, you can not compare directly None because both types are not equals. One is [enum_name]::[type] and the other is Option<T>.
- If you are using enums with match, remember; <T> if you specify in match's arms the type as value instead of pure type (i32 for example) the value must equal with variable.
- As with "if" and others you can call functions in match's arms. But remember, the function's arguments called must be the same type than the others match's arms.
- If Rust understand and knows in compiling time the variable's type, will tell you that it will never match with X. Generally as warning notification.
- If in some arms you don't want/can return or execute something, you can simply put "()".


For example;
```rust
enum Customtype{
    Newt1(i32),
    Newt2(String),
}

fn dummy_function(x: i32) {
    println!("x: {}",x);
}

fn main() {
    
    let _var1 = Some(30);
    let _var2 = Some("a str");
    let _var3 = Customtype::Newt1(30);
    let _var4 = Customtype::Newt2("another string".to_string());
    let _var5 = 5;
    let _var6 = "another string".to_string();
    let _var7 = "another_string".to_string();
    
    let _retrieve1 = match _var1 {
        None => {
            println!("The var1 is None");
            0
        },
        Some(5) => {
            println!("Is 5 i32 the type of var1");
            1
        },
        Some(30) => {
            println!("Is 30 i32 the type of var1");
            1
        }
        _ => {
            println!("var1: No matches");
            -1
        }
    };
    
    let _retrieve2 = match _var2 {
        None => {
            println!("The var2 is None");
            0
        },
        Some(String) => {
            println!("Is String the type of var2");
            1
        },
        Some(str) => {
            println!("Is str the type of var2");
            1
        },
        _ => {
            println!("var2: No matches");
            -1
        },
    };
    
    let _retrieve3 = match _var3 {
        Customtype::Newt1(i32) => {
            println!("The var3 is Customtype::Newt1(i32) type");
            1
        },
        Customtype::Newt2(String) => {
            println!("The var3 is Customtype::Newt2(String) type");
            1
        },
        _ => {
            println!("var3: no matches");
            -1
        },
    };
    
    let _retrieve4 = match _var4 {
        Customtype::Newt1(i32) => {
            println!("The var4 is Customtype::Newt1(i32) type");
            1
        },
        Customtype::Newt2(String) => {
            println!("The var4 is Customtype::Newt2(String) type");
            1
        },
        _ => {
            println!("var4: no matches");
            -1
        },
    };
    
    match _var5 {
        5 => { 
                println!("_var5 have value; 5");
                dummy_function(_var5);
            },
        _ => println!("_var5 do not have value; 5"),
    };
    
    match _var6 {
        _var7 => println!("_var6 have value 'another_string'"),
        _ => println!("_var6's value do not march"),
    };
    
}
```

With above code we are creating an enum called "CustomType" with two new subtypes; "Newt1" which can only hold i32 value, and "Newt2" which can only hold Strings values.

Then we create a function "dummy_function" with an argument "x" of i32 type.

In main we create this variables;
- let _var1 = Some(30);

So "_var1" is "Option<30>" type.

- let _var2 = Some("a str");

So "_var2" is "Option<str>" type.

- let _var3 = Customtype::Newt1(30);

So "_var3" is "Customtype::Newt1(i32)" type. Remember is not the same compare type in enums and Options.

- let _var4 = Customtype::Newt2("another string".to_string());

So "_var4" is "Customtype::Newt2(String)" type.

- let _var5 = 5;

So "_var5" is i32 type.

- let _var6 = "another string".to_string();

So "_var6" is String type.

- let _var7 = "another_string".to_string();

So "_var7" is String type.

After that, start the "match":
1. First we start comparing "_var1" variable. As is "Option<30>" type we must include "None" comparation, if is empty will be printed "The var1 is None" and then will return "0". If do not match, will check if equals with "Some(5)", remember "Some(5)", so it is the Type which is not the same as "Some<u32>", and as is it will print and then return 1. The rest of code is if equals with "Some<30>" and if none matches (Which is not this case) will print and then return -1.

2. The same with "_var2", the parts "Some(String)" will check if is it type and "Some(str)" it type.

3. With "_var3" and "_var4" check the same with "Customtype::Newt1(i32)" and "Customtype::Newt2(String)" types. But here is the difference, as "_var3" is an enum and not "Option<T>" so here as is specified "i32" and "String" we are including them as types not as values, so any value inside them types will match. In this case match with "Customtype::Newt1(i32)".

4. With "_var5" we are not checking against types, we are checking if equals with values; "5" so if the specific value of "_var5" is five, will print and call "dummy_function()" if not will print (the "_" arm).

5. With "_var6" we are checking against variables, so both variable must be exactly the same to check's value be true.

### Match compact mode

The compact mode only is usefull when you are not returning something when match's options end; " _ => () " .

This is because the compact mode will use a combination of "if" and "let" to execute the code only if match.

Example of code;
```rust
fn main(){
    let _variable1 = Some(15);
    // Uncompress mode
    match _variable1 {
        Some(15) => println!("Match. _variable1 is Some(15) type."),
        _ => (),
    };
    
    // Compress mode
    if let Some(15) = _variable1 {
        println!("Match. _variable1 is Some(15) type.");
    };
    
}
```

As you can see, the difference between both is the syntax of compress mode is;
```rust
if let [thing_to_match] = [variable] {
	[code_to_execute_if_match];
};
```

This is more small and you must not have to include "_".
Also you can include "else" sentence here after "if let".

```rust
fn main(){
    let _variable1 = Some(15);
    // Uncompress mode
    match _variable1 {
        Some(15) => println!("Match. _variable1 is Some(15) type."),
        _ => (),
    };
    
    // Compress mode
    if let Some(15) = _variable1 {
        println!("Match. _variable1 is Some(15) type.");
    }
    else {
        println!("No match.");
    };
    
}
```

## Project management - Split features into files, dependencies, packages, libraries and modules

The programs made until here are very simple, but when your project grows you need administrate your code grouping in more easy ways.
In Rust there are many ways of grouping code (from Rust book);
- Packages: A Cargo feature that lets you build, test, and share crates
- Crates: A tree of modules that produces a library or executable
- Modules and use: Let you control the organization, scope, and privacy of paths
- Paths: A way of naming an item, such as a struct, function, or module

Rust (unlike C,C++, etc) have a dependency manager; Cargo. Cargo allows you to indicate specifically with dependency you want/need to use and in which version, the combination of your libraries, binaries and dependencies (this last managed by Cargo) into one same folder/directory is called; project.

Cargo administrate a project with commands;

- cargo new [project_name]

Will create a project into the path where you executed the command.

Into that directory you will see a toml ext file and one "src" folder in which is your "main.rs" rust source code file.

```bash
10:13 pm ~:$ cargo new test1
     Created binary (application) `test1` package


10:14 pm ~:$ exa test1/
Cargo.toml  src


10:14 pm ~:$ exa test1/src/
main.rs
```
Note: exa is a modern replacement of "ls" written in Rust (of course).

As you can see in the first command, cargo interpreted that your new project will be a final program (a binary). When you compile your program will take that name.

Into "Cargo.toml" is specified the dependencies, the version and the information of your program:
```rust
[package]
name = "test1"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

A dependencie is specified in this syntax;

```rust
[dependencie_name] = "[version]"
```

- cargo build 

Will compile the project. If you dont specify nothing more, Cargo will compile as a debug release putting the binary in the folder; [project]/target/debug , if you specify "-\-release" in the command, Cargo will pass arguments to rustc and will not leave debug symbols and another useless things.

## Modules

As we said in the "Theory" section;

As a create is group of functionality, the module is the code group. A module constains one or more functions.

So a create can group many modules as developers want, and each module have related (in the objetive) functions. But there is a very important thing;
 - a module can have two type of code; a private code (in which only the module or module's function will can use it) or public (in which you can call it from your external code).

The syntax/structure of a module is;
```rust
mod [module_name] {
	[pub_or_not] [specific_module] {
		[pub_or_not] fn [function](){
			[functions_code];
		}

		[pub_or_not] fn [function_x] {
			[functions_code];
		}
	}
}
```

1. First you must declare de module's name.
2. Second, If you want a second module, you must declarate if you want it will be public or not. If want it, add "pub" before module name, if not want it, do not add it.
3. Third, the same about public or not but now with functions/structs/implementations or wherever you want.

ShyanJMC Notes:

1. If some module or struct is public, it doesn't mean that their content will be, you must indicate which part of content will be also public (to be used outside the lib.rs file). In functions is not neccesarry (or possible) make internal code public.
2. If two modules have the same return's type, you must specify the module "[module]::[Return]" or create an alias with "as" in "use"'s line.
3. If in your library you are using your module into some function and also you want export it, you must put an "pub use crate::[module]" to allow it use by two or more parts. Ownership things :).
4. If you are using Cargo, with rust "use [module]::[XXXX]" is enough. Cargo will put libs automatically.

Example code;
```rust
mod module_shyanjmc {
    
    struct Data1 {
        name: String,
        date: u64,
    }
    
    pub fn shyanjmc_function(x: String) -> usize {
        let instance1 = Data1 {
            name: x,
            date: 20220212,
        };
        let return1: usize = instance1.name.len();
        return1
    }
    
}

fn main() {
    println!("Hello, world!");
    let return2 = crate::module_shyanjmc::shyanjmc_function( ("Welcome to shyanjmc.com".to_string()) );
    println!("The lenght of welcome message is; {}", return2);
}
```

This code is more interesting, right?

This is all in the same file (main.rs), I will tech you how to split modules into files after, the crate and the main function.

The crate created (the module) is called "module_shyanjmc" and by default is public. Inside it, we have a struct (which as is not public, so only can be used by the rest of module but not from outside the module) Data1 and a public function called "shyanjmc_function" (which takes an argument, works with a struct instance and returns a value). As "shyanjmc_function" is a public function inside "module_shyanjmc", we can call it from outside the module (in this case from main function).

The syntax to call a public function is;

```rust
crate::[parent_module]::[sub_module_if_there_are]::[public_function_enum_or_wharever]
```

There are other ways to use modules (like using "super::XXX") but I consider this; let me supose that you are a good dev and you created a good module with 45 functions (some public and others not) with structs, enums, etc (again; some publics and others not) and with many levels of sub modules, etc. You are programming that excelent lib (crate) and you use "super" to refer something in the same level as your are into the module, Are you sure that you or another dev will keep in mind the complete structure of levels and relationships of your module? Exactly, we are humans and when the code is big, is better writte more words but be sure.

You must specify it even in the same module.

But when you are using the standard library, you are noy using in each function that call way. When you are using functions like; "String::from(XXXXX)" you are using a new crate from standard library with the module "String" and then the public function "from". So, why in the first code we can call directly to String module and functions without the complete syntax? By the "use" keyword.

The "use" keyboard allows you to avoid the use the complete reference and just indicate the parent module and then the fuction which you will call. In Rust's terms when you use the "use" keyword, that module and functions/structs/etc are now valid name in that scope.

This is simple example with the two ways;
```rust
mod module1 {
    pub mod module2 {
        pub fn fninput1(x: String){
            println!("The input's len is; {}", x.len());
        }
    }
}

use crate::module1::module2;

fn main() {
    // Mothod 1 without the "use" 
    crate::module1::module2::fninput1("Hello World".to_string());
    // Method 2 now with "use"
    module2::fninput1("Hello World".to_string());
    
}
```

Using the above example, if instead bring all module2 you just want add to scope "fninput1" in use's lines you can add it (after the module, of course) to avoid specify "module2::" when you want call it.

But, sometimes can there are issues if two modules include the same returns, for example this in Rust Book;
```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {
    // --snip--
}

fn function2() -> io::Result<()> {
    // --snip--
}
```

As you can see, you are obligated to indicate the parent module because both Result's have the same name ('Result', I think there is not requeriment of clarification). But if not want it, you can use "as" keyword in the "use" line which will crate an alias;

Example from Rust Book;
```rust
use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {
    // --snip--
}

fn function2() -> IoResult<()> {
    // --snip--
}
```

We both know that sometimes is not confortable put 35 lines of "use". But, there are a good choice if them belogs to the same module:

```rust
use std::cmp::Ordering;
use std::io;

use std::{cmp::Ordering, io};
```

You can also think that if you import the module you are importing all of them, but not, you are just importing the first public non-submodules (like functions, etc) because of that you can be in this situation;
```rust
use std::io;
use std::io::Write;
```

but you can compress that like in;
```rust
use std::io::{self, Write};
```

But if you want import ALL public sub-things (modules, functions, structs, etc) you can use "*":
```rust
use std::io::*;
```

But my recomendation is; do not use it. Import in specific want you need, you will save memory and bugs.

### Separating modules into files

Others things not but if there are something that is very confortable in Rust is knows automatically when a module is in a external file. But how knows it? Because the module must have the same name that the external file. For example, supouse that we have the project; test1

```bash
03:40 am ~:$ exa -R test1
Cargo.lock  Cargo.toml  src  target

test1/src:
main.rs  shyanjmclib.rs

test1/target:
CACHEDIR.TAG  debug  release
```

As you can see, there are a many files;
- Cargo.lock : This file exist because I already compiled the project before.

- Cargo.toml : This file contains metadata about the project and project's dependencies.

- shyanjmclib.rs :  As the name indicate, this is my library. In this lib I wrote a public asyncronous function to get ATOM coin price from coingecko and if the conection was fine returns Ok. That function is called; "get_atomcoin_price".

- main.rs : Here become the usefull. As "main.rs" is the file which will call my public function is requeriment use the properly calls to import my lib;

```rust
mod shyanjmclib;

use crate::shyanjmclib::get_atomcoin_price;
```

With the first line we are saying that we will use the external module (library) which have name "shyanjmclib" as crate. Rust compiler and Cargo will search a file with the same name that module (and extension .rs of source).

Then, the second line indicate which parts of "shyanjmc" we will import to scope for use. This line is not mandatory, will avoid you a lot of words like we saw before.

So, you must indicate as module the name (with extension) of file in which you have your modules, functions, etc which you want use in your file. You can do this even in files inside directories, spliting a module into many files, but the login is the next;

- Let us supouse that we have "module1.rs" file which we use as library and inside it there are;

```rust
pub mod module_count {
	pub fn get_count() {}
}
```

Whats the new here? See the public fuction; is empty. The empty block code (even without a space) tells to Rust to search a file with the exactly same name and take the function from it. What from where search? Rust will search in a folder a file with the same name that the module ("module1").

```bash
[project_folder]
|-> src
     |-> module1.rs
```

But also there are another option, split a module into another files (I am not fan of split and split and split but you must know that exist the option). To be exactly, you can split in many files and sub directories as you want. The logic is the next;

1. You have your module "module1.rs"
2. Inside "module1.rs" you make public another module (sub-module) without anything inside, just "{}". Rust will search in "src/" for a directory with the same name as parent module ("module1") and then will search for a file (with ".rs" extension) with name of this sub-module.
3. And if you want, you can continue spliting modules into many files as you want.

## Vectors

Vectors are a collection type which use the generic type "T"; Vector\<T\>. 

So a vector is a collection of values which in memory are located next to each other (this is important in low-performance systems because save CPU cycles and time when you know what exactly value need and you know that you must have use it). The values must be the same type.

As types are located next to each other in RAM, Rust must know the type because needs to allocate the exactly size in RAM.

As any another thing in Rust, you can drop it from memory using the ownership rules.

- Vec::new()

Will create a new empty vector.

- vec![x,y,z,a,..]

Will create a vector with values; x,y,z,a and so on. Remember; because have "!" means that is a macro.

- [variable_vector].push(x)

Will update the vector (as variable; [variable_vector]) with a new value "x". The new value will be at least of the collection.

-  [variable_vector].get(x)

Will take the value number in position "x" (remember, the first position is zero) from vector "[variable_vector]". Returns "Option<&T>" and because of that you must consider if returns "Some" or "None" (spoiler; use "match" with this). To compare with specific values you must use "Some\<x\>".

Another option is use arrays; [variable_vector][x]   remember that this option will need also be used as reference (with "&" at start) because use arrays.

Example code;

```rust
    let mut vector1: Vec<i64> = Vec::new();
    vector1.push(1);
    vector1.push(2);
    vector1.push(3);
    vector1.push(4);
    vector1.push(5);
    vector1.push(6);
    
    match vector1.get(0) {
        Some(1) => println!("Value in position 0; {:?}",vector1.get(0)),
        Some(f64) => println!("Value in position 0 is float; {:?}",vector1.get(0)),
        None => println!("Empty value."),
    }
    
    let variablevec = &vector1[0];
    match vector1.get(0) {
        Some(variablevec) => println!("Value in position 0; {:?}",vector1.get(0)),
        Some(f64) => println!("Value in position 0 is float; {:?}",vector1.get(0)),
        None => println!("Empty value."),
    }
```

As you can see, we create a new vector called "vector1" and we update it allocating 6 new values (1,2,3,4,5 and 6). Then we use "match" operator to compare the value in position zero; if is Some(1) (which means the value is; 1) will print the first line.

I used both methods to show you how they work, the result is the same; "Some(1)" and "Some(variablevec)" will be executed because both values taked from the same position (0) are equal to vector's position zero value.

As a vector is a collection of types, you can use subtypes right? Exactly, enums. You can use an enum type with different subtypes;
```rust
enum rarevector {
    Name(String),
    Date(i64),
    Timestamp(String),
}

fn main() {
    let init1 = vec![
        rarevector::Name("JohnDoe".to_string()),
        rarevector::Date(198321),
        rarevector::Timestamp("2022-01-25 13:45:56".to_string()),
    ];
}
```
As you can see, is very similitar to enums.


## Iterations

In Rust (as with Python and others, but not with C,C++ and others) you can use the keywords and syntax; "for ... in ... " to iterate in each value of a collection.

The theory is this; you use a temporal variable (which only exist, or in Rust terms only is in scope, temporally) to store one value at time and execute something, then continue with the next value and execute the code again, and so on to finish the collection.

The syntax is this;
```rust
for [temp_variable] for [variable_to_iterate] {
	[code_to_execute];
}
```

For example;
```rust
    let vector1 = vec![1,2,3,4,5,6,7,8,9,10];
    let mut position = 0;
    for i in vector1 {
        println!("Position; {} have value; {}",position,i);
        position = position +1;
    }
```

In the above example we create a vector called "vector1" with values; 1,2,3,4,5,6,7,8,9 and 10. Then we create a second variable "position" with init value; 0.

Then we start with the iteration; we create a temporal variable called "i" which take the first vector1's value, print in screen the value of it and add 1 to position. So you have this output;

```rust
Position; 0 have value; 1
Position; 1 have value; 2
Position; 2 have value; 3
Position; 3 have value; 4
Position; 4 have value; 5
```

Easy right? :).

And what if you want modify mutable variables? Well, see this Rust book example;

```rust
    let mut v = vec![100, 32, 57];
    for i in &mut v {
        *i += 50;
    }
```

In this example we create a mutable vector called 'v' with values; 100, 32 and 57. In the iteration process the new temporal variable do reference to the mutable vector (because of that must have the "&mut" before the vector's name) and then can change the value.

Take in consideration; in that moment "i" will be pointing internally directly to the mutable variable, so if you change "i" will change the pointed variables' value. As you can see is using the dereferencer operator ("*") which is an advanced concept, I will speak deeply of it later.

Notes;
1. Take in consideration; the variable used in the iteration will be moved to it, so if you want use again let, you must pass it (in the iteration) with "&" in the name.

## Hash Maps
The syntax of a hash map is; "HashMap<K,V>" where stores a mapping of keys of type "K" to values of type "V".

Hash maps are very usefull to keep a track from a key (an ID; K) to a specific value (V).

To use hash maps you must take under scope the collections;
```rust
use std::collections::HashMap;
```

- To create a new hash map;
```rust
let mut [variable_name] = HashMap::new();
```

- To add keys (K) and values (V);
```rust
[variable_name].insert(K,V);
```

- To add a key only if not exist in the hashmap;
```rust
[variable_name].entry(K).or_inseret(V);
```

Notes;
1. You can add many keys as you want.
2. If your key (K) is a string (probably you will do it in the 100% of the cases) you must use; String::from("K") to store properly the key's name.
3. All keys in the HashMaps must be the same type, take it with attention when you create a new hashmap.
4. Like vectors, HashMaps are stored in HEAP.
5. As HashMaps use two types (K and V) you can use "_" in type's place to indicate Rust that they can be any time.
6. Instead of i32,i64 and rest, Strings are owned types, so when you use it in your hashmap, they will be moved to it. Take it under consideration if you do not want have issues with onwership.
7. When you print the values from a hashmap, the "println!" function will start from the last key to the first.
8. If you use "get" to retrieve value from key, take in consideration that is "Option<T>" type, so the return will be the same.
9. If you want overwrite an existing value, add a new value with the same key name, Rust will overwrite in memory.


Taking in consideration all this, you should easily understand this code;

```rust
use std::collections::HashMap;

fn main() {
    let mut init1 = HashMap::new();
    let key1 = String::from("Lovecraft");
    let value = 35976;
    let key2 = String::from("King");
    let value2 = 38475;
    
    init1.insert(key1,value);
    init1.insert(key2,value2);
    
    for (key,value) in &init1 {
        println!("Key; {}, Value: {}",key,value);
    }
    
    let value3 = init1.get("King");
    println!("Value for King key; {:?}",value3);
}
```

With above code we bring under scope the HashMap module. Then we create a new hashmap empty variable, a string variable, a integer variable, a second string variable and a second integer variable.

Then we indicate to Rust to insert into the hashmap first; the key "key1" variable and value "value" variable. Then we repeat but with "key2" and "value2". After that, we start with an iteration in which we create two temporal variables; "key" and "value" which each one will take the hashmap each time of the iteration. Then we print them values for each iteration.

At least, we get the value from key "King" and we print it. Remember as the return is "Option" we must specify "{:?}" to indicate println macro do not format the output.

At this point we can go with some advanced things about Rust and pointers returned from functions. To explain it, I will create a program for Rsut book chapter 08 first exercise;

- Given a list of integers, use a vector and return the median (when sorted, the value in the middle position) and mode (the value that occurs most often; a hash map will be helpful here) of the list.

```rust
use std::collections::HashMap;

fn medium_in_vector(mut init1: Vec<u64>) -> Vec<u64> {
    let mut cont = 0;
    // Sort the vector
    init1.sort();
    
    println!("The medium of sorted vector is; {:?}", init1.get(20/2));
    init1
}

fn number_repeted(mut init1: Vec<u64>, mut init2: HashMap<u64,u64>) {
    let mut cont = 0;
    init1.sort();
    
    cont =0;
    while cont < 20 {
        for j in init1.get(cont){
            let count = init2.entry(*j).or_insert(0);
            *count += 1;
        }
        cont +=1;
    }
    
    // Print the complete HashMap
    println!("{:?}",init2)
}

fn main() {
    let mut init1 = Vec::new();
    let mut init2 = HashMap::new();
    let mut cont = 0;
    
    while cont < 20 {
        init1.push(cont);
        cont= cont+1;
    }
    
    init1.push(3);

    init1 = medium_in_vector(init1);
    number_repeted(init1,init2);

}
```

First we create one new vector ('init1') and a new hashmap ('init2') and at least, a temporal variable for count (with init at zero).

Then we start a bucle in which while "cont" value is less than 20; will put into the hashmap the cont's value and then increase cont's value by one.

Then we add value; 3 to hash map.

Then we call "medium_in_vector" with arguments; "init1" and storing the returns in "init1". Is that rare no? Let me explain; as "init1" is a vector that we pass it to be sorted, we are taking the ownership of that variable, so if we want return it (the ownership) to "main" function to keep it valid in memory we store it in itself, so we do not need change the rest of program (or create a new variable) because we will not use the unsorted vector.

The "medium_in_vector" sort the mutable vector ('init1') using the object ".sort()" and then print the medium position's value. At least 'main' calls "number_repeted" with arguments; "init1" and "init2" which sort the vector (in the case that the first function did not it properly) and then use the hashmap ('init2') to keep a count of values. And there are something very important that you must understand about that expression in the "while" bucle; "j" point to "cont" position. So, with "entry" detects if "j" position exist, "or_insert" returns a pointer to "j" value's position, so if not exist "j" position will asign "0" but if exist as returns a pointer to "j" value's position and is assigned to "count" variable, if you modify that variable (count) you are changing the "j" position value.

With that you can keep a track of each value and update it into the hashmap if already exist.

## Error handling
When you are programming, sometimes you need handle errors. For example; if the file is not detected or remote port is closed.

In Rust there are two types of issues; unrecoverable (RAM corruption, etc) and recoverable (file not found, closed connection, etc). Rust can call "panic!" automatically when a bug happens (for example; if you try to get RAM information from where not exist).

- panic!("XXXXXXX");

"panic!" is a macro (like "println!") which prints the "XXXXXX" message to Cargo or user when the developer founds a situation in which belives it as an unrecoverable issue for the program. Internally, "panic!" macro makes the "unwinding" which means; rust will freeze the program, clean up the memory data for each instruction and then kill the program. This is the most safe way to kill a program, but if you want use the unsafe rust features you must add into Cargo.toml file;

```rust
[profile.release]
panic = 'abort'
```

That indicates not clean the RAM memory and close inmediattly, but take in consideration that program0s memory will be not cleaned so the OS must clean up, or your program's data will be accesible to others. My recomendation is not use this unless you really really know what you do.

- Result<T,E>

In Rust the recoverable errors can be used with enum 'Result' which returns two possible; "Ok(T)" and "Err(E)". As you probably know "T" represents the "Ok" returns types and "E" the "Err" returns types because both are generics.

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

One simple way to know if some function returns 'Result' is search the documentation, or another way is store the result as another type than 'Result<T,E>' so the compiler will let you know if is other. So if the functions ended well will returns "Ok(T)" and if was a recoverable error will return "Err(E)". For example this code from Rust book;

```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?}", error),
    };
}
```

We import the filesystem module and then the submodule "File". Then we create a variable which will store the returns of "open" function and then we compare it; if "f" values match with "Ok(file)" ('file' is the "T" specified in the "open" function which is the file opened. Because of that you not see it into the primary code. Always you must see what code return's specifically.) in which case will return the file to be stored into "f" again, and if not, will match with "Err(error)" ('error' is the "E" specified in the "open" function. Again, you must see the documentation to know everything) and execute "panic!" to close safety the program.

How we know that will not match with "Some(X)" for example? Because in standard's library documentation is specified that will return "Result<File, error>".

But there are something very very important about the "Err" return; can be a lot of things. So, you can always match to specific things and take the properly actions. For the "E" generic you can use ".kind" object (remember "E" is the variables name of Err's return) with this example also from Rust book;

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {:?}", e),
            },
            other_error => {
                panic!("Problem opening the file: {:?}", other_error)
            }
        },
    };
}
```

That code will import from standard crate, the public module for input output and the public sub module "ErrorKind". It allows to analyze the "Err(e)" returned by some function. The program starts trying to open "hello.txt" file and store the returns into "f" variable (which is Option<T> type), and then start to match "f", if the value is "Ok(file)" returns "file" variable, but if f's values is "Err(error)" will match using "kind" object (which returns the corresponding ErrorKind for this error) and start to compare, if the problem was the file doesn't exist, try to create it (with; "File::create") and math the returns again in case it fails. If the issue was other (represented as "other_error") will panic and close safety the program. In both cases, if matches properly, will return Ok's variables to "f" shadowing the original value.

Those behaviour can be done because "io::Error" is a struct inside Rust standard library and ".kind" is provided as a method (implementation). In specific ":io::ErrorKind" is an enum and each variant indicate the specific issue (like "ErrorKind::NotFound" for file operations).

"Match" and the comparations is the long way to handle recoverable issues. There are another method you can use ".unwrap_or_else" in combination with "|error|" :

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let f = File::open("hello.txt").unwrap_or_else(|error| {
        if error.kind() == ErrorKind::NotFound {
            File::create("hello.txt").unwrap_or_else(|error| {
                panic!("Problem creating the file: {:?}", error);
            })
        } else {
            panic!("Problem opening the file: {:?}", error);
        }
    });
}
```

The above code do;
1. Import from standard library two modules; "fs" (file system) and "io" (input/output) with respectives submodules; "File" (from "fs") and "ErrorKind" (from "io").
2. Define "f" variable to open (File::open()) the file (hello.txt). 
3. If that code fails, " unwrap_or_else" will check the error's kind (error.kind, the variable name is because in unwrap's line is specified it as; |error|) is equal to file not found (ErrorKind::NotFound).
4. If is equal, will create the file (File::create) and will check again if fails (" unwrap_or_else( |error| { " ), if failed will panic the program.
5. If is not equal to file not found will panic.


- Result as returns

What about if you want use Result's types as returns? Easy;

Syntax;
```rust
fn [function] -> Result<[OKs_types],[Err_types]> {
```

For example;
```rust
fn new(args: &[String]) -> Result<Config, &'static str> {
```

The above signature/header means that the binary take one one of type 'String', and returns Ok(Config) or Err(&'static str) which means that the type is "str" and lifetime "static".


- unwrap_or_else

The "unwrap_or_else" method is in the standar library in the "option" and "result" modules, in this case we use it for "result". In both modules "unwrap_or_else" will return the contained OK's values or will execute the contained code from the closures, you can store the specific error into a variable (in the code example "error") specifing it between "| |".

The objective of "unwrap_or_else" is provide a return in case of error. So in case of first assesment returns an error to "unwrap_or_else", will execute the code. So we have;

```rust
operation_x.unwrap_or_else( operation_y );
```

if "operation_x" fails and return some "Err(x)" so will be execute "operation_y".

"unwrap_or_else" extract the content from "Ok(XXXX)" and "Err(XXXXX)" to work properly (panic in case of "Err" or store the value from "Ok").

You get the same behaviour with;
```rust
if let Err(e) = [function_with_return_Err(e)] {
	[code_to_execute]
}
```

- unwrap

The "unwrap" method also lives in "option" and "result" modules. 

```rust
operation_x.unwrap();
```

if "option_x" fails, unwrap fill panic the program.

"unwrap" extract the content from "Ok(XXXX)" and "Err(XXXXX)" to work properly (panic in case of "Err" or store the value from "Ok").

- expect

The "expect" method works in the same way than "unwrap" but having the useful option to show a final message before panic.

```rust
operation_x.expect("Message to show when the program panic.");
```

As "unwrap", extract the content from "Ok(XXXX)" and "Err(XXXXX)" to work properly (panic in case of "Err" or store the value from "Ok") but with specific message.

Notes:
- When you create a function which opterations can fail is a very good idea put as returns a "Result<T,E>", that is called; "propagating errors".

For example;

```rust
use std::fs::File;
use std::io::{self, Read};

fn in_file(xfile: String) -> Result<String,io::Error> {
    let mut r1 = File::open(xfile).expect("File not found.");
    let mut buffer = String::new();

    match r1.read_to_string(&mut buffer) {
        Ok(_) => Ok(buffer),
        Err(e) => Err(e),
    }
}

fn main() {
    let input = String::from("file.txt");
    let input2 = in_file(input);

    println!("{:?}",input2);
}
```

The above code;
- Import from "fs" module, the submodule "File" and from the module, the submodule "Read" and itself.
- Create a new function "in_file" with String argument and return "Result<String, io::Error>" so if the returns are ok will be a string, if there was an issue the type will be "io::Error". We use "io::Error" because the error when you access a file can be a lot of things; file system issues, file not found, device damaged, etc.
- Create a mutable variable "r1" which open a file (File::open) with name inside string variable "xfile". If the operation fails will print "File not found" and panic the program (remember the behaviour of "expect").
- Create a mutable string variable "buffer".
- Pass the file variable "r1" to "read_to_string" which copy all content to "buffer" and then "match" compare the returns. If was any type of "Ok" (that means the underscore; _, remember it) will return as String the buffer's data, if is an Err, will return it with the issue. "E" in this case is not refered as a variable, is a generic type.
- Has specified "input" string variable with value "file.txt" which is the same that is passed to our function.
- And at least, we print the "in_file" return. If everything was right, will show you the content.

There are another way to handle errors; "?".

- "?" 

The "?" symbol, indicate to rust to return "Ok(X)" that can be used in the same function or "Err(X)". This make "?" only useful for types that can be returned in any time by the function, because; "only works with it returns and will returns it", that means you can not use it in "main" function, why? Because "main" returns "()" not "Result<T,E>" or wherever. 

Tacking back your example, the Result Err will be returned as function return, and Result Ok will be returned inside the same function. So, taking a second version of previusly code;

```rust
use std::fs::File;
use std::io::{self, Read};

fn search_in_file(xfile: String) -> Result<String,io::Error> {
    let mut r1 = File::open(xfile)?;
    let mut buffer = String::new();

    r1.read_to_string(&mut buffer)?;
    Ok(buffer)
}

fn main() {
    let input = String::from("file.txt");
    let input2 = search_in_file(input);

    println!("{:?}",input2);
}
```

That code do the same thing that the first code but now we replaced the "expect" and "match" with "?". So in this code if open properly the file, the return will be assigned to "r1" but if there was en error the function "search_in_file" will end (panic) and the "Err(X)" returned to "main". The same for "read_to_string". But, there are another way to even compress more;

```rust
use std::fs;
use std::io::{self, Read};

fn search_in_file(xfile: String) -> Result<String,io::Error> {
    fs::read_to_string(xfile)
}

fn main() {
    let input = String::from("file.txt");
    let input2 = search_in_file(input);

    println!("{:?}",input2);
}
```

Why this version of "search_in_file" function is better?
1. We are saving one variable, which in memory terms is better.
2. Is a waste of code just put "fs::read_to_string" in a separate function but I keeped to show you the change.
3. As "fs::read_to_string" only returns the file's data, is a good choice the use of "Result<String,io::Error>" because still the file's data is a String.
4. Taking in consideration the point 3, you can even delete "input2" and put the read function into "println!".

## Traits, Generics and Lifetime

- Generics

In long way; A generic type is a common way to indicate Rust that the type/function can be anyone of primitive types (integers, floats, chars, strings, etc). A generic type is a polymorphism ('many' 'phorms') type. We used before (Options and Results), and when two or more generic types have the same generic name, they will respond to the same type when it is defined. With that you can change many of the behaviour.

In short way; we use generics to create definitions.

Note; the convention is to use "T" as main generic, but you can use wherever you want.

Example;

```rust
fn search_in_file<T> (xfile: <T>) -> <T>{
```

With above example we are defining;
1. That the generic type "T" is in the scope of "search_in_file" function.
2. That as argument, there is a variable called "xfile" with generic type "T"
3. That as return, there is a generic type "T"

So, when the "search_in_file" function is called if "xfile" is "char", the return and all "T" generics inside the code will be taked as "char" types. If is "u32" the same; the return and all "T" generics inside the code will be it type, and so on.

Here an example about how to use with an struct, her implementation and the call:

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```
Above another example, if "x" or "y" is "u32" the others too, if is "float" the others too. With that you can control the types depending of the scenario. Then, the implementation specify the generic which will modify (must match with the variable's generic) and at least is called by "main".

Note; the generic's specifiction after "impl" indicates the declaration to use into it is a generic and not a type.

But what about if we want use two generics? Easy; add another character

```rust
struct Point<T, U> {
    x: T,
    y: U,
}
```

Above code indicate two generics, that allows dev to use one, two or more generic types.

In nums we used before in Options, as we said before;

```rust
enum Option<T> {
    Some(T),
    None,
}
```

```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Rust implements the generics in some way that if in the code is specified the type, you will not have performance costs.


- Traits

A trait in Rust describe a common way and behaviour between many types. For example; you want that a specific function/method can only be used with Strings and Str and not with the others types, how do you limit it? With Traits, in which you specific for what types are implemented and only those types can use them as methods. Maybe you can think that is better put argument's types but remember that a variable can have only a type, while a trait can be implemented to be used (as method) as many types dev wants.

First we need create the Trait, in the creation step you can define the functions or just the signature:

```rust
pub trait [Trait_name]{
	fn [function_name](&self, [Arguments]);
	fn [function_name2](&self, [Arguments]){
		[code]
	}
}
```
When the Trait's function do not have code (just the signature) must be finished with semicolon (;). When Trait's function have code, the code and the function's end must not have semicolon (;). The function with code will be the default behaviour in all implementation, the rest of functions (which not have code) must be completed with code inside the implementation.

Then we need implement (a clue) it (the trait) into a type. Traits are implemented on structs so self references (to structs) must be used inside "impl" step. This is an example from my shyanjmclib.rs file:
```rust
fn coinvalue(x: Coins ) {
    // format! macro outputs as strings
    if (x.blockchain == "cosmos-hub"){
        let urip = format!("https://www.coingecko.com/en/coins/cosmos\n");
        println!("{}",urip);
    }
    else {
        println!("No hub detected.");
    }
}

pub struct Coins {
    pub name: String,
    pub blockchain: String,
    pub cosmoshub: bool,
}

pub trait GetPrice {
    fn price(self); 
}

impl GetPrice for Coins {
    fn price(self)  {
        println!("The coin;  {} from blockchain; {} has an actual value of;",self.name,self.blockchain); 
        // if I pass directly the string "blockchain" the argument will be string, not Coins struct
        coinvalue(self);
    }
}

```

In the above code, we;
1. Create a public struct called "Coins" with "name", "blockchain" and "cosmoshub" public variables, of type; String, String and bool.
2. Create a public trait with signature of function "price".
3. Implement that trait for Coins struct specifing the behaviour, why not use it as the default into trait creation directly into point 2? Well, see the coinvalue's function signature. There you will see "x: Coins" so if you call it from the "pub trait GetPrice" section you will not respect the rule "references and use of structs must be done from impl step". But in the default behaviour you can call another trait's functions. 

Then into main.rs we import the file (with "mod ...") and import specific things (like Coins structure and GetPrice trait). With the import into scope of "GetPrice" trait we are also importing "coinvalue" because was declareted into the trait's scope.

```rust
mod shyanjmclib;

use crate::shyanjmclib::Coins;
use crate::shyanjmclib::GetPrice;

fn main() {
    // get_atomcoin_price();
    let ccoin = Coins {
        name: String::from("cosmos"),
        blockchain: String::from("cosmos-hub"),
        cosmoshub: true,
    };

    ccoin.price();
}
```

The complete program will check if ccoin.blockchain is equal to "cosmos-hub" to return the URI in which information about price is stored, if not will return "no hub detected". The trait limits "price" method to only be used by "Coins" type structs.

Also you can indicate that only implemented types in a specific trait can be used as function's arguments. For example, see this function's signature;

```rust
pub fn notify(item1: &impl Summary, item2: &impl Summary) {
```

It indicates that only variables with traits "Summary" implemented in their types can be used as arguments.

You can also use Generics as aliases. The before signature can be rewrited in this (I did put both so you can see quickly the difference);
```rust
pub fn notify(item1: &impl Summary, item2: &impl Summary) {

pub fn notify<T: Summary>(intem1: &T, item2: &T){
```

As you can see, is a very short way.

And what if you have the situation in which you want that maybe the same argument can be implemented in two or more traits? Easy, use "+". Here two options;
```rust
pub fn notify(item: &(impl Summary + Display)) {

pub fn notify<T: Summary + Display>(item: &T) {
```

or even use two or more generics in the signature as traits types (from Rust Book);
```rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {

// or as second way to write it:

fn some_function<T, U>(t: &T, u: &U) -> i32
    where T: Display + Clone,
          U: Clone + Debug
{
```

and also you can specify implemented traits as returns (from Rust Book);
```
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("horse_ebooks"),
        content: String::from(
            "of course, as you probably already know, people",
        ),
        reply: false,
        retweet: false,
    }
}
```

The above function will return the struct "Tweet" implemented into "Summary" trait before. The ability to return specific types implemented in specific traits is very useful, but remember that only one type implemented is allowed.

Restricting more;

Take this example from Rust Book

```rust
fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
```

The above signature will limit the argument's type to only which have PartialOrd and Copy traits implemented. "PartialOrd" (from  std::cmp::PartialOrd ) is a Trait  for values that can be compared for a sort-order like vectors. "Copy" is a trait used (as we saw in Ownership section) when the type's data size in heap/ram is known by the compiler and can copy the data to a function as argument.

Most of methods are implemented in "Display" for example; "to_string" (see; https://doc.rust-lang.org/src/alloc/string.rs.html#2388-2402 ) so will fail if some type is not implemented in Display. Types like u32,u64,f64,char,Strings are in Display trait but maybe you can have issues with structs and others.

- Lifetime

This is a sub-term of ownership. In specific the lifetime allows you to customize how ownership works, not all but yes some. 

The lifetime is a way to know and determinate how valid is the data's ownership. As standard we name each one with; ' and then the name (starting from "a").

From Rust book;

```rust
    {
        let r;                // ---------+-- 'a
                              //          |
        {                     //          |
            let x = 5;        // -+-- 'b  |
            r = &x;           //  |       |
        }                     // -+       |
                              //          |
        println!("r: {}", r); //          |
    }                         // ---------+
```

In the above example there are two lifetimes in the code ownership; 'a (the main lifetime) and 'b (the sub lifetime). The variable "r" is in 'a lifetime while "x" variable is in 'b.

In the example when we enter into 'b lifetime "x" variable data is valid and "r" take "x" as value by reference but then 'b ends and "x" is not valid (remember, was in 'b lifetime) now, so "r" will be pointing to a void value and Rust will not allow you do it and the code will not compile it. If you want that "x" will be still available after 'b ends you must indicate that it is under the 'a control. It is detailed in function's signature.

Signature syntax (I use norsk character; Æ as character variable in reference can be any);
```rust
fn [function_name]<'Æ> ([variable_n]: [&]'Æ [type]) -> [&]'Æ [type] {
```

If you must have include more lifetimes just separate them with "," inside "<>".

Take very under considerations this rules; 
1. If you declareted one argument's lifetime you must do it again for the rest. No argument must be without her lifetime specified.
2. The second rule is if there is exactly one input lifetime parameter, that lifetime is assigned to all output lifetime parameters.
3. The third rule is if there are multiple input lifetime parameters, but one of them is &self or &mut self because this is a method, the lifetime of self is assigned to all output lifetime parameters.
4. If in an impl there is only "self" in function, is not required put lifetimes in functions. If there are more arguments in the function you should include lifetimes.

And in any variable (in functions and structs also);
```rust
[variable_name]: [&]'Æ [type]
```

And in impl;
```rust
impl <'Æ> [implementation_name]<'Æ>{
```

In a struct the lifetime is referenced after the struct's name in the same way than in function. If you use references in structs, you should include lifetimes (mainly with; 'a) because remember one of most important things about ownership; when you use "{}" the ownership of data change, so take care of references here because you will find a very complicated issues to fix if you mess up.

When you put lifetimes in signature's argumens are called; "input lifetimes". And when you put lifetimes in signature's returns are called; "output lifetimes".

Sometimes you can have situations in which Rust can know the lifetime of each argument and sometimes when is not clear you will must insert them manually. When Rust can do it automatically is becuase is applying the "elision rules" (are in compiler's code).

As Rust book indicate;
> Remember, when we specify the lifetime parameters in this function signature, we’re not changing the lifetimes of any values passed in or returned. Rather, we’re specifying that the borrow checker should reject any values that don’t adhere to these constraints....Ultimately, lifetime syntax is about connecting the lifetimes of various parameters and return values of functions. Once they’re connected, Rust has enough information to allow memory-safe operations and disallow operations that would create dangling pointers or otherwise violate memory safety.

Until now you do not know it, but in every function Rust checks the lifetime of each parameter/argument. Instead of be obligated to write every parameter's/argument's lifetime, you are blessed that elision rules exist.

Special case;

There is a special lifetime called; 'static which indicate to Rust that the stored data must be valid and in scope until program finish. But knowing the human, try to fix issues and not use this.

You can combinate inside the same "<>" generics and lifetimes without issues. This is because both are types of generics.

With this you should write code without many repetitions and that works in different scenarios with different data.

## Write tests and use it

You do not need to execute the program with respective arguments after each compilation, also, how you can test manually a function if you can not call it directly? Rust and Cargo have a configuration for it; tests. When you execute a test, Cargo will execute the code and will inform you if was successful.

The tests must be inside; "lib.rs" or "main.rs"

Syntax;
```rust
#[cfg(test)]
mod tests {
	#[test]
	fn [function_name] {
		[code];
	}
	#[test]
	fn [function_n] {
		[code];
	}
}
```

Then you just execute; "cargo test". For each test function Cargo will inform if was "ok" or "FAILED".

Notes;
- Is a very good choice use; "assert!", "assert_eq!", "assert_ne!" nad "panic!" macros. 
- For each test function must be before an; "#[test]".
- "panic!" macro allows you to specify a custom error message.
- You can call another functions, wherever if are public or not. If you will test private functions (functions without the "pub fn" ) you must bring them into scope with "use supper::*" before the "#[test]" section but inside the "mod tests" section.
- If you want execute more than one test at the same time, put Cargo's arguments; " -- --test-threads=X" where X is the threads numbers.
- If you want put binary's arguments put after; "cargo test --" for example; "cargo test -- --help" will pass "--help" to the final binary.

If you want execute one specific test or specifics tests do; "cargo test XXXX" where;
- XXXX is the test name
- XXXX is a string where exist in many test names.

If you do not want execute some test unless is specific called by you with "cargo test XXXX" you must add after "#[test]" the "#[ignore]". But if you want execute all ignored tests (instead put names one by one) you can call cargo test with "-- --ignored" and if you want execute ALL tests (included ignored) put; "-- --include-ignored".

But also as with files, we can split functions into files, also with tests. Just create a "tests" folder inside your Cargo's project src folder and bring them into scope with "use adder". And you can call just specific tests from specific file with "cargo test --test [test_file_name]" and with it, Cargo will just execute tests functions specified into your code where they are from [test_file_name].

If your test functions are not in you "mod tests {}" sectuions, Cargo will execute them without arguments, if they are Cargo will execute them based in your code. But if there is some reason why you dont want to call specific functions in file inside "tests" folder, you need create a new folder (inside "tests" directory) and then inside it name the file as "mod.rs", with it Rust understands that file is not an integration test (remember bring it under scope with "mod [folder_name]").

And remember; binary crates can not have tests functions. Why? Because is not secure and is not logic compile a final binary with "test" code inside (there is something very very powerfull called; reverse engeneering), just the libraries crates can have test functions.

## Intesresting crates and functions
Here I will list insteresting crates and functions which you can use in your programs. Some of this functions you will need all knowledge you have at now. As rustcean (a rust developper) you must read always the documentation, why? Because is;

1. The official source of knowledge of something.
2. The most technical source of something.

Because of that, here I will link you to the Rust official source. The main index is;
   - https://doc.rust-lang.org/std/index.html 

The "std::str" module is imported by default.

Said it, here the most (in my opinion) interesting and must-know rust modules. You can import under scope them with "use [module]";

1. Module; "std::arch"
This module have specific functions and macros to use to identify CPU, CPU's architecture and allows you to detect if some feature is enabled into the architecture (for example; lse, lse2, rdm, rcpc, sve2, sve2-sha3, sha2, sha3, sm4, etc).

   - https://doc.rust-lang.org/std/arch/index.html 

2. Module; "std::env"
This module allows you to inspect and manipulate process' environment. Like process' arguments, current directory, process' current directory (where the executable is allocated), the home directory, PATH environment, set and remove environment variables, etc.

   - https://doc.rust-lang.org/std/env/index.html

Is recomended use "collect" iterator to store arguments into a Vec<String> variable, then you can access each of them with arrays over that variable.

For example, to collect arguments;
```rust
use std::env;

fn main() {
    let arguments: Vec<String> = env::args().collect();
    println!("{:?}", arguments);

    let environment_variables = env::var("[ENVIRONMENT_VARIABLE]");
}
```
Then you can access each element in "arguments" using arrays. After that, the program check if [ENVIRONMENT_VARIABLE] environment variable exist in the system and store the value into "environment_variables" var.

3. Module; "std::fmt"
This module allows you with many utilities to format and print strings in many ways (we used 'format!' macro from this module before).

   - https://doc.rust-lang.org/std/fmt/index.html 

4. Module; "std::vec"
This module allows you to use and works with vectors.
   
    - https://doc.rust-lang.org/std/vec/index.html

5. Module; "std::fs"
This module allows you to do basic operations in the local filesystem (like; copy file, is there a directory?, create dir/s, hard links, file metadata, read file/directory, delete directory, rename file or directory, set permissions, write file, etc).

    - https://doc.rust-lang.org/std/fs/index.html

For example (from Rust book);
```rust
use std::env;
use std::fs;

fn main() {
    // --snip--
    println!("In file {}", filename);

    let contents = fs::read_to_string(filename)
        .expect("Something went wrong reading the file");

    println!("With text:\n{}", contents);
}
```

6. Module; "std::os"
Specifics sub-modules and functions for systems like; Linux, Unix, Windows, WebAssembly and RAW.

    - https://doc.rust-lang.org/std/os/index.html

7. Module; "std::io"
This module allows you to do input and output operations.

    - https://doc.rust-lang.org/std/io/index.html

8. Module; "std::net"
This module allows you to do primitives operations for TCP and UDP communications as well as IP and sockets addresses (like; listen in TCP, open UDP sockets, configure IPv4, IPv6 or borth, etc).

    - https://doc.rust-lang.org/std/net/index.html

9. Module; "std::string"
As we work before in this webpage, this module allows you to work with strings.

    - https://doc.rust-lang.org/std/string/index.html

For example;
```rust
use std::string;

fn main() {
    let strings = "hello world".to_string();
    println!("{}", strings);
}
```

10. Module; "std::time"
This module allows you to work with the time (for example; how many seconds/nanos/etc passed from X moment, etc).

    - https://doc.rust-lang.org/std/time/index.html

11. Module; "std::process"
This module allows you to work with processes (like; spawning child processes from local system, etc).

    - https://doc.rust-lang.org/std/process/index.html

One thing that I recommend to do with thos module is avoid "panic!" when is not a requeriment and use "unwrap_or_else( |err| { [code] });" to handle error with nice and pretty message and then exit the process with;

```rust
process::exit(1)
```

In that case "1" will be the OS stored value (in Linux you can see it with bash command; "$?").



12. Module; "std::iter"
This module allows you to work with iterations over collections.

    - https://doc.rust-lang.org/std/iter/index.html

Special mention to "collect" method (https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.collect) which create a vector from the iteration and "iter" (https://doc.rust-lang.org/std/iter/trait.Iterator.html#tymethod.next) method which iterate over a collection and return each element every time is called (you can go manually to the next element with "next()" method).

13. Module; "std::result"
This module allows you to with Results types; check if the returns is Err (returns True if is), etc.

    - https://doc.rust-lang.org/std/result/index.html

## Closures
The closures is a method to use a function inside just an specific context without expose it to outside.

For example, we have this code;
```rust
use std::io;

fn work_from_home(employee_id: String){
    let top: String = 200.to_string();
    println!("Calculating if employee can work from home or not...");
    if employee_id > top {
        println!("Classified employee, can not work from home because manage critical information.");
    }
}

fn main() {
    println!("Hello, world!\nInsert employee id, remember must have an integer; ");
    let mut buffer = String::new();
    std::io::stdin().read_line(&mut buffer).expect("Fail to read stdin.");
    let buffer2_result = work_from_home(buffer);
}
```

As you can see we are call the function "work_from_home" and store the result in "buffer2_result" but, what about if we want that just the code inside "main" can call that code? We can use 'closures'. The syntax is;

```rust
let [variable] = | [argument_1],[argument_n] | -> [return_type] {
	[code];
	[return_to_store_in_variable]
};
```

Take in consideration this; the [variable] is to store the code inside delimited memory under the scope of specific context (the function where is located inside) is not where the return will be stored, take in consideration it. Also you can not print directly a closure in "println!" or similiar, because even with "Debug" the 'closure' trait is not implemented.

The first code can be refactored in;
```rust
fn main() {
    println!("Hello, world!\nInsert employee id, remember must have an integer; ");
    let mut buffer = String::new();
    std::io::stdin().read_line(&mut buffer).expect("Fail to read stdin.");

    let buffer2_result = | buffer: String | -> u64 {
        let top: String = 200.to_string();
        println!("Calculating if employee can work from home or not...");
        if buffer >= top {
            println!("Classified employee, can not work from home because manage critical information.");
            1
        }
        else {
            println!("The employee can work from home.");
            0
        }
    };

    let _return = buffer2_result(buffer);
    println!("{}",_return);

}
```

With above code the code of "work_from_home" function (in the first code) is stored now in "buffer2_result" and that code can be only executed from the rest of code inside "main" (because is the function where lives). The closure's signature specify that the argument is String type and return is u64 type. At least, we call it, storing the result in "_return" variable and printing properly.

Instead like in functions, in closures is not necessary specifie the returns/arguments type but I highly recommend use them because if Rust can not infer the type, will take them as "Strings".

As a closure is use a variable as container for instructions, this can be applied also in structs, but now we must use Traits and generics to indicate Rust that every struct's instance can use them:

```rust
struct [Name]<Æ>
where
	Æ: Fn([TYPE]) -> [TYPE],
{
	[variable_closure]: Æ.
	[variable_x]: [Type],
}
```

With above example, we declarate a struct called [Name] with generic "Æ"
