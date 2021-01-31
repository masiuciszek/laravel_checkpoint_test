# New born ruslang

## Table of Contents

- [New born ruslang](#new-born-ruslang)
  - [Table of Contents](#table-of-contents)
  - [About <a name = "about"></a>](#about-)
  - [Statement vs Expression <a name ="s-vs-e"></a>](#statement-vs-expression-)
  - [Control Flow <a name ="cf"></a>](#control-flow-)
  - [Enums <a name ="enums"></a>](#enums-)
  - [Structs <a name ="structs"></a>](#structs-)
  - [Methods <a name ="methods"></a>](#methods-)
  - [Borrowing <a name ="borrowing"></a>](#borrowing-)
  - [Borrowing patterns <a name ="borrowing-patterns"></a>](#borrowing-patterns-)
  - [Slices <a name ="slices"></a>](#slices-)
  - [Self <a href = "self"></a>](#self-)
  - [Ownership <a name ="ownership"></a>](#ownership-)
  - [Playground](#playground)

## About <a name = "about"></a>

New born ruslang, a beginner repo that will go through the very basics in rust such as
`[Control Flow](#cf)`, `[Structs](#structs)` `[Methods](#methods)` and so much more.

Rust is a system level programing language, but it is so much more thane that. Me personally that coming from a `Javascript` background, Rust is a game changer, people think that web-assembly and rust will replace `Javascript` but I don't think it is like that. I know that Rust together with Javascript will make `Javascript` so much more powerful and only the feature can tell us what it will bring.

Javascript developers will use Rust and web assembly without even knowing it, if you don't want of course, for example front end frameworks like `React` or `Svelte` could be even more optimized with `Rust` and thats is what I mean that you will probably use it without even knowing it. The thing you will make notice of is how much faster and precise everything would be.

This Repo is for you as a `JS` developer to learn the fundamentals in `Rust` and how it could help you to become a much better `Javascript` developer

## Statement vs Expression <a name ="s-vs-e"></a>

To know statement vs expression is important specially in `rust` when to add
semicolon or not. A statement is something that we currently do in part of code
without returning for example.

```rust
 if a > 10 {
   println!("foo");
 }else{
   println!("bar");
 }
```

as you see wee add semicolon after the `println!` function do declare that this
is a statement and not a expression.

To show ho a expression would look like we could been writing it like this.

```rust
  fn double(x:u8) -> u:8 {
    // also a expression here
    x * 2
  }
  let a:u8 = 20;

  if a > 10 {
    double(a)
  }else{
  // else just return a
   a
  }

```

## Control Flow <a name ="cf"></a>

## Enums <a name ="enums"></a>

An `enum` is a a single type. That are fixed and describes a pattern of a static item, for example:

```rust
enum Day {
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}

```

We access the `variants` from the `enum` via `::` ex `Day::Friday`
An `enum` can also hold data like tuples,unit struts ore records.

```rust

enum StatusMessage {
    Success,                                // unit variant
    Warning { code: i32, message: String }, // Struct variant
    Error(String),                          // tuple variant
}

fn main() {
    let mut form_status = StatusMessage::Success;
    print_status(form_status);
    form_status = StatusMessage::Warning {
        code: 404,
        message: String::from("Oooops!"),
    };
    print_status(form_status);
    form_status = StatusMessage::Error(String::from("Error!"));
    print_status(form_status);
}

fn print_status(status: StatusMessage) {
    match status {
        StatusMessage::Success => println!("Success "),
        StatusMessage::Warning { code, message } => println!("Warning {} - {}", code, message),
        StatusMessage::Error(msg) => println!("Error: {} ", msg),
    }
}

}
```

## Structs <a name ="structs"></a>

With `Structs` we can structure our `rust` programs in a more logical and proper way.
Structs are used to encapsulate related properties into one unified data type.
`rust` follows a convention to use `PascalCase` when creating structs.

There are 3 different structs in `rust`

1. **C-like structs**

- Similar to classes if you coming from a `OOP` background.
- Fields has key's so we can access properties via dot notation

2. **Tuple structs**

- One ore more values separated with a comma, no key value pairs!
- uses parenthesizes instead of curly brackets

3. **Unit structs**

- useful when using generics

**C-like-struct**

```rust
  #[derive(Debug)]
struct Dog {
    name: String,
    age: u8,
    owner: Person,
}

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
    cool: bool,
}

impl Dog {
    fn new(name: String, age: u8, owner: Person) -> Self {
        Dog { name, age, owner }
    }

    fn greet(&self) {
        println!(
            "Hello my name is {} and my owner is {:?}",
            self.name, self.owner.name
        );
    }
}

impl Person {
    fn new(name: String, age: u8, cool: bool) -> Self {
        Person { name, age, cool }
    }
}

fn main() {
    let bob = Person::new(String::from("Bob"), 34, true);
    let mike = Person::new(String::from("Mike"), 21, true);

    let snickers = Dog::new(String::from("Snickers"), 2, bob);
    let logan = Dog::new(String::from("Logan"), 6, mike);

    snickers.greet();
    // Hello my name is Snickers and my owner is "Bob"
}

```

another good example on using `C-like structs`

```rust
#[derive(Debug)]
struct Shape {
    width: u8,
    height: u8,
}

impl Shape {
    fn area(&self) -> u8 {
        self.width * self.height
    }

    fn rectangle(width: u8, height: u8) -> Shape {
        Shape { width, height }
    }

    fn square(side: u8) -> Shape {
        Shape {
            width: side,
            height: side,
        }
    }
}
fn does_fit(s1: &Shape, s2: &Shape) -> bool {
    s1.width >= s2.width && s1.height >= s2.height
}

fn main() {
    let rec = Shape::rectangle(30, 25);
    let square = Shape::square(15);

    println!(
        "this is a square {:?} and this is an rectangle {:?}",
        square, rec
    );

    let does_fit_check_first = does_fit(&rec, &square);
    let does_fit_check_second = does_fit(&square, &rec);

    println!(
        "first check = {}, second check = {} ",
        does_fit_check_first, does_fit_check_second
    );
}

```

A tuple struct has only one element,
we usually call it new-type pattern. Because it helps to create a new type.

```rust
  struct Rgb(u8, u8, u8);
struct IsCool(bool);


fn main() {
    let blue = Rgb(2, 136, 209);
    let cool = IsCool(true);
}

```

Unit structs is not so common to use but are more powerful when combined with other features.

```rust
#[derive(Debug)]
struct Foo;

fn main() {
    let f = Foo;
    println!("{:?}", f); // Foo
}

```

## Methods <a name ="methods"></a>

## Borrowing <a name ="borrowing"></a>

Borrowing in `Rust` helps us to barrow a the data for a short amount of time, for exempla when passing a user struct into a greet method like this.

```rust
  struct User {
    username: String,
    age: u8,
    cool: bool,
    email: String,
    password: String,
}

impl User {
  fn greet(&self) {
    println!(
      "Hello my name is {} and I am {} years old",
            self.username, self.age
        );
    }
  }

  fn main() {
    let  linda = User::new(User {
      username: String::from("Linda"),
        email: String::from("linda@io.com"),
        cool: true,
        age: 32,
        password: String::from("123456"),
    });
    &linda.greet();
}
```

Borrowing a value may feel similar to pointers if you been working with `C` ore other languages that using pointers.Borrowing is a way to use some code for a time without taking the ownership.
Like someone want's to borrow your car for a while.
Even if your friend is using your car it is still your car and your responsibility to pay the taxes and stuff, in this case when it come to `rust` clean up after you.

```rust
enum AnimalType {
  Dog,
    Cat,
}

struct Animal {
  name: String,
    animalType: AnimalType,
}

// Barrow the animal by making a reference
fn greet(animal: &Animal) {
  println!("hello there {} ", animal.name);
}

fn main() {
    let dog = Animal {
        name: String::from("Snickers"),
        animalType: AnimalType::Dog,
    };

    greet(&dog);
    println!(
        "I can still us dog here: {}, because we just barrowed the dog when passing goh to greet",
        dog.name
    );
```

## Ownership <a name ="ownership"></a>

Rust does not have any garbage collector like languages like `javascript`, `java` ore `golang`. To really understand `rust` we will go through how clearing up memory works in `rust` and how ownership works.
Ownership in `rust` is a strategy for the rust compiler to managing data in memory and preventing common problems.
Every chunk of memory must have one value that is the owner of the memory.
The owner responsibility it to clean up data en free up space(memory).
This happens when the owners variable go out of scope.
We can also decide if the dta should be mutable or not with the `mut` keyword.

Imagine that you inviting your friends for a nice dinner at home. You are responsible for cooking and serving the food, everyone can share and eat the food but you have to clean up and make the dishes when everyone leaves.

Same as for the owner of the variable, we can barrow the data for a bit and then give it back to the owner, for example making a reference to a function parameter.

for example:

```rust
fn say_hi(str: String) {
    println!("hello {} ", str);
}

fn main() {
    let a = String::from("legia");
    say_hi(a);
    // Will give us a error
    println!("{}", a);
}

```

**Why do we borrowing?**
With help of borrowing a value we gain performance. Instead of make a copy of a value and pass it to the function to create a new spot in memory, we can simply borrow the value and then give it back when we are finished.

- What is borrowing? lend out a value instead of transferring ownership
- Why borrow? reduce allocations, improve performance

## Borrowing Patterns <a name = "#borrowing-patterns"> </a>

How does the compiler works when follow different patterns in rust?
Borrowing patterns in rust is great to know to have much better understanding how the complier works, and to learn to work with the complier and not against it.

`At the same time`, what does this actually mean?
Most when you here somone says `Borrow at the same time` they mean they are the same lexical scope created by curly brackets.

```
At the same time = in the same scope
```

```rust
fn main() {
  let xs = vec![1, 2, 3, 4, 5];

  let first = xs.first();
  let last = xs.last();

  println!(
    "The first number is {:?} and the last number is {:?}",
    first, last
  );
}

```

To tell rust that we are done with the immutable borrows before the end of the main, we can add another scope, a inner scope that end before the outer scope.

in Rust > 1.24 this code will compile and works fine.

```rust
  fn main() {
  let mut xs = vec![1, 2, 3, 4, 5];

  let first = xs.first();
  let last = xs.last();

  println!(
    "The first number is {:?} and the last number is {:?}",
    first, last
  );

  *xs.first_mut().expect("list was empty") += 1;
}

```

But in versions < 1.24 we had to wrap our code in local inner scope to make it work.

```rust
fn main() {
  let mut xs = vec![1, 2, 3, 4, 5];

{

  let first = xs.first();
  let last = xs.last();

  println!(
    "The first number is {:?} and the last number is {:?}",
    first, last
  );

 }

  *xs.first_mut().expect("list was empty") += 1;
}

```

the `entry` method in rust defined on a `HashMap`.
This method abstracts away the conditionals that handle if the key is present or not, and instead exposes methods to customize what to do in those cases.

For example this code will not compile

```rust
use std::collections::HashMap;

fn main() {
  let sen = "Legia Waraszawa is the best team in the world!";

  let mut freqs = HashMap::new();
  let one_string: String = sen.split_whitespace().collect();

  for char in one_string.chars() {
    match freqs.get(char) {
      Some(c) => *c += 1,
      None => freqs.insert(char, 1),
    }
  }
}

```

But when using the `entry` method we can easily split up the logic and make the compiler happy again.

```rust
use std::collections::HashMap;

fn main() {
  let sen = "Legia Waraszawa is the best team in the world!";

  let mut freqs = HashMap::new();
  let one_string: String = sen.split_whitespace().collect();

  for char in one_string.chars() {

    *freqs.entry(char).or_insert(0) += 1;
  }
}

```

`entry` works similar to a get method where you provide the key and you will get back both the key and the value pair.

for example

```rust
  freqs.entry('l') // { key: 'l', value: 1 })
```

## Slices <a name ="slices"></a>

Slices is a datatype in `Rust` that has to do with borrowing different values.
**So what is a slice?**
A slice is a data type that always borrow data owned by some other data structure, like for example a `String`, or `u8`.
A slice contains a pointer and a length, The pointer is a reference to the start of the data that the slice contains, and the length is the amount of elements after the start that the slice contains.

How to store a slice in `Rust`.
We create a slice using an ampersand, the variable we're using/referencing, and square brackets containing a range.

```rust
fn main() {
    let name = "marcell";
    let name_slice = &name[0..3];
    let cell = &name[3..];
    let barrow_all_data = &name[..];
    println!(
        "name_slice is {} and the length is {:?} ",
        name_slice,
        name_slice.chars().count()
    );
    // name_slice is mar and the length is 3
    println!("{}", cell); // cell
    println!("{}", barrow_all_data); // marcell
}

```

We can even use slices from a `vector` ore an `array`. The difference between a vector and a arrray is that an vector can grow in size similar like a array in `JS` and a array in `Rust` has a fixed length.

rust will panic if we try to create a slice which is greater then the length of the data structure itself.

```rust
  let xs = vec![1,2,3];
  let xsSlice = &xs[0..99]; // Panic ! Not alllowed
```

## Self <a href = "self"></a>

When using the `self` keyword `Rust` creates the reference automatically, and it know when we want to make a mutable reference as well.
For example, a user struct where we implement a `birthday` method, this is a good use case when we want to mute the users age.

````rust
  struct User {
    name: String,
    age: u8,
  }

  impl User {
    birthday(&mut self){
        self.age +=1;
    }
  }

  fn main(){

    let mut marcell = User{ name: String::from("Marcell"), age: 24 };
    marcell.birthday();
    // {name: Marcell, age: 25}
  }
This happens because as soon be use `a` as a parameter in `say_hi` function, the `str` argument will take the ownership over a and we will no longer have access to a.

The compiler will help us:

```rust
error[E0382]: borrow of moved value: `a`
 --> src/main.rs:8:20
  |
6 |     let a = String::from("legia");
  |         - move occurs because `a` has type `String`, which does not implement the `Copy` trait
7 |     say_hi(a);
  |            - value moved here
8 |     println!("{}", a);
  |                    ^ value borrowed here after move
````

To make it work we could borrow the string instead by making a reference.

```rust
fn say_hi(str: &String) {
    println!("hello {} ", str);
}

fn main() {
    let a = String::from("legia");
    say_hi(&a);
    println!("{}", a);
}

```

## Playground <a name ="playground"></a>

A simple filter even numbers example not using built in filter function.

```rust
fn main() {
    let xs: Vec<i32> = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];

    let evenXs = evens(&xs);
    println!("{:?}", evenXs);
}

fn evens(xs: &Vec<i32>) -> Vec<i32> {
    let mut newXs: Vec<i32> = Vec::new();

    for x in xs.iter() {
        if x % 2 == 0 {
            newXs.push(*x);
        }
    }
    newXs
}

```
