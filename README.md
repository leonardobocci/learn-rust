``functionCall()`` vs ``macroCall!()`` : macros are special funcs

``rustc filename.rs`` compiles code. can run using ``./filename``

``main() {}`` is the entrypoint of rust programs

lines end with ;

cargo is the build system. Useful cmds: \
``cargo init`` to create new repo \
``cargo build`` to compile code and dependencies \
``./target/debug/filename`` then runs the code \
or just use ``cargo run`` to compile and run \
you can use ``cargo check`` to verify if code will be able to compile \
``cargo build --release`` to compile code with optimizations (longer compile and different outputdir for shorter runtimes) \
Cargo can be used to install **crates**. A *library crate* is a collection of source code not intended for use on its own, while a *binary crate* is an executable that was pre-compiled. \
Add crates in the dependencies section of Cargo.toml \
The versioning allows for automatic patch updates using ``cargo update``, but does not cross minor or major releases automatically. \
crates.io is the Pypi equivalent distribution index. \

To import libraries: \
``use std::io;`` \
where std is the parent library and io is the library scope to import. \
You can also import *traits*. Traits are a way to implement common behaviours (interfaces) for different types.
``use library::trait;``

Variables: \
```rust
let mut mutableVariableName = 1 //mutable with initialization;
let constantVariableName = 10 //immutable with initizalization;
let mut mutableVariableName = String::new() //empty mutable of type String;
```
let creates the variable \
mut defines mutability \
String is the initizalized type \
``::new()`` calls the method of the type that allows init of empty object of that type

References: \
The ampersand (&) character is used to call a reference. \
References are similar to variables, but don't load the whole contents of the reference into memory every time they are referenced in code.

Function calls vs method calls: \
``::myfunc()`` vs ``::myfunc().mymethod()``

Enums: \
Enums are a type that can hold multiple states (each state is a variant). \
The variants can then be *matched* to a specific outcome. \
A match expression has *arms*. Each arm has the pattern to match, and the outcome to execute. \
Each variant is connected with the matched behaviour using the ``=>`` character. \
A special Enum type is: ``Result``, which holds the success state (Ok or Err). Ok holds the result of the succesfull operation, while Err holds extra information about the exception. \
The ``.expect()`` method allows to catch **exceptions** and display the error message passed to ``.expect(MSG)`` \
A better way to handle exceptions is the ``match`` keyword. \
An enum with two variants (Ok and Err) can be matched with different behaviours. \
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
It can be obtained with the ``cmp`` comparison method that takes a reference (with ampersand &) and compares it against the object that called the method. \

Type conversions: \
It's possible to convert a type into another using the ``.parse()`` method. Here, *shadow* the name of an existing variable (re-initialize it, providing new type) you want to convert and pass the type in the initialization:
```rust
let my_var = "10";
let my_var: i32 = my_var.parse().expect("Received unparsable content");
```
Or, use the turbofish syntax ``::<TYPE>``:
```rust
let my_var = "10";
let my_var = my_var.parse::<i32>().expect("Received unparsable content");
```

Loops: \
The ``loop {}`` keyword creates an infinite loop. \

Formatted strings: \
```rust
println!("placeholder {} < placeholder {}", 1, 2); //many placeholders
let a = 10;
println!("{a} > 5"); //variable reference
```

Comments:
// inline comment

Code formatting: \
``cargo fmt``


