202209021649

Status: #info 
Tags: #rust #notes #rust/basics

# The Rust Programming Language 

Bookmark - [Bookmark](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html)

### 1.3 Hello, Cargo

Cargo is a combination of the build system and package manager. 

Use Cargo to create new Rust programs.

```sh
cargo new project_name
```

> NOTE: Cargo automatically initializes a git repo. 

#### Cargo Commands
#rust/cargo/commands

```sh
# Build the project (executable stored in target/debug/project_name)
cargo build

# Build and run the project
cargo run

# Build without producing executable
cargo check
```

Building for release is different than development. Further optimizations are created in the release build.

```sh
# Build release (executable in target/release/project_name)
cargo build --release
```

## Programming a Guessing Game
#rust/basics

`use` us rge import keyword for libraries and modules. Nested imports use double colon syntax. Example, `use std::io`.

> NOTE: functions ending with a bang ("!") are called macros and have different behavior than functions.

By default, variables are immutable. Use the `mut` keyword to declare a variable as mutable.

```rust
let apples = 5; // immutable
let mut bananas = 5; // mutable
```

`&` indicates a *reference* in rust, which means that it allows multiple areas of the code to access a single piece of data without copying the data into memory multiple times.  Even if the referenced variable is mutable, the reference itself is not. Therefore, it's required to make it mutable explicitly:

```rust
# Mutable reference
io::stdin().read_line(&mut guess)
```

Rust will automatically detect certain uncaught errors for you and enforce exception handling. For example:

```sh
$ cargo build Compiling guessing_game v0.1.0 (file:///projects/guessing_game) warning: unused `Result` that must be used --> src/main.rs:10:5 | 10 | io::stdin().read_line(&mut guess); | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ | = note: `#[warn(unused_must_use)]` on by default = note: this `Result` may be an `Err` variant, which should be handled warning: `guessing_game` (bin "guessing_game") generated 1 warning Finished dev [unoptimized + debuginfo] target(s) in 0.59s
```

### Importing Packages/Libraries
#rust/cargo/commands 

Add dependencies in the cargo.toml file explicitly.

Cargo knows when your dependencies have or haven't changed, leading to faster builds between `src` code changes.

```sh
# Updates the Cargo.lock file with latest versions
cargo update
```

Imports can be "Scoped" to where you still use the main library name but it only loads a subsect of methods. These are called *Traits*. For example:

```rust
use rand::Rng
// Loads range methods ON rand module
let secret_number = rand::thread_rng().gen_range(1..=100);
```

> Note: You won’t just know which traits to use and which methods and functions to call from a crate, so each crate has documentation with instructions for using it. Another neat feature of Cargo is that running the `cargo doc --open` command will build documentation provided by all of your dependencies locally and open it in your browser. If you’re interested in other functionality in the `rand` crate, for example, run `cargo doc --open` and click `rand` in the sidebar on the left.

The `match` expression has different *arms* which are patterns it tries to match against. There are different types of *arms* depending on what values attempt to be matched.

When using `parse()` method, Rust infers the type based on the annotation of the variable it's being set to. For example:

```rust
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

### Handling invalid inputs

Different functions in rust essentially have a callback that can be used to map the `Ok(result)` and `Err(er)` returns. Syntactically, it's similar to a function map.

```rust
// INCLUDE MATCH KEYWORD
let guess: u32 = match guess.trim().parse() { 
	Ok(num) => num, 
	Err(_) => continue, 
};
```

## Variables and Mutability

Convention in rust uses upcase and underscore in constant names. Constants are **always** immutable (`const MY_CONSTANT: u32 = 60 * 60 * 3;`). What's important to is that this constant value is calculated at build time, meaning that you can write out the expression in a more human-readable format without it affecting the programs performance with added operations.

When *shadowing* a variable (re-assigning its value to the same name on a non-mutable variable), you must restate the `let` keyword:

```rust
let x = 5;
let x = x + 1;
```

> NOTE: A shadowed variable can also have different values between two scopes and the same name.

## Data Types

In statically types languages all variables types must be known at compile time.

**Scalar Types** - A _scalar_ type represents a single value. Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters.

**Integer Types in Rust**

