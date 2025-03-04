### Starter info:
``rustc filename.rs`` compiles code. can run using ``./filename`` \
``./target/debug/filename`` then runs the code \
``main() {}`` is the entrypoint of rust programs \
lines end with ``;``, expect for when returning values (eg. function returns). \
cargo is the build system. Useful cmds: \
``cargo init`` to create new repo \
``cargo build`` to compile code and dependencies \
just use ``cargo run`` to compile and run \
you can use ``cargo check`` to verify if code will be able to compile \
``cargo build --release`` to compile code with optimizations (longer compile and different outputdir for shorter runtimes) \
Cargo can be used to install **crates**. A *library crate* is a collection of source code not intended for use on its own, while a *binary crate* is an executable that was pre-compiled. \
Add crates in the dependencies section of Cargo.toml \
The versioning allows for automatic patch updates using ``cargo update``, but does not cross minor or major releases automatically. \
crates.io is the Pypi equivalent distribution index.

### Import libraries:
``use std::io;`` \
where std is the parent library and io is the library scope to import. \
You can also import *traits*. Traits are a way to implement common behaviours (interfaces) for different types.
``use library::trait;``

### Variables:
```rust
let mut mutableVariableName = 1; //mutable with initialization
let pseudoConstantVariableName = 10; //immutable with initizalization
const CONSTANT_NAME: i32 = 100; //must be type annotated, cannot every become mutable
let mut mutableVariableName = String::new(); //empty mutable of type String
let typedVariableName: str = "hi"; //init with type annotation
```
let creates the variable \
mut defines mutability \
String is the initizalized type \
``::new()`` calls the method of the type that allows init of empty object of that type \
You can't assign the same value to multiple variables directly: ``a = b = "val";`` but you can using tuples: ``(a, b) = ("val" "val")`` or expressions: ``(a, b) = ["val", 2]``

### References:
The ampersand (&) character is used to call a reference. \
References are similar to variables, but don't load the whole contents of the reference into memory every time they are referenced in code.

### Functions and macros:
``functionCall()`` vs ``macroCall!()`` : macros are special functions. \
``::myfunc()`` vs ``::myfunc().mymethod()``: types can have methods. \
Declare functions using ``fn`` keyword. `
Function order of declaration does not matter. 
Functions declared below in the same code scope can still be called. \
Functions must have a return type and argument types. \
Calling a function only supports positional arguments, not named or default ones. \
Return values specified either by last expression (not statement: without ``;`` endline), or with ``return`` keyword. \




### Enums:
Enums are a type that can hold multiple states (each state is a variant). \
The variants can then be *matched* to a specific outcome. \
A match expression has *arms*. Each arm has the pattern to match, and the outcome to execute. \
Each variant is connected with the matched behaviour using the ``=>`` character. \
A special Enum type is: ``Result``, which holds the success state (Ok or Err). Ok holds the result of the succesfull operation, while Err holds extra information about the exception. \
The ``.expect()`` method allows to catch **exceptions** and display the error message passed to ``.expect(MSG)`` \
A better way to handle exceptions is the ``match`` keyword. \
An enum with two variants (Ok and Err) can be matched with different behaviours.
```rust
let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => {
                println!("Not a valid number!");
                continue;
            }
        };
//failure to parse into u32 is ignored with a print
// the _ character catches all exception types
```
Another special Enum is the Ordering type, with Less, Greater and Equal variants. \
It can be obtained with the ``cmp`` comparison method that takes a reference (with ampersand &) and compares it against the object that called the method.

### Types:
**Scalar** types have a single value. \
These include: \
    *Integer*: \
Length	Signed	Unsigned (can only be positive ints) \
8-bit	i8	    u8 \
16-bit	i16	    u16 \
32-bit	i32	    u32 (default int) \
64-bit	i64	    u64 \
128-bit	i128	u128 \
arch	isize	usize (32bit or 64bit) \
####################### \
    *Floating point*: \
Length	Type \
32-bit	f32 \
64-bit	f64 (default float) \
####################### \
    *Boolean*: \
Type \
bool (can be ``true`` or ``false``) \
####################### \
    *Character*: \
Type \
char (represents single character of full unicode, not just ASCII) \
``let my_char: char = 'c' //use single quotes`` \
####################### \
    *String*: \
Type \
&str (represents series of valid UTF8 characters) \
``let my_str: &str = "string" //use double quotes`` \
Note: str without & is unsized, so it can't be used for function signatures or var type initialization.
####################### \
**Compound** types group multiple values. \
These include: \
    *Tuple*: \
Immutable length, can contain different types, round brackets.
```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
let (x, y, z) = tup; //extract elements (destructuring)
let first_el = x.0; //extract element by index (dot notation)
```
####################### \
    *Array*: \
Immutable length, can contain a single type, square brackets.
```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
let a = [3; 5]; //an array of 3s with length of 5
let first_el = months[0]; //extract element by index (square notation)
```
####################### \
    *Vector*: \
Re-sizeable arrays.
#TODO
####################### \
    *Structs*: \
#TODO

### Number operations:
```rust
// addition
let sum = 5 + 10;

// subtraction
let difference = 95.5 - 4.3;

// multiplication
let product = 4 * 30;

// division
let quotient = 56.7 / 32.2;
let truncated = -5 / 3; // Results in int -1, not in float -1.66
let integer_quotient = f64::from(-5) / f64::from(3); //safely converts to floats before division -> -1.66

// remainder
let remainder = 43 % 5;
```

### Type conversions:
It's possible to convert a type into another using the ``.parse()`` method. \
Here, *shadow* the name of an existing variable (re-initialize it, providing new type) you want to convert and pass the type in the initialization:
```rust
let my_var = "10";
let my_var: i32 = my_var.parse().expect("Received unparsable content");
```
Or, use the turbofish syntax ``::<TYPE>``:
```rust
let my_var = "10";
let my_var = my_var.parse::<i32>().expect("Received unparsable content");
```

### Flow control (if expression):
```rust
if <condition> {
    <code block>;
} else {
    <optional alt code block>;
}

if <condition> {
    <code block>;
} else if <alt condition 1> {
    <optional alt code block>;
} else if <alt condition 2> {
    <optional alt code block>;
} else {
    <final condition>;
}

//conditional assignment:
let number = if condition { 5 } else { 6 };
```

### Loops:
**Simple loops** \
The ``loop { }`` syntax creates an infinite loop. \
Use ``break`` to stop a loop. \
Break can also have a return value, if the loop is an assigned expression: 
```rust
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter * 2;
    }
};
```
Use ``continue`` to skip remaining code in the loop and move to next cycle. \
In the case of nested loops, ``break`` and ``continue`` would only apply to the innermost loop. This can be addressed using *loop labels*:
```rust
let mut counter = 0;
'outer_loop: loop {
    loop {
        counter += 1;
        if counter > 2 { break 'outer_loop}
        println!("inner");
    }
    println!("outer"); //this is unreachable because outer loop is broken out of.
    // without a loop label, this would be stuck in printing "outer"
}
```
####################### \
**Conditional loops** \
Use the ``while condition { }`` syntax. \
####################### \
**Iterative loops** \
Use the ``for element in collection { }`` syntax. This is more efficient and safer than a while loop with indexing. \

### Formatted strings:
```rust
println!("placeholder {} < placeholder {}", 1, 2); //many placeholders
let a = 10;
println!("{a} > 5"); //variable reference
```

### Comments:
``// inline comment`` and ``/* multiline comment */``

### Code check:
``cargo fmt`` //formatting
``cargo clippy`` //linting


