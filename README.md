# Dart Programming Complete Syllabus

A comprehensive, step-by-step learning path for mastering Dart programming language before diving into Object-Oriented Programming (OOP) concepts.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Development Environment](#development-environment)
3. [Project Setup & Management](#project-setup--management)
4. [Variables & Constants](#variables--constants)
5. [Operators](#operators)
6. [Comments](#comments)
7. [Data Types](#data-types)
8. [Collections](#collections)
9. [Control Flow](#control-flow)
10. [Functions](#functions)
11. [Concurrency](#concurrency)
12. [Null Safety](#null-safety)
13. [JSON Handling](#json-handling)

---

## Getting Started

### What is Flutter?
A cross-platform UI toolkit developed by Google for building natively compiled applications for mobile, web, and desktop from a single codebase.

### Why Learn Flutter?
- Single codebase for multiple platforms (iOS, Android, Web, Desktop)
- Hot reload for faster development
- Beautiful, customizable UI components
- Strong community and Google support
- High performance with native compilation

### What is a Programming Language?
A formal language comprising instructions that produce various outputs. It enables humans to communicate with computers through syntax and semantics.

### What is Dart?
Dart is a client-optimized programming language developed by Google, primarily used for building mobile, desktop, server, and web applications. It's the language behind Flutter.

---

## Development Environment

### What are Editor Tools?
Software applications that help developers write, edit, debug, and manage code. They provide features like syntax highlighting, code completion, and error detection.

### What is DartPad?
An online editor for experimenting with Dart code directly in your browser. No installation required – perfect for quick testing and learning.

**Access:** https://dartpad.dev

### What is Android Studio?
A powerful IDE (Integrated Development Environment) for Android development, built on IntelliJ IDEA. It includes tools for Flutter development with plugins.

### What is Git?
A distributed version control system that tracks changes in source code during software development. It enables multiple developers to work together on projects.

### What is GitHub?
A web-based platform that hosts Git repositories. It provides collaboration features like pull requests, issues, and project management tools.

### What is Flutter SDK?
Software Development Kit containing all the necessary tools, libraries, and frameworks to develop Flutter applications.

### What is JDK?
Java Development Kit – a software development environment required for building Android applications. Includes compiler, debugger, and runtime environment.

### What is Gradlew?
Gradle Wrapper – a script that allows you to run Gradle builds without installing Gradle. It ensures consistent build environments across different machines.

### What is pubspec.yaml?
A configuration file in Dart/Flutter projects that defines:
- Project dependencies
- Package versions
- Assets (images, fonts)
- Project metadata

---

## Project Setup & Management

### How to Create a Flutter Project

```bash
flutter create project_name
```

### How to Check Versions

```bash
# Flutter version
flutter --version

# Dart version
dart --version

# Java version
java -version
```

### How to Set Up Flutter in Windows

1. Download Flutter SDK from official website
2. Extract to desired location (e.g., `C:\src\flutter`)
3. Add Flutter to PATH environment variable
4. Install Android Studio
5. Install Flutter and Dart plugins in Android Studio
6. Run `flutter doctor` to verify installation
7. Accept Android licenses: `flutter doctor --android-licenses`

---

## Variables & Constants

### What is a Variable?
A named storage location in memory that holds a value which can change during program execution.

### What is var?
A keyword for declaring variables without explicitly specifying the type. Dart infers the type from the assigned value.

```dart
var name = 'John';  // String type inferred
var age = 25;       // int type inferred
```

### What is a Dart Variable?
A container that stores data values in Dart programs. Variables must be declared before use and follow Dart's type system.

### What is late Variable?
A modifier that allows you to declare non-nullable variables that are initialized after declaration but before use.

```dart
late String description;
void initialize() {
  description = 'Initialized later';
}
```

### What is final Keyword?
Creates a runtime constant – a variable that can only be set once and cannot be changed after initialization.

```dart
final String name = 'Alice';
final currentTime = DateTime.now();  // Evaluated at runtime
```

### What is const Keyword?
Creates a compile-time constant – a value that must be known and fixed at compile time.

```dart
const pi = 3.14159;
const maxItems = 100;
```

### Difference Between final and const

| Aspect | final | const |
|--------|-------|-------|
| Evaluation | Runtime | Compile-time |
| Use Case | Values known at runtime | Values known at compile-time |
| Memory | Each instance gets own copy | Single canonical instance |
| Objects | Can contain mutable objects | Deep immutability |

```dart
final list1 = [1, 2, 3];
list1.add(4);  // Allowed – list is mutable

const list2 = [1, 2, 3];
// list2.add(4);  // ERROR – completely immutable
```

### What are Compile-time Constants?
Values that are calculated and fixed during compilation, before the program runs. Must use `const` keyword.

### What are Runtime Constants?
Values that are determined when the program executes. Can use `final` keyword.

### What is static Keyword?
Creates class-level members that belong to the class itself rather than instances of the class.

```dart
class MathUtils {
  static const pi = 3.14159;
  static int add(int a, int b) => a + b;
}
```

---

## Operators

### What are Operators?
Special symbols that perform operations on operands (variables or values).

### Types of Operators

#### 1. Arithmetic Operators
Perform mathematical calculations.

| Operator | Name | Example |
|----------|------|---------|
| `+` | Addition | `5 + 3 = 8` |
| `-` | Subtraction | `5 - 3 = 2` |
| `*` | Multiplication | `5 * 3 = 15` |
| `/` | Division | `5 / 2 = 2.5` |
| `~/` | Integer Division | `5 ~/ 2 = 2` |
| `%` | Modulus (Remainder) | `5 % 2 = 1` |

#### 2. Equality and Relational Operators
Compare values and return boolean results.

| Operator | Name | Example |
|----------|------|---------|
| `==` | Equal to | `5 == 5` is `true` |
| `!=` | Not equal to | `5 != 3` is `true` |
| `>` | Greater than | `5 > 3` is `true` |
| `<` | Less than | `3 < 5` is `true` |
| `>=` | Greater than or equal | `5 >= 5` is `true` |
| `<=` | Less than or equal | `3 <= 5` is `true` |

#### 3. Type Test Operators
Check and cast types at runtime.

| Operator | Name | Usage |
|----------|------|-------|
| `is` | Type check (true if match) | `x is String` |
| `is!` | Type check (true if not match) | `x is! int` |
| `as` | Type cast | `x as String` |

#### 4. Assignment Operators
Assign values to variables.

| Operator | Example | Equivalent to |
|----------|---------|---------------|
| `=` | `x = 5` | Assign |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `~/=` | `x ~/= 3` | `x = x ~/ 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `&=` | `x &= 3` | `x = x & 3` |
| `|=` | `x |= 3` | `x = x | 3` |
| `^=` | `x ^= 3` | `x = x ^ 3` |
| `<<=` | `x <<= 3` | `x = x << 3` |
| `>>=` | `x >>= 3` | `x = x >> 3` |
| `>>>=` | `x >>>= 3` | `x = x >>> 3` |

#### 5. Logical Operators
Combine or invert boolean expressions.

| Operator | Name | Example |
|----------|------|---------|
| `!` | NOT (negation) | `!true` is `false` |
| `||` | OR | `true || false` is `true` |
| `&&` | AND | `true && false` is `false` |

#### 6. Bitwise and Shift Operators
Perform bit-level operations.

| Operator | Name | Description |
|----------|------|-------------|
| `&` | AND | Both bits must be 1 |
| `|` | OR | At least one bit is 1 |
| `^` | XOR | Bits are different |
| `~` | NOT | Inverts bits |
| `<<` | Left shift | Shift bits left |
| `>>` | Right shift | Shift bits right |
| `>>>` | Unsigned right shift | Shift right with zero fill |

#### 7. Conditional Expressions
Compact if-else alternatives.

| Operator | Name | Syntax |
|----------|------|--------|
| `? :` | Ternary | `condition ? valueIfTrue : valueIfFalse` |
| `??` | Null coalescing | `value1 ?? value2` (returns value2 if value1 is null) |

#### 8. Cascade Notation
Chain multiple operations on the same object.

| Operator | Usage | Example |
|----------|-------|---------|
| `..` | Cascade | `obj..method1()..method2()` |
| `?..` | Null-aware cascade | `obj?..method()` |

#### 9. Spread Operators
Expand collections inline.

| Operator | Usage | Example |
|----------|-------|---------|
| `...` | Spread | `[...list1, ...list2]` |
| `...?` | Null-aware spread | `[...?nullableList]` |

#### 10. Other Operators

| Operator | Name | Usage |
|----------|------|-------|
| `()` | Function call | `function()` |
| `[]` | List access | `list[0]` |
| `?[]` | Null-aware list access | `list?[0]` |
| `.` | Member access | `object.property` |
| `?.` | Null-aware member access | `object?.property` |
| `!` | Null assertion | `nullable!` |

---

## Comments

### What are Comments?
Non-executable text in code that explains functionality, provides documentation, or adds notes for developers.

### Types of Comments

#### 1. Single-line Comments
```dart
// This is a single-line comment
int age = 25;  // Age of the user
```

#### 2. Multi-line Comments
```dart
/*
This is a multi-line comment
spanning multiple lines
Useful for longer explanations
*/
int calculate(int a, int b) {
  return a + b;
}
```

#### 3. Documentation Comments
```dart
/// Calculates the sum of two numbers.
///
/// Returns the sum of [a] and [b].
/// 
/// Example:
/// ```dart
/// int result = add(5, 3);  // Returns 8
/// ```
int add(int a, int b) {
  return a + b;
}
```

---

## Data Types

### What is the main() Function?
The entry point of every Dart program. Execution starts from the main() function.

```dart
void main() {
  print('Hello, Dart!');
}
```

### How to Run Your First App

```bash
# Run Dart file
dart run filename.dart

# Or in Flutter
flutter run
```

### What are Emulator Device and Real Device?

**Emulator Device:**
- Virtual device running on your computer
- Simulates Android/iOS environment
- Useful for testing without physical hardware

**Real Device:**
- Physical smartphone or tablet
- More accurate testing experience
- Better performance testing

### Core Data Types

#### 1. Numbers
```dart
int age = 25;              // Integer
double price = 19.99;      // Floating-point number
num quantity = 10;         // Can be int or double
```

#### 2. Strings
```dart
String name = 'Alice';
String message = "Hello, World!";
String multiline = '''
This is a
multi-line string
''';
```

#### 3. Booleans
```dart
bool isActive = true;
bool hasPermission = false;
```

#### 4. Records
```dart
(int, String) record = (1, 'First');
var (id, name) = record;  // Destructuring
```

#### 5. Functions
```dart
Function greet = (String name) => print('Hello, $name');
```

#### 6. Lists (Arrays)
```dart
List<int> numbers = [1, 2, 3, 4, 5];
var names = ['Alice', 'Bob', 'Charlie'];
```

#### 7. Sets
```dart
Set<String> uniqueNames = {'Alice', 'Bob', 'Charlie'};
var numbers = {1, 2, 3, 3};  // Duplicates removed
```

#### 8. Maps
```dart
Map<String, int> scores = {
  'Alice': 90,
  'Bob': 85,
  'Charlie': 95,
};
```

#### 9. Runes
```dart
Runes input = Runes('\u{1f600}');  // 😀 emoji
```

#### 10. Symbols
```dart
Symbol sym = #mySymbol;
```

### Special Type Keywords

#### What is enum?
Defines a set of named constant values.

```dart
enum Status { pending, approved, rejected }
Status currentStatus = Status.pending;
```

#### What is Future?
Represents a potential value or error that will be available at some time in the future.

```dart
Future<String> fetchData() async {
  return 'Data loaded';
}
```

#### What is void?
Indicates that a function doesn't return a value.

```dart
void printMessage(String msg) {
  print(msg);
}
```

#### What is Iterable?
A collection of values that can be accessed sequentially.

```dart
Iterable<int> numbers = [1, 2, 3, 4, 5];
```

#### What is Never?
Indicates that a function never successfully completes (always throws or never returns).

```dart
Never throwError() {
  throw Exception('Error occurred');
}
```

#### What is dynamic?
Allows any type at runtime – bypasses type checking.

```dart
dynamic variable = 'String';
variable = 42;  // Allowed
```

#### What is Object?
The base class of all Dart objects (except null).

```dart
Object value = 'Can be any type';
```

#### What is Return Type?
The data type that a function returns to its caller.

```dart
int add(int a, int b) {  // int is the return type
  return a + b;
}
```

#### What are Typedefs?
Creates an alias for a function signature or type.

```dart
typedef IntOperation = int Function(int, int);

IntOperation add = (a, b) => a + b;
IntOperation multiply = (a, b) => a * b;
```

#### What is Type Safety?
A feature that prevents type errors by enforcing type constraints at compile time.

---

## Collections

### What are Collections?
Data structures that hold multiple values in a single variable.

### List Operations

```dart
List<int> numbers = [1, 2, 3];

// Properties
numbers.length;           // Get size

// Methods
numbers.add(4);           // Add single element
numbers.addAll([5, 6]);   // Add multiple elements
numbers.remove(2);        // Remove by value
numbers.removeAt(0);      // Remove by index
numbers.clear();          // Remove all elements
```

### What are Generics?
Type parameters that allow you to write reusable code that works with different types while maintaining type safety.

```dart
List<int> intList = [1, 2, 3];
List<String> stringList = ['a', 'b', 'c'];

T getFirst<T>(List<T> items) {
  return items[0];
}
```

### Why Use Generics?
1. **Type Safety:** Catch type errors at compile time
2. **Code Reusability:** Write once, use with multiple types
3. **Better Documentation:** Code is self-documenting
4. **Performance:** Avoid runtime type checks

### What is cast()?
Converts a collection from one type to another.

```dart
var numbers = [1, 2, 3];
List<num> numList = numbers.cast<num>();
```

### What is Null-assert (!)?
Tells Dart that a nullable value is definitely not null.

```dart
String? nullableText = 'Hello';
String text = nullableText!;  // Assert it's not null
```

### What is Wildcard (_)?
A placeholder that ignores a value.

```dart
var (x, _) = (10, 20);  // Ignore second value
```

### What are Pattern Types?
New feature in Dart 3 for destructuring and matching values.

```dart
switch (value) {
  case [var a, var b]:
    print('List with two elements: $a, $b');
  case {'key': var v}:
    print('Map with key: $v');
}
```

---

## Control Flow

### What are Loops?
Constructs that repeat a block of code multiple times.

### Types of Loops

#### 1. For Loop
```dart
for (int i = 0; i < 5; i++) {
  print(i);
}

// For-in loop
for (var item in ['a', 'b', 'c']) {
  print(item);
}
```

#### 2. While Loop
```dart
int count = 0;
while (count < 5) {
  print(count);
  count++;
}
```

#### 3. Do-While Loop
```dart
int count = 0;
do {
  print(count);
  count++;
} while (count < 5);
```

#### 4. Break and Continue
```dart
for (int i = 0; i < 10; i++) {
  if (i == 5) break;        // Exit loop
  if (i % 2 == 0) continue; // Skip iteration
  print(i);
}
```

### What is if-else?
Conditional statement that executes code based on boolean conditions.

```dart
int age = 18;
if (age >= 18) {
  print('Adult');
} else if (age >= 13) {
  print('Teenager');
} else {
  print('Child');
}
```

### What is switch-case?
Multi-way branch statement that selects one of many code blocks to execute.

```dart
String grade = 'A';
switch (grade) {
  case 'A':
    print('Excellent');
    break;
  case 'B':
    print('Good');
    break;
  default:
    print('Keep trying');
}
```

### What is Error Handling?
The process of responding to and recovering from error conditions in programs.

### What is an Exception?
An object representing an error or unexpected event during program execution.

### What is throw?
Keyword used to raise an exception.

```dart
throw FormatException('Invalid format');
```

### What is try-catch?
Mechanism to handle exceptions and prevent program crashes.

```dart
try {
  int result = 10 ~/ 0;  // Will throw exception
} catch (e) {
  print('Error: $e');
}
```

### How does finally Work?
A block that always executes, whether an exception occurred or not.

```dart
try {
  // risky operation
} catch (e) {
  print('Error: $e');
} finally {
  print('This always runs');
}
```

### What is assert?
A statement that checks conditions during development (disabled in production).

```dart
assert(age >= 0, 'Age cannot be negative');
```

---

## Functions

### What is a Function?
A reusable block of code that performs a specific task.

```dart
int add(int a, int b) {
  return a + b;
}
```

### What are Parameters?
Variables that receive values when a function is called.

### Types of Parameters

#### 1. Named Parameters
```dart
void greet({required String name, int age = 0}) {
  print('Hello $name, age $age');
}

greet(name: 'Alice', age: 25);
greet(name: 'Bob');  // age defaults to 0
```

#### 2. Optional Positional Parameters
```dart
void display(String name, [int? age]) {
  print('Name: $name, Age: ${age ?? 'N/A'}');
}

display('Alice');
display('Bob', 30);
```

### Function Types

#### Anonymous Functions (Lambda)
```dart
var multiply = (int a, int b) => a * b;

List<int> numbers = [1, 2, 3];
numbers.forEach((n) => print(n * 2));
```

### What are Annotations?
Metadata that provides additional information about code.

```dart
@override
void toString() {
  return 'Custom string';
}

@deprecated
void oldFunction() {
  // ...
}
```

### What are Libraries & Imports?
**Libraries:** Collections of code that can be reused across projects.

```dart
// Import built-in library
import 'dart:math';

// Import package
import 'package:http/http.dart';

// Import with prefix
import 'dart:math' as math;

// Import specific parts
import 'package:lib/lib.dart' show functionName;
```

---

## Concurrency

### What is Asynchronous Programming?
Code execution that allows other operations to run while waiting for long-running tasks to complete.

### What is Synchronous Programming?
Sequential code execution where each operation must complete before the next one starts.

### What is async Keyword?
Marks a function as asynchronous, enabling the use of `await` inside it.

```dart
Future<String> fetchData() async {
  return 'Data loaded';
}
```

### What is await Keyword?
Pauses execution until a Future completes and returns its value.

```dart
Future<void> loadData() async {
  String data = await fetchData();
  print(data);
}
```

### Why is Async/Await Needed?
1. **Non-blocking:** UI remains responsive during long operations
2. **Readable:** Write asynchronous code that looks synchronous
3. **Error Handling:** Use try-catch with async operations

### What is async*?
Creates an asynchronous generator function that yields values over time.

```dart
Stream<int> countStream(int max) async* {
  for (int i = 0; i < max; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}
```

### Difference Between async and await

| Aspect | async | await |
|--------|-------|-------|
| Purpose | Declares function as asynchronous | Waits for Future completion |
| Returns | Future automatically | Unwraps Future value |
| Usage | Function modifier | Expression operator |

### What are Isolates?
Independent workers that run code in parallel without sharing memory. True concurrency in Dart.

```dart
import 'dart:isolate';

void heavyTask(SendPort sendPort) {
  // Perform intensive computation
  sendPort.send('Result');
}

void main() async {
  ReceivePort receivePort = ReceivePort();
  await Isolate.spawn(heavyTask, receivePort.sendPort);
  var result = await receivePort.first;
  print(result);
}
```

---

## Null Safety

### What is Null Safety?
A feature that prevents null reference errors by making nullability part of the type system.

### What is Sound Null Safety?
Dart's guarantee that non-nullable types will never contain null values at runtime.

```dart
int age = 25;        // Cannot be null
int? nullableAge;    // Can be null
```

### What is Unsound Null Safety?
A mixed mode where some code has null safety while other parts don't (migration period).

### Null Safety Operators

```dart
String? nullable = null;

// Null-aware access
nullable?.length;

// Null assertion
nullable!.length;  // Throws if null

// Null coalescing
String value = nullable ?? 'default';

// Null-aware cascade
nullable?..trim()..toLowerCase();
```

---

## JSON Handling

### What is JSON?
JavaScript Object Notation – a lightweight data interchange format that's easy to read and write.

```json
{
  "name": "Alice",
  "age": 25,
  "isActive": true,
  "hobbies": ["reading", "gaming"]
}
```

### What is Decode (Parsing)?
Converting JSON string into Dart objects.

```dart
import 'dart:convert';

String jsonString = '{"name": "Alice", "age": 25}';
Map<String, dynamic> user = jsonDecode(jsonString);

print(user['name']);  // Alice
print(user['age']);   // 25
```

### What is Encode (Serialization)?
Converting Dart objects into JSON strings.

```dart
import 'dart:convert';

Map<String, dynamic> user = {
  'name': 'Alice',
  'age': 25,
  'hobbies': ['reading', 'gaming']
};

String jsonString = jsonEncode(user);
print(jsonString);  // {"name":"Alice","age":25,"hobbies":["reading","gaming"]}
```

---

## Next Steps

After completing this syllabus, you'll be ready to:

1. **Learn Object-Oriented Programming (OOP)** concepts in Dart
2. **Build Flutter Applications** with confidence
3. **Explore Advanced Topics** like streams, mixins, and extensions
4. **Practice Real-World Projects** to solidify your knowledge

---

## Resources

- **Official Dart Documentation:** https://dart.dev/guides
- **DartPad (Online Editor):** https://dartpad.dev
- **Flutter Documentation:** https://flutter.dev/docs
- **Dart Package Repository:** https://pub.dev

---

**Note:** This syllabus is designed to build a strong foundation in Dart programming. Each topic should be understood thoroughly before moving to the next. Practice coding examples for every concept to reinforce learning.