> NOTE: _Signed_ and _unsigned_ refer to whether it’s possible for the number to be negative (has a SIGN or doesn't).

Length | Signed | Unsigned
8-bit | i8 | u8
16-bit |	 i16 |	u16
32-bit	| i32 | u32
64-bit	| i64	| u64
128-bit |	i128 | u128
arch	| isize | usize

**Char Types**

```rust
fn main() {     
	let c = 'z';     
	let z: char = 'ℤ'; // with explicit type annotation     
	let heart_eyed_cat = '😻'; 
}`
```

>Note that we specify `char` literals with single quotes, as opposed to string literals, which use double quotes. Rust’s `char` type is four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid `char` values in Rust. Unicode Scalar Values range from `U+0000` to `U+D7FF` and `U+E000` to `U+10FFFF` inclusive. However, a “character” isn’t really a concept in Unicode, so your human intuition for what a “character” is may not match up with what a `char` is in Rust. We’ll discuss this topic in detail in [“Storing UTF-8 Encoded Text with Strings”](https://doc.rust-lang.org/book/ch08-02-strings.html#storing-utf-8-encoded-text-with-strings) in Chapter 8.

**Compound Tuple**
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

Array's are best used when you know the number of elements will not need to change.

```rust
fn main() {
	let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```

## Functions

All function arguments **MUST** be typed. 

Rust distinguishes between *statements* and *expressions*.

A *statement* is an instruction that does not return ant value. An *expression* evaluates to a resulting value.

Unlike in Ruby or Python, there is NO implicit return value in a statement, like setting a variable returns the variable.

In rust, *expressions* are things like functions and macros. They return a value. For example:

```rust
fn main() {
	// New scope block is an expression returning it's last line
	let y = {
        let x = 3;
        // This expression DOES NOT end with a semi colon. Semicolon would denote it as a statement.
        x + 1
    };

    println!("The value of y is: {y}");
}
```

Return values in functions get a declared type denoted after an arrow.

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```


## Control Flows
 Like with the `match` expressions, expressions in `if` statements are often called *arms*.

`if` controls explicitly need a boolean value. Unlike other languages which will infer a boolean from truthy or falsy like values.

Rust supports single line `if` statements with assignment.

```rust
let condition: bool = true;
let number = if condition { 5 } else { 6 };
```

> NOTE: Rust will check for the return type of both flows on expression to make sure the assignment is type-safe.

### Loop Types

Simple loop.
```rust
fn main() { 
	loop { 
		println!("again!"); 
	} 
	// break keyword ends loop.
	// continue keyword skips iteration.
}
```

Loops can also be used to return a value from the expression.

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
	        // For some reason, here the semi-colon is optional
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

With nested loops you can label them as to disambiguate between the different loops for use with keywords. The label is denoted by the single quote:

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

While loops accepting boolean values:

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

For loops

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```


## Ownership

The *Ownership* concept refers to Memory allocation and usage in Rust.

### Stack vs. Heap

Stack is the last in, first out memory. Data is *pushed* onto the stack and then *popped* off. All data stored on the must have a fixed size.

>NOTE: When a function is called, it's local variables get pushed onto the *Stack*. When it's over, the get popped off the *Stack*.

Heap is using the memory allocator to find space that's "big enough" and return a *pointer*. The pointer returned is known data fixed in size so it can be stored on the *Stack*. However, when you want data that it points to, you must follow the *pointer.*  

Rust manages variables on the stack while they are within scope. 

A String-literal is treated differently from a String type. The reason is that the String type accommodates for unknown sizes of data, where the string literal is essentially hardcoded into the application and therefore thrown on the stack. 

In the cases of both Stack and Heap, memory is freed as soon as the variable referencing it is removed from scope. There is a special keyword called `drop` that rust calls at the end of a curly brace (closing of scope) to free memory.

If a scalar value is set to a variable, this is a value whose size is discrete and can be added to the stack. With a string or unknown size value, the data is thrown on the heap and it's pointer is on the stack. This means that another variable set to that string would *copy it's pointer as opposed to it's data*.

In Rust, there isn't a shallow vs deep copy, there is a `move` where the pointer is moved from one variable name to the next, invalidating the first. A Deep clone would have to be explicitly accomplished through a method like `.clone()` though because of this all automatic copying can be assumed safe for runtime performance.

Functions CAN transfer ownership back to with return values. Really, think of it like a game of passing around the pointer and only one person (a.k.a, Scope) being able to have it at a time. 

>NOTE: Values can be returned by a function using Tuple so that ownership and a calculated value can be passed back from a function. `return (s, length)`

## References and Borrowing

*References* allow you to pass around variables without having to pass ownership. This allows for a variable to maintain it's original scope while still get passed to functions or other scopes. It's leveraged by using the `&` followed by the function name.

```rust
fn main() {
    let s1 = String::from("hello");
	// s1 variable is passed as reference to fn
    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

//  Parameter type expected is a reference to a String
fn calculate_length(s: &String) -> usize {
    s.len()
} // The drop function is NOT called, as this was just a reference and no memory is being cleared or relieved.

```

>NOTE: The `drop` function is only called to free memory when the current scope that maintains *ownership* to the variable is left. This is why when using a *reference* (a.k.a, *borrowing* the pointer) `drop` is not called.

### Mutable References

By default, a reference is immutable, just like a variable. Therefore if we're going to mutate the value through it's reference we must explicitly declare it's mutability while passing it through scope.

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

>NOTE: Only 1 mutable reference is allowed to a value/variable. This prevents *data racing*.

## The Slice Type

>NOTE: `usize & isize` are used when there's uncertainty around whether the underlying machine is 32-bit or 64-bit. Essentially, they mean `64 bits if possible - if not, 32 bits' 

Slices in Rust actually point to a range of a given string as opposed to copying out the subsection of the string into memory. For example:

```rust
fn main() {
	// Stores data on the heap and pointer on the stack
	let s = String::from("hello world");

	// Stores pointer on the stack to the string starting point and length
    let hello = &s[0..5];
    let world = &s[6..11];
}
```

Note that syntactically you can drop the 0 index or last index and Rust is able to infer the appropriate range.

```rust
let s = String::from("hello");
// 5 to .len() range
let slice = &s[5..]
// 0 to 5 range
let slice = &s[..5];
// Full range
let slice = &s[..];
```

>NOTE: If you're returning a slice of a string, you must denote that it's a reference to a string! This is done using a type called `&str`, which denotes a reference to a string that's already in a heap.

String literals, since they are hardcoded into the program, are always immutable references. This is because the variable stores a Slice.

This then opens up a lot of options for how we can share strings and different sections of strings using references. Consider the following.

```rust
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}

fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or whole
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```

While String slices are specific to strings, there are also slices for things like Arrays and Tuples.

What's unique about rust is the level of control over memory. Concepts like ownership, borrowing, and how slices work all are there to help ensure memory safety at compile time. However, what's cool is that while in other languages you'd have to manually free up memory and debug issues when improperly done, rust has provides debug info at the compiler level and handles freeing of memory using `drop` and `clear` when variables are dropped out of scope.

## Structs and Methods

Structs are essentially objects. Structs get declared using keynames and field types and then can be instantiated using the Struct type name before the curly braces, applying values for the fields.

Spread syntax in Rust works like in Javascript but uses only 2 periods. Unlike Javascript, it will only inherit the MISSING values, which is why it comes after the new values:

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

let user2 = User {
	active: user1.active,
	username: user1.username,
	email: String::from("another@example.com"),
	sign_in_count: user1.sign_in_count,
};
// Understand that in this example user1 is now invalidated as the 
// values that were supplied for username and otherfields have had 
// their ownership transferred to user2.
let user2 = User {
	email: String::from("some@email.com"),
	..user1
}
```

Tuple structs are also supported:

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

Structs require different Traits for printing to the console. We'll implement the Debug trait using `{:?} or {:#?}`. Now, a custom Struct won't have the Trait by default, which means we have to add it as an *outer attribute*. This is very similar to a decorator in other languages.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {:?}", rect1);
}
```

This would be pretty tedious though to constantly be logging statements, so Rust provides a debugger macro that accepts expressions and returns ownership of the supplied value. It's the `dbg!()` macro:

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

Methods get "implemented" on a struct using `impl` keyword.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

	// Equvalent of class method and called using Rect::square(20)
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```

In Rust, *associated functions* are kind of like class methods and get denoted like an instance method though they do NOT have a reference to self as the first argument. 


## Working with Enums

Enums allow us to define a set of types. 

Enums can store data within them so that separate structs don't need to be created for each type. For example:

```rust
    enum IpAddrKind {
        V4,
        V6,
    }

    struct IpAddr {
        kind: IpAddrKind,
        address: String,
    }

    let home = IpAddr {
        kind: IpAddrKind::V4,
        address: String::from("127.0.0.1"),
    };

    let loopback = IpAddr {
        kind: IpAddrKind::V6,
        address: String::from("::1"),
    };
```

Is the equivalent of:

```rust
fn main() {
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));

    let loopback = IpAddr::V6(String::from("::1"));
}
```

What's cool here too is that the different variants can actually take different data as their argument types, allowing for more variation in the ways enums can be used. For example:

```rust
fn main() {
    enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
    }

    let home = IpAddr::V4(127, 0, 0, 1);

    let loopback = IpAddr::V6(String::from("::1"));
}
```

Meanwhile, it's easy to add custom data properties on an enum LIKE it were a struct.

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
	fn call(&self) {
		// method body would be defined here
	}
}

fn main() {
    let m = Message::Write(String::from("hello"));
    m.call();
}

```

### Option in Enum

Rust does NOT have *Null* values. Instead it has a two special types contained in the *Option* type, *Some* and *None*. Both of these types can be set to any value either implicitly with Some or explicitly with None. 

What's important here is that the Compiler wont allow for non-Option types and Option types to be operated on together, like other languages would allow you to set what you think is a valid variable when it's infact null.

Example:

```rust
fn main() {
    let x: i8 = 5;
    let y: Option<i8> = Some(5);

	// the trait `Add<Option<i8>>` is not implemented for `i8`
    let sum = x + y;
}
```

This is in essence all there to force the developer to consider handling the situation of a non-value being present. The *Option* enum comes preloaded with a ton of assertion methods to help you determine whether the value is or isn't present.

Docs on Option methods are [here](https://doc.rust-lang.org/std/option/enum.Option.html).

## Match conditions

One of the most powerful features of Rust is the match conditions for arguments passed, giving great pattern matching capabilities. For all the restrictions around conditional flows, matching is handled 10x!

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {}
```

Match conditions can either support single lines of code or a function block.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {}

```

There's some other cool things we can do in here too to where we pass enums as arguments to other enum types as to further charactize/customize them. Take this state quarter example:

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}

fn main() {
    value_in_cents(Coin::Quarter(UsState::Alaska));
}
```

Match patterns are exhaustive meaning that if an enum is being passed to it there must be an arm that takes into consideration each of the possible types.

Match has some special keywords, like `other` and  `_` which are catch-all. The difference between these two is that *other* becomes a usable variable in the function body while *_* is used when the argument-value is not wanted.

`if let` are essentially syntactic sugar to reduce the need of making match conditions for single match needs.

```rust
fn main() {
    let config_max = Some(3u8);
	// The Some is the pattern
	// The max is the argument passed to the blocl
	// The config_max is the expression being evaluated
    if let Some(max) = config_max {
        println!("The maximum is configured to be {}", max);
    } else { 
		// The else block is optional
	    // do something
    }
	
}

```

## Packages and Crates

Rust has both *binary crates* and *library crates*. The difference being one is executable while the other is code that is extensible within another project. A package can have multiple binary crates by placing files in the _src/bin_ directory: each file will be a separate binary crate. A package can contain as many binary crates as you like, but at most only one library crate. A package must contain at least one crate, whether that’s a library or binary crate.

Cargo has built in commands for generating libraries and binary crates.

```rust
cargo new --lib NAME
```

The `super` keyword moves the current scope up one level to the parent module.

## Strings in Rust
Strings are tricky in rust. You have to have a lower level of awareness of them. The string class is essentially a wrapper around a `Vec<T>` type that stores character bytes. 

Some things to keep in mind:
1. You can ONLY add a &str to a String
2. You cannot add a String to a String
3. When iterating strings, be explicit about wanting `.chars() or .bytes()`
 
## Error Handling
#rust/basics/error-handling

Rust distinguishes between recoverable and unrecoverable errors. For unrecoverable, it uses the `panic!()` macro, which essentially stops everything. 

>NOTE: Apps that run the `cargo build or run` command without `--release` flag will enable backtrace debugging.

Recoverable errors rely on the `Result` type. 

```rust
enum Result<T, E> {
	Ok(T),
	Err(E),
}
```

You can use a match argument to navigate this, eventually leading to termination. Note that the example below is explanative but not accurate in that there are closures and other methods on these types that allow for more concise handling and syntax.

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {:?}", e),
            },
            other_error => {
                panic!("Problem opening the file: {:?}", other_error);
            }
        },
    };
}
```

>NOTE: *Unwraping* is about moving a value out of a type like `Some(value) || Ok(value)` when dealing with enums/structs such as `Option` or `Result`. However, different unwrap methods will handle or not handle errors for you, defaulting to the `panic!` macro.

Since recoverable errors are a first-class type, they can be passed around or propagated. Think of this as passing an error as an argument to any variable that's set to a `Result` type.

Propogating errors in rust is so common that it has its own operator, the `?` symbol. This tells the code or function to return the wrapped error of a statement automatically.

```rust
// V1
fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}

// V2
fn read_username_from_file() -> Result<String, io::Error> {
    let mut username = String::new();
    File::open("hello.txt")?.read_to_string(&mut username)?;
    Ok(username)
}

// V3
fn read_username_from_file() -> Result<String, io::Error> {
    fs::read_to_string("hello.txt")
}
```

___
# References
[The Rust Programming Language](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html#hello-cargo)
