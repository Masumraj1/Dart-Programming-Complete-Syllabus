# ডার্ট OOP (অবজেক্ট-ওরিয়েন্টেড প্রোগ্রামিং) সম্পূর্ণ গাইড

অবজেক্ট-ওরিয়েন্টেড প্রোগ্রামিং (OOP) হলো একটি প্রোগ্রামিং প্যারাডাইম যা "অবজেক্ট" ধারণার উপর ভিত্তি করে গড়ে উঠেছে। ডার্টে OOP এর সমস্ত ধারণা সম্পূর্ণভাবে সমর্থিত।

---

## বিষয়সূচি

1. [OOP পরিচিতি](#oop-পরিচিতি)
2. [ক্লাস ও অবজেক্ট](#ক্লাস-ও-অবজেক্ট)
3. [কনস্ট্রাক্টর](#কনস্ট্রাক্টর)
4. [এনক্যাপসুলেশন](#এনক্যাপসুলেশন)
5. [ইনহেরিট্যান্স](#ইনহেরিট্যান্স)
6. [পলিমরফিজম](#পলিমরফিজম)
7. [অ্যাবস্ট্রাকশন](#অ্যাবস্ট্রাকশন)
8. [ইন্টারফেস](#ইন্টারফেস)
9. [মিক্সিন](#মিক্সিন)
10. [এক্সটেনশন](#এক্সটেনশন)
11. [জেনেরিক্স (OOP প্রসঙ্গে)](#জেনেরিক্স)
12. [স্ট্যাটিক সদস্য](#স্ট্যাটিক-সদস্য)
13. [অপারেটর ওভারলোডিং](#অপারেটর-ওভারলোডিং)
14. [ফ্যাক্টরি কনস্ট্রাক্টর](#ফ্যাক্টরি-কনস্ট্রাক্টর)
15. [কলেবল ক্লাস](#কলেবল-ক্লাস)
16. [এনাম (Enum)](#এনাম)
17. [ডিজাইন প্যাটার্ন](#ডিজাইন-প্যাটার্ন)
18. [SOLID নীতি](#solid-নীতি)

---

## OOP পরিচিতি

### OOP কী?
অবজেক্ট-ওরিয়েন্টেড প্রোগ্রামিং হলো এমন একটি প্রোগ্রামিং পদ্ধতি যেখানে প্রোগ্রামকে বাস্তব জীবনের বস্তুর মতো করে মডেল করা হয়। প্রতিটি বস্তুর নিজস্ব তথ্য (properties/attributes) এবং কার্যক্রম (methods/behaviors) থাকে।

### OOP কেন শিখবেন?
- কোড পুনর্ব্যবহারযোগ্য হয়
- কোড রক্ষণাবেক্ষণ সহজ হয়
- বড় প্রজেক্ট সংগঠিতভাবে পরিচালনা করা যায়
- বাস্তব জীবনের সমস্যা সহজে মডেল করা যায়
- টিম ওয়ার্ক সহজ হয়

### OOP এর চারটি মূল স্তম্ভ
১. **এনক্যাপসুলেশন (Encapsulation)** – ডেটা লুকানো ও সুরক্ষা
২. **ইনহেরিট্যান্স (Inheritance)** – একটি ক্লাস থেকে আরেকটি ক্লাস তৈরি
৩. **পলিমরফিজম (Polymorphism)** – একই নামে ভিন্ন রূপ
৪. **অ্যাবস্ট্রাকশন (Abstraction)** – জটিলতা লুকানো, সহজ ইন্টারফেস দেখানো

---

## ক্লাস ও অবজেক্ট

### ক্লাস কী?
ক্লাস হলো একটি ব্লুপ্রিন্ট বা ছাঁচ যা অবজেক্টের গুণাবলী এবং আচরণ সংজ্ঞায়িত করে। ক্লাস নিজে কোনো ডেটা ধারণ করে না, শুধু কাঠামো তৈরি করে।

```dart
// ক্লাস তৈরি করা
class Car {
  // প্রপার্টি (Instance Variables)
  String brand;
  String model;
  int year;
  double price;

  // মেথড
  void startEngine() {
    print('$brand $model এর ইঞ্জিন চালু হয়েছে!');
  }

  void displayInfo() {
    print('ব্র্যান্ড: $brand');
    print('মডেল: $model');
    print('বছর: $year');
    print('মূল্য: $price টাকা');
  }
}
```

### অবজেক্ট কী?
ক্লাসের একটি নির্দিষ্ট উদাহরণ (instance) হলো অবজেক্ট। ক্লাস থেকে অবজেক্ট তৈরি করলে সেটি তার নিজস্ব ডেটা ধারণ করে।

```dart
void main() {
  // অবজেক্ট তৈরি করা (Instantiation)
  Car car1 = Car();
  car1.brand = 'Toyota';
  car1.model = 'Corolla';
  car1.year = 2022;
  car1.price = 2500000;

  Car car2 = Car();
  car2.brand = 'Honda';
  car2.model = 'Civic';
  car2.year = 2023;
  car2.price = 3000000;

  // মেথড কল করা
  car1.startEngine();   // Toyota Corolla এর ইঞ্জিন চালু হয়েছে!
  car1.displayInfo();
  car2.startEngine();   // Honda Civic এর ইঞ্জিন চালু হয়েছে!
}
```

### this কীওয়ার্ড
`this` কীওয়ার্ড বর্তমান অবজেক্টকে নির্দেশ করে। লোকাল ভেরিয়েবল ও ইনস্ট্যান্স ভেরিয়েবলের মধ্যে পার্থক্য করতে ব্যবহৃত হয়।

```dart
class Person {
  String name;
  int age;

  void setInfo(String name, int age) {
    this.name = name;  // this.name = ইনস্ট্যান্স ভেরিয়েবল
    this.age = age;    // age = প্যারামিটার
  }

  void introduce() {
    print('আমার নাম ${this.name}, আমার বয়স ${this.age}');
  }
}
```

### ইনস্ট্যান্স ভেরিয়েবল
প্রতিটি অবজেক্টের নিজস্ব কপি থাকে এমন ভেরিয়েবল।

```dart
class Student {
  String name;       // ইনস্ট্যান্স ভেরিয়েবল
  int rollNumber;    // ইনস্ট্যান্স ভেরিয়েবল
  double cgpa;       // ইনস্ট্যান্স ভেরিয়েবল

  void showDetails() {
    print('নাম: $name, রোল: $rollNumber, CGPA: $cgpa');
  }
}
```

---

## কনস্ট্রাক্টর

### কনস্ট্রাক্টর কী?
কনস্ট্রাক্টর হলো একটি বিশেষ মেথড যা অবজেক্ট তৈরির সময় স্বয়ংক্রিয়ভাবে কল হয়। এটি অবজেক্টের প্রাথমিক অবস্থা সেট করে।

### ১. ডিফল্ট কনস্ট্রাক্টর
ক্লাসে কোনো কনস্ট্রাক্টর না লিখলে ডার্ট স্বয়ংক্রিয়ভাবে একটি খালি কনস্ট্রাক্টর দেয়।

```dart
class Animal {
  String name = '';
  int age = 0;
  // ডার্ট স্বয়ংক্রিয়ভাবে Animal() {} কনস্ট্রাক্টর দেয়
}

void main() {
  Animal a = Animal(); // ডিফল্ট কনস্ট্রাক্টর কল হয়
  a.name = 'বিড়াল';
  a.age = 3;
}
```

### ২. প্যারামিটারাইজড কনস্ট্রাক্টর
প্যারামিটার গ্রহণ করে এমন কনস্ট্রাক্টর।

```dart
class Rectangle {
  double width;
  double height;

  // প্যারামিটারাইজড কনস্ট্রাক্টর
  Rectangle(double width, double height) {
    this.width = width;
    this.height = height;
  }

  double area() {
    return width * height;
  }
}

void main() {
  Rectangle rect = Rectangle(10.0, 5.0);
  print('ক্ষেত্রফল: ${rect.area()}'); // ক্ষেত্রফল: 50.0
}
```

### ৩. শর্টহ্যান্ড কনস্ট্রাক্টর (Initializer List)
ডার্টের বিশেষ সুবিধা – কনস্ট্রাক্টর প্যারামিটার সরাসরি ইনস্ট্যান্স ভেরিয়েবলে নির্ধারণ করা।

```dart
class Circle {
  double radius;
  String color;

  // শর্টহ্যান্ড কনস্ট্রাক্টর
  Circle(this.radius, this.color);

  double area() => 3.14159 * radius * radius;
  double circumference() => 2 * 3.14159 * radius;
}

void main() {
  Circle c = Circle(5.0, 'লাল');
  print('ক্ষেত্রফল: ${c.area()}');
  print('পরিধি: ${c.circumference()}');
}
```

### ৪. নামযুক্ত কনস্ট্রাক্টর (Named Constructor)
একই ক্লাসে একাধিক কনস্ট্রাক্টর তৈরি করা যায়।

```dart
class Temperature {
  double celsius;

  // ডিফল্ট কনস্ট্রাক্টর
  Temperature(this.celsius);

  // নামযুক্ত কনস্ট্রাক্টর – ফারেনহাইট থেকে
  Temperature.fromFahrenheit(double fahrenheit)
      : celsius = (fahrenheit - 32) * 5 / 9;

  // নামযুক্ত কনস্ট্রাক্টর – কেলভিন থেকে
  Temperature.fromKelvin(double kelvin)
      : celsius = kelvin - 273.15;

  double toFahrenheit() => celsius * 9 / 5 + 32;
  double toKelvin() => celsius + 273.15;

  @override
  String toString() => '$celsius°C';
}

void main() {
  Temperature t1 = Temperature(100);                    // সেলসিয়াস
  Temperature t2 = Temperature.fromFahrenheit(212);     // ফারেনহাইট থেকে
  Temperature t3 = Temperature.fromKelvin(373.15);      // কেলভিন থেকে

  print(t1); // 100.0°C
  print(t2); // 100.0°C
  print(t3); // 100.0°C
}
```

### ৫. কনস্ট্যান্ট কনস্ট্রাক্টর (Const Constructor)
কম্পাইল-টাইমে কনস্ট্যান্ট অবজেক্ট তৈরি করে।

```dart
class Point {
  final double x;
  final double y;

  const Point(this.x, this.y);

  double distanceTo(Point other) {
    double dx = x - other.x;
    double dy = y - other.y;
    return (dx * dx + dy * dy);
  }
}

void main() {
  const Point p1 = Point(0, 0);
  const Point p2 = Point(3, 4);
  print('দূরত্বের বর্গ: ${p1.distanceTo(p2)}'); // 25.0
}
```

### ৬. Initializer List
কনস্ট্রাক্টর বডির আগে ভেরিয়েবল ইনিশিয়ালাইজ করা।

```dart
class BankAccount {
  final String accountNumber;
  final String holderName;
  double balance;

  BankAccount(String accountNum, String name, double initialBalance)
      : accountNumber = accountNum,      // initializer list
        holderName = name,
        balance = initialBalance {
    print('অ্যাকাউন্ট খোলা হয়েছে: $accountNumber');
  }

  void deposit(double amount) {
    balance += amount;
    print('জমা: $amount টাকা। বর্তমান ব্যালেন্স: $balance');
  }

  void withdraw(double amount) {
    if (amount <= balance) {
      balance -= amount;
      print('উত্তোলন: $amount টাকা। বর্তমান ব্যালেন্স: $balance');
    } else {
      print('অপর্যাপ্ত ব্যালেন্স!');
    }
  }
}
```

### ৭. Redirecting Constructor
একটি কনস্ট্রাক্টর থেকে অন্য কনস্ট্রাক্টরে পুনর্নির্দেশ করা।

```dart
class Employee {
  String name;
  String department;
  double salary;

  Employee(this.name, this.department, this.salary);

  // Redirecting constructor
  Employee.intern(String name) : this(name, 'Internship', 15000);
  Employee.manager(String name) : this(name, 'Management', 80000);
}

void main() {
  Employee emp1 = Employee('করিম', 'Engineering', 50000);
  Employee intern = Employee.intern('রহিম');
  Employee mgr = Employee.manager('সুমাইয়া');

  print('${emp1.name} - ${emp1.department} - ${emp1.salary}');
  print('${intern.name} - ${intern.department} - ${intern.salary}');
  print('${mgr.name} - ${mgr.department} - ${mgr.salary}');
}
```

---

## এনক্যাপসুলেশন

### এনক্যাপসুলেশন কী?
ডেটা এবং মেথড একসাথে বাঁধাই করে ডেটা বাইরে থেকে সরাসরি পরিবর্তন হতে রক্ষা করার প্রক্রিয়া।

### প্রাইভেট সদস্য (Private Members)
ডার্টে আন্ডারস্কোর `_` দিয়ে প্রাইভেট সদস্য তৈরি করা হয়। এটি শুধু একই লাইব্রেরি/ফাইলের মধ্যে অ্যাক্সেসযোগ্য।

```dart
class BankAccount {
  String _accountNumber;  // প্রাইভেট
  double _balance;        // প্রাইভেট
  String holderName;      // পাবলিক

  BankAccount(this._accountNumber, this.holderName, this._balance);

  // প্রাইভেট মেথড
  bool _isValidAmount(double amount) {
    return amount > 0;
  }

  // পাবলিক মেথড – নিয়ন্ত্রিত অ্যাক্সেস
  void deposit(double amount) {
    if (_isValidAmount(amount)) {
      _balance += amount;
      print('জমা সফল। ব্যালেন্স: $_balance');
    } else {
      print('অবৈধ পরিমাণ!');
    }
  }

  void withdraw(double amount) {
    if (_isValidAmount(amount) && amount <= _balance) {
      _balance -= amount;
      print('উত্তোলন সফল। ব্যালেন্স: $_balance');
    } else {
      print('লেনদেন ব্যর্থ!');
    }
  }
}
```

### Getter ও Setter
প্রাইভেট ভেরিয়েবলে নিয়ন্ত্রিত অ্যাক্সেস প্রদান করে।

```dart
class Person {
  String _name;
  int _age;

  Person(this._name, this._age);

  // Getter
  String get name => _name;
  int get age => _age;

  // Getter – গণনা করা প্রপার্টি
  String get info => '$_name (বয়স: $_age)';

  // Setter – যাচাই সহ
  set name(String value) {
    if (value.isNotEmpty) {
      _name = value;
    } else {
      print('নাম খালি হতে পারবে না!');
    }
  }

  set age(int value) {
    if (value >= 0 && value <= 150) {
      _age = value;
    } else {
      print('অবৈধ বয়স!');
    }
  }
}

void main() {
  Person p = Person('আলী', 25);

  // Getter ব্যবহার
  print(p.name);   // আলী
  print(p.age);    // 25
  print(p.info);   // আলী (বয়স: 25)

  // Setter ব্যবহার
  p.name = 'করিম';
  p.age = 30;
  p.age = -5;  // অবৈধ বয়স!

  print(p.info); // করিম (বয়স: 30)
}
```

### এনক্যাপসুলেশনের সুবিধা
- ডেটা সুরক্ষিত থাকে
- কোড পরিবর্তন সহজ হয়
- অবৈধ ডেটা প্রবেশ রোধ করা যায়
- কোডের নির্ভরযোগ্যতা বাড়ে

---

## ইনহেরিট্যান্স

### ইনহেরিট্যান্স কী?
একটি ক্লাস (চাইল্ড/সাব ক্লাস) অন্য একটি ক্লাসের (প্যারেন্ট/সুপার ক্লাস) প্রপার্টি ও মেথড গ্রহণ করার প্রক্রিয়া। `extends` কীওয়ার্ড ব্যবহার করা হয়।

```dart
// প্যারেন্ট/বেস ক্লাস
class Animal {
  String name;
  int age;
  String sound;

  Animal(this.name, this.age, this.sound);

  void makeSound() {
    print('$name বলছে: $sound');
  }

  void breathe() {
    print('$name শ্বাস নিচ্ছে...');
  }

  void eat() {
    print('$name খাচ্ছে...');
  }

  @override
  String toString() => 'প্রাণী: $name, বয়স: $age';
}

// চাইল্ড ক্লাস – Animal থেকে ইনহেরিট করে
class Dog extends Animal {
  String breed;

  Dog(String name, int age, this.breed) : super(name, age, 'ঘেউ ঘেউ');

  void fetch() {
    print('$name বল আনছে!');
  }

  void wag() {
    print('$name লেজ নাড়ছে!');
  }
}

// আরেকটি চাইল্ড ক্লাস
class Cat extends Animal {
  bool isIndoor;

  Cat(String name, int age, this.isIndoor) : super(name, age, 'মিয়াও');

  void purr() {
    print('$name গর্গর শব্দ করছে...');
  }

  void scratch() {
    print('$name আঁচড় দিচ্ছে!');
  }
}

void main() {
  Dog dog = Dog('বাদল', 3, 'Labrador');
  Cat cat = Cat('মিনি', 2, true);

  // ইনহেরিট করা মেথড
  dog.makeSound();  // বাদল বলছে: ঘেউ ঘেউ
  dog.eat();        // বাদল খাচ্ছে...
  dog.breathe();    // বাদল শ্বাস নিচ্ছে...

  // নিজস্ব মেথড
  dog.fetch();      // বাদল বল আনছে!
  dog.wag();        // বাদল লেজ নাড়ছে!

  cat.makeSound();  // মিনি বলছে: মিয়াও
  cat.purr();       // মিনি গর্গর শব্দ করছে...
}
```

### super কীওয়ার্ড
প্যারেন্ট ক্লাসের মেথড বা কনস্ট্রাক্টর অ্যাক্সেস করতে ব্যবহৃত হয়।

```dart
class Vehicle {
  String brand;
  int speed;

  Vehicle(this.brand, this.speed);

  void move() {
    print('$brand চলছে, গতি: $speed km/h');
  }

  String getInfo() => 'যানবাহন: $brand';
}

class ElectricCar extends Vehicle {
  int batteryLevel;

  ElectricCar(String brand, int speed, this.batteryLevel)
      : super(brand, speed);  // প্যারেন্ট কনস্ট্রাক্টর কল

  @override
  void move() {
    super.move();  // প্যারেন্টের move() কল করা
    print('ব্যাটারি ব্যবহার হচ্ছে: $batteryLevel%');
  }

  @override
  String getInfo() {
    return '${super.getInfo()}, ব্যাটারি: $batteryLevel%';
  }
}

void main() {
  ElectricCar tesla = ElectricCar('Tesla', 200, 85);
  tesla.move();
  print(tesla.getInfo());
}
```

### মাল্টি-লেভেল ইনহেরিট্যান্স
ডার্টে একাধিক স্তরে ইনহেরিট্যান্স সম্ভব।

```dart
class LivingBeing {
  void breathe() => print('শ্বাস নিচ্ছি...');
  void grow() => print('বড় হচ্ছি...');
}

class Animal2 extends LivingBeing {
  String name;
  Animal2(this.name);

  void move() => print('$name নড়াচড়া করছে...');
}

class Mammal extends Animal2 {
  Mammal(String name) : super(name);

  void feedMilk() => print('$name দুধ পান করাচ্ছে...');
}

class Human extends Mammal {
  String profession;
  Human(String name, this.profession) : super(name);

  void think() => print('$name ($profession) চিন্তা করছে...');
  void speak() => print('$name কথা বলছে...');
}

void main() {
  Human h = Human('রহিম', 'ডাক্তার');
  h.breathe();    // LivingBeing থেকে
  h.grow();       // LivingBeing থেকে
  h.move();       // Animal2 থেকে
  h.feedMilk();   // Mammal থেকে
  h.think();      // Human নিজস্ব
  h.speak();      // Human নিজস্ব
}
```

### ইনহেরিট্যান্সের সুবিধা
- কোড পুনর্ব্যবহারযোগ্যতা বাড়ে
- কোড ডুপ্লিকেশন কমে
- কোডের কাঠামো পরিষ্কার থাকে
- সহজে নতুন ফিচার যোগ করা যায়

---

## পলিমরফিজম

### পলিমরফিজম কী?
"পলি" মানে অনেক, "মরফ" মানে রূপ। একই নামের মেথড বিভিন্ন ক্লাসে ভিন্নভাবে কাজ করতে পারে।

### মেথড ওভাররাইডিং (Method Overriding)
চাইল্ড ক্লাসে প্যারেন্ট ক্লাসের মেথড পুনর্সংজ্ঞায়িত করা।

```dart
class Shape {
  String color;

  Shape(this.color);

  double area() => 0.0;  // বেস মেথড

  double perimeter() => 0.0;

  void display() {
    print('আকার: ${runtimeType}, রং: $color');
    print('ক্ষেত্রফল: ${area()}');
    print('পরিসীমা: ${perimeter()}');
  }
}

class Rectangle2 extends Shape {
  double width;
  double height;

  Rectangle2(String color, this.width, this.height) : super(color);

  @override
  double area() => width * height;  // ওভাররাইড

  @override
  double perimeter() => 2 * (width + height);
}

class Circle2 extends Shape {
  double radius;

  Circle2(String color, this.radius) : super(color);

  @override
  double area() => 3.14159 * radius * radius;  // ওভাররাইড

  @override
  double perimeter() => 2 * 3.14159 * radius;
}

class Triangle extends Shape {
  double base;
  double height;
  double sideA;
  double sideB;
  double sideC;

  Triangle(String color, this.base, this.height, this.sideA, this.sideB, this.sideC)
      : super(color);

  @override
  double area() => 0.5 * base * height;  // ওভাররাইড

  @override
  double perimeter() => sideA + sideB + sideC;
}

void main() {
  List<Shape> shapes = [
    Rectangle2('লাল', 10, 5),
    Circle2('নীল', 7),
    Triangle('সবুজ', 8, 6, 8, 10, 6),
  ];

  for (Shape shape in shapes) {
    shape.display();  // প্রতিটি ভিন্নভাবে কাজ করে
    print('---');
  }
}
```

### রানটাইম পলিমরফিজম
প্রোগ্রাম চলাকালীন সঠিক মেথড নির্বাচন হয়।

```dart
class Payment {
  void processPayment(double amount) {
    print('পেমেন্ট প্রক্রিয়া করা হচ্ছে: $amount টাকা');
  }
}

class CreditCardPayment extends Payment {
  String cardNumber;

  CreditCardPayment(this.cardNumber);

  @override
  void processPayment(double amount) {
    print('ক্রেডিট কার্ড ($cardNumber) দিয়ে $amount টাকা পেমেন্ট করা হলো');
  }
}

class MobilePayment extends Payment {
  String phoneNumber;

  MobilePayment(this.phoneNumber);

  @override
  void processPayment(double amount) {
    print('মোবাইল ব্যাংকিং ($phoneNumber) দিয়ে $amount টাকা পেমেন্ট করা হলো');
  }
}

class CashPayment extends Payment {
  @override
  void processPayment(double amount) {
    print('নগদ $amount টাকা পেমেন্ট করা হলো');
  }
}

void processOrder(Payment payment, double amount) {
  payment.processPayment(amount);  // রানটাইমে সঠিক মেথড কল হয়
}

void main() {
  processOrder(CreditCardPayment('1234-5678-9012'), 1500.0);
  processOrder(MobilePayment('01712345678'), 800.0);
  processOrder(CashPayment(), 500.0);
}
```

---

## অ্যাবস্ট্রাকশন

### অ্যাবস্ট্রাকশন কী?
জটিল বাস্তবায়নের বিবরণ লুকিয়ে শুধু প্রয়োজনীয় বৈশিষ্ট্য দেখানো। ব্যবহারকারী জানে "কী করে" কিন্তু "কীভাবে করে" তা জানা দরকার নেই।

### অ্যাবস্ট্রাক্ট ক্লাস
অ্যাবস্ট্রাক্ট ক্লাস থেকে সরাসরি অবজেক্ট তৈরি করা যায় না। এটি সাব-ক্লাসের জন্য ব্লুপ্রিন্ট হিসেবে কাজ করে।

```dart
abstract class Database {
  // অ্যাবস্ট্রাক্ট মেথড – বাস্তবায়ন নেই
  void connect(String connectionString);
  void disconnect();
  List<Map> query(String sql);
  void execute(String sql);

  // কংক্রিট মেথড – বাস্তবায়ন আছে
  void printStatus() {
    print('ডেটাবেজ সংযুক্ত।');
  }
}

class MySQLDatabase extends Database {
  String? _connectionString;

  @override
  void connect(String connectionString) {
    _connectionString = connectionString;
    print('MySQL-এ সংযুক্ত হয়েছে: $connectionString');
  }

  @override
  void disconnect() {
    print('MySQL সংযোগ বিচ্ছিন্ন হয়েছে।');
    _connectionString = null;
  }

  @override
  List<Map> query(String sql) {
    print('MySQL Query চালানো হচ্ছে: $sql');
    return [{'id': 1, 'name': 'Alice'}];
  }

  @override
  void execute(String sql) {
    print('MySQL Execute: $sql');
  }
}

class PostgreSQLDatabase extends Database {
  @override
  void connect(String connectionString) {
    print('PostgreSQL-এ সংযুক্ত হয়েছে: $connectionString');
  }

  @override
  void disconnect() {
    print('PostgreSQL সংযোগ বিচ্ছিন্ন হয়েছে।');
  }

  @override
  List<Map> query(String sql) {
    print('PostgreSQL Query: $sql');
    return [];
  }

  @override
  void execute(String sql) {
    print('PostgreSQL Execute: $sql');
  }
}

void main() {
  Database db = MySQLDatabase();
  db.connect('localhost:3306/mydb');
  db.printStatus();
  var results = db.query('SELECT * FROM users');
  print(results);
  db.disconnect();
}
```

### অ্যাবস্ট্রাক্ট মেথড
শুধু সিগনেচার থাকে, বাস্তবায়ন নেই – সাব-ক্লাসকে বাস্তবায়ন করতে বাধ্য করে।

```dart
abstract class Notification {
  String title;
  String message;

  Notification(this.title, this.message);

  // অ্যাবস্ট্রাক্ট মেথড
  void send();
  void schedule(DateTime dateTime);

  // কংক্রিট মেথড
  void log() {
    print('নোটিফিকেশন লগ করা হয়েছে: $title');
  }
}

class EmailNotification extends Notification {
  String email;

  EmailNotification(String title, String message, this.email)
      : super(title, message);

  @override
  void send() {
    print('ইমেইল পাঠানো হয়েছে $email এ: $title - $message');
  }

  @override
  void schedule(DateTime dateTime) {
    print('ইমেইল শিডিউল করা হয়েছে: $dateTime');
  }
}

class SMSNotification extends Notification {
  String phoneNumber;

  SMSNotification(String title, String message, this.phoneNumber)
      : super(title, message);

  @override
  void send() {
    print('SMS পাঠানো হয়েছে $phoneNumber এ: $message');
  }

  @override
  void schedule(DateTime dateTime) {
    print('SMS শিডিউল করা হয়েছে: $dateTime');
  }
}

class PushNotification extends Notification {
  String deviceToken;

  PushNotification(String title, String message, this.deviceToken)
      : super(title, message);

  @override
  void send() {
    print('Push নোটিফিকেশন পাঠানো হয়েছে ডিভাইসে ($deviceToken): $title');
  }

  @override
  void schedule(DateTime dateTime) {
    print('Push নোটিফিকেশন শিডিউল: $dateTime');
  }
}
```

---

## ইন্টারফেস

### ইন্টারফেস কী?
ডার্টে আলাদা `interface` কীওয়ার্ড নেই। যেকোনো ক্লাসই ইন্টারফেস হিসেবে ব্যবহার করা যায়। `implements` কীওয়ার্ড দিয়ে ইন্টারফেস বাস্তবায়ন করা হয়।

### ইন্টারফেস বাস্তবায়ন

```dart
// ইন্টারফেস হিসেবে ব্যবহার
class Printable {
  void print() {}
  void printPreview() {}
}

class Saveable {
  void save() {}
  void saveAs(String path) {}
}

class Shareable {
  void share() {}
  void shareWith(List<String> users) {}
}

// একাধিক ইন্টারফেস বাস্তবায়ন
class Document implements Printable, Saveable, Shareable {
  String title;
  String content;

  Document(this.title, this.content);

  @override
  void print() {
    print('নথি প্রিন্ট হচ্ছে: $title');
  }

  @override
  void printPreview() {
    print('প্রিভিউ: $content');
  }

  @override
  void save() {
    print('নথি সংরক্ষণ হচ্ছে: $title');
  }

  @override
  void saveAs(String path) {
    print('নথি সংরক্ষণ হচ্ছে $path তে');
  }

  @override
  void share() {
    print('নথি শেয়ার হচ্ছে: $title');
  }

  @override
  void shareWith(List<String> users) {
    print('নথি শেয়ার হচ্ছে ${users.join(", ")} এর সাথে');
  }
}
```

### ইন্টারফেস বনাম অ্যাবস্ট্রাক্ট ক্লাস

| বৈশিষ্ট্য | ইন্টারফেস (implements) | অ্যাবস্ট্রাক্ট ক্লাস (extends) |
|-----------|----------------------|-------------------------------|
| একাধিক | হ্যাঁ, একাধিক সম্ভব | না, শুধু একটি |
| কনস্ট্রাক্টর | না | হ্যাঁ |
| কংক্রিট মেথড | না (সব ওভাররাইড করতে হবে) | হ্যাঁ |
| ব্যবহার | চুক্তি/কন্ট্র্যাক্ট নির্ধারণে | আংশিক বাস্তবায়নে |

```dart
// ইন্টারফেস হিসেবে ব্যবহারের ভালো উদাহরণ
abstract class Flyable {
  void fly();
  void land();
  double get maxAltitude;
}

abstract class Swimmable {
  void swim();
  void dive();
  double get maxDepth;
}

class Duck implements Flyable, Swimmable {
  @override
  void fly() => print('হাঁস উড়ছে!');

  @override
  void land() => print('হাঁস অবতরণ করছে!');

  @override
  double get maxAltitude => 100.0;

  @override
  void swim() => print('হাঁস সাঁতার কাটছে!');

  @override
  void dive() => print('হাঁস ডুব দিচ্ছে!');

  @override
  double get maxDepth => 1.5;
}
```

---

## মিক্সিন

### মিক্সিন কী?
মিক্সিন হলো কোড পুনর্ব্যবহারের একটি পদ্ধতি যা একাধিক ক্লাস হায়ারার্কি জুড়ে কাজ করে। `mixin` কীওয়ার্ড দিয়ে তৈরি এবং `with` কীওয়ার্ড দিয়ে ব্যবহার করা হয়।

```dart
// মিক্সিন তৈরি করা
mixin Swimming {
  void swim() => print('সাঁতার কাটছি...');
  void floatOnWater() => print('পানিতে ভাসছি...');
}

mixin Flying {
  void fly() => print('উড়ছি...');
  void glide() => print('গ্লাইড করছি...');
}

mixin Running {
  void run() => print('দৌড়াচ্ছি...');
  void sprint() => print('দ্রুত দৌড়াচ্ছি...');
}

mixin Singing {
  void sing() => print('গান গাইছি...');
}

// ক্লাসে মিক্সিন ব্যবহার
class Duck2 extends Animal with Swimming, Flying {
  Duck2(String name) : super(name, 2, 'কুয়াক');
}

class Fish extends Animal with Swimming {
  Fish(String name) : super(name, 1, '...');
}

class Eagle extends Animal with Flying, Running {
  Eagle(String name) : super(name, 5, 'কী কী');
}

class Human2 extends Animal with Running, Swimming, Singing {
  Human2(String name) : super(name, 25, '...');
}

void main() {
  Duck2 duck = Duck2('ডাক ডাক');
  duck.swim();   // Swimming থেকে
  duck.fly();    // Flying থেকে
  duck.makeSound(); // Animal থেকে

  Human2 human = Human2('রফিক');
  human.run();   // Running থেকে
  human.swim();  // Swimming থেকে
  human.sing();  // Singing থেকে
}
```

### on কীওয়ার্ড সহ মিক্সিন
নির্দিষ্ট ক্লাসের সাথে মিক্সিন সীমাবদ্ধ করা।

```dart
class Logger {
  void log(String message) {
    print('[LOG] $message');
  }
}

// শুধু Logger ক্লাসে ব্যবহারযোগ্য মিক্সিন
mixin TimestampLogger on Logger {
  void logWithTime(String message) {
    log('[${DateTime.now()}] $message');
  }
}

class AppLogger extends Logger with TimestampLogger {
  void start() {
    log('অ্যাপ শুরু হচ্ছে...');
    logWithTime('টাইমস্ট্যাম্প সহ লগ');
  }
}
```

### মিক্সিনের সুবিধা
- একাধিক ক্লাস থেকে কোড পুনর্ব্যবহার
- ইনহেরিট্যান্সের সীমাবদ্ধতা কাটানো
- কোড মডুলার হয়

---

## এক্সটেনশন

### এক্সটেনশন কী?
বিদ্যমান ক্লাস পরিবর্তন না করে নতুন ফাংশনালিটি যোগ করা। তৃতীয় পক্ষের ক্লাসেও এক্সটেনশন যোগ করা যায়।

```dart
// String-এ এক্সটেনশন
extension StringExtension on String {
  // প্রথম অক্ষর বড় করা
  String capitalize() {
    if (isEmpty) return '';
    return '${this[0].toUpperCase()}${substring(1).toLowerCase()}';
  }

  // প্রতিটি শব্দের প্রথম অক্ষর বড় করা
  String toTitleCase() {
    return split(' ').map((word) => word.capitalize()).join(' ');
  }

  // ইমেইল যাচাই
  bool get isValidEmail {
    return RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(this);
  }

  // ফোন নম্বর যাচাই
  bool get isValidPhone {
    return RegExp(r'^(\+88)?01[3-9]\d{8}$').hasMatch(this);
  }

  // প্যালিনড্রোম যাচাই
  bool get isPalindrome {
    String cleaned = toLowerCase().replaceAll(' ', '');
    return cleaned == cleaned.split('').reversed.join('');
  }

  // শব্দ গণনা
  int get wordCount => trim().isEmpty ? 0 : trim().split(RegExp(r'\s+')).length;
}

// int-এ এক্সটেনশন
extension IntExtension on int {
  bool get isEven => this % 2 == 0;
  bool get isOdd => this % 2 != 0;
  bool get isPrime {
    if (this < 2) return false;
    for (int i = 2; i <= this ~/ 2; i++) {
      if (this % i == 0) return false;
    }
    return true;
  }
  int factorial() {
    if (this <= 1) return 1;
    return this * (this - 1).factorial();
  }
}

// List-এ এক্সটেনশন
extension ListExtension<T> on List<T> {
  T? get firstOrNull => isEmpty ? null : first;
  T? get lastOrNull => isEmpty ? null : last;

  List<T> unique() => toSet().toList();
}

void main() {
  // String এক্সটেনশন
  print('hello world'.capitalize());       // Hello world
  print('hello world'.toTitleCase());      // Hello World
  print('user@email.com'.isValidEmail);    // true
  print('racecar'.isPalindrome);           // true
  print('hello world dart'.wordCount);     // 3

  // int এক্সটেনশন
  print(7.isPrime);      // true
  print(5.factorial());  // 120
  print(4.isEven);       // true

  // List এক্সটেনশন
  List<int> nums = [1, 2, 2, 3, 3, 4];
  print(nums.unique());  // [1, 2, 3, 4]
}
```

---

## জেনেরিক্স

### OOP-এ জেনেরিক্স
জেনেরিক ক্লাস এবং মেথড তৈরি করা যা বিভিন্ন টাইপে কাজ করে।

```dart
// জেনেরিক ক্লাস
class Stack<T> {
  final List<T> _items = [];

  void push(T item) {
    _items.add(item);
    print('যোগ করা হয়েছে: $item');
  }

  T pop() {
    if (isEmpty) throw Exception('Stack খালি!');
    T item = _items.removeLast();
    print('সরানো হয়েছে: $item');
    return item;
  }

  T get peek => isEmpty ? throw Exception('Stack খালি!') : _items.last;

  bool get isEmpty => _items.isEmpty;
  int get size => _items.length;

  @override
  String toString() => 'Stack: $_items';
}

// জেনেরিক Pair ক্লাস
class Pair<A, B> {
  final A first;
  final B second;

  Pair(this.first, this.second);

  Pair<B, A> swap() => Pair(second, first);

  @override
  String toString() => '($first, $second)';
}

// জেনেরিক Result ক্লাস
class Result<T> {
  final T? data;
  final String? error;
  final bool isSuccess;

  Result.success(this.data)
      : error = null,
        isSuccess = true;

  Result.failure(this.error)
      : data = null,
        isSuccess = false;

  @override
  String toString() => isSuccess ? 'সফল: $data' : 'ব্যর্থ: $error';
}

void main() {
  // জেনেরিক Stack
  Stack<int> intStack = Stack<int>();
  intStack.push(1);
  intStack.push(2);
  intStack.push(3);
  print(intStack.pop());
  print(intStack);

  Stack<String> stringStack = Stack<String>();
  stringStack.push('ডার্ট');
  stringStack.push('ফ্লাটার');
  print(stringStack);

  // Pair
  Pair<String, int> pair = Pair('বয়স', 25);
  print(pair);        // (বয়স, 25)
  print(pair.swap()); // (25, বয়স)

  // Result
  Result<String> success = Result.success('ডেটা লোড হয়েছে');
  Result<String> failure = Result.failure('নেটওয়ার্ক ত্রুটি');
  print(success);
  print(failure);
}
```

### জেনেরিক মেথড

```dart
class Utility {
  // জেনেরিক মেথড
  static T findMax<T extends Comparable<T>>(List<T> items) {
    if (items.isEmpty) throw Exception('লিস্ট খালি!');
    T max = items[0];
    for (T item in items) {
      if (item.compareTo(max) > 0) max = item;
    }
    return max;
  }

  static List<T> filter<T>(List<T> items, bool Function(T) predicate) {
    return items.where(predicate).toList();
  }

  static Map<K, V> fromLists<K, V>(List<K> keys, List<V> values) {
    Map<K, V> result = {};
    for (int i = 0; i < keys.length; i++) {
      result[keys[i]] = values[i];
    }
    return result;
  }
}

void main() {
  print(Utility.findMax([3, 1, 4, 1, 5, 9]));         // 9
  print(Utility.findMax(['apple', 'mango', 'banana'])); // mango

  List<int> evens = Utility.filter([1,2,3,4,5,6], (n) => n % 2 == 0);
  print(evens); // [2, 4, 6]
}
```

---

## স্ট্যাটিক সদস্য

### স্ট্যাটিক প্রপার্টি ও মেথড
ইনস্ট্যান্স তৈরি না করেই ক্লাসের মাধ্যমে সরাসরি অ্যাক্সেসযোগ্য।

```dart
class MathHelper {
  // স্ট্যাটিক কনস্ট্যান্ট
  static const double pi = 3.14159265358979;
  static const double e = 2.71828182845904;
  static const double goldenRatio = 1.61803398874989;

  // স্ট্যাটিক মেথড
  static double circleArea(double radius) => pi * radius * radius;
  static double sphereVolume(double radius) => (4/3) * pi * radius * radius * radius;
  static int factorial(int n) => n <= 1 ? 1 : n * factorial(n - 1);
  static bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i <= n ~/ 2; i++) {
      if (n % i == 0) return false;
    }
    return true;
  }
  static int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
  }
}

class Counter {
  static int _count = 0;  // স্ট্যাটিক ভেরিয়েবল
  int id;

  Counter() : id = ++_count;

  static int get totalCount => _count;
  static void reset() => _count = 0;
}

void main() {
  print(MathHelper.circleArea(5));   // 78.539...
  print(MathHelper.factorial(10));   // 3628800
  print(MathHelper.isPrime(17));     // true
  print(MathHelper.fibonacci(10));   // 55

  Counter c1 = Counter();
  Counter c2 = Counter();
  Counter c3 = Counter();
  print('মোট: ${Counter.totalCount}'); // মোট: 3
  Counter.reset();
  print('রিসেটের পর: ${Counter.totalCount}'); // 0
}
```

---

## অপারেটর ওভারলোডিং

### অপারেটর ওভারলোডিং কী?
বিল্ট-ইন অপারেটর (`+`, `-`, `*`, `==` ইত্যাদি) কাস্টম ক্লাসের জন্য পুনর্সংজ্ঞায়িত করা।

```dart
class Vector {
  double x;
  double y;
  double z;

  Vector(this.x, this.y, this.z);

  // যোগ অপারেটর
  Vector operator +(Vector other) {
    return Vector(x + other.x, y + other.y, z + other.z);
  }

  // বিয়োগ অপারেটর
  Vector operator -(Vector other) {
    return Vector(x - other.x, y - other.y, z - other.z);
  }

  // গুণ অপারেটর (স্কেলার)
  Vector operator *(double scalar) {
    return Vector(x * scalar, y * scalar, z * scalar);
  }

  // সমতা অপারেটর
  @override
  bool operator ==(Object other) {
    if (other is Vector) {
      return x == other.x && y == other.y && z == other.z;
    }
    return false;
  }

  // ইন্ডেক্স অপারেটর
  double operator [](int index) {
    switch (index) {
      case 0: return x;
      case 1: return y;
      case 2: return z;
      default: throw RangeError('ইন্ডেক্স 0-2 এর মধ্যে হতে হবে');
    }
  }

  // ম্যাগনিচুড
  double get magnitude => (x*x + y*y + z*z);

  // ডট প্রোডাক্ট
  double dot(Vector other) => x*other.x + y*other.y + z*other.z;

  @override
  int get hashCode => Object.hash(x, y, z);

  @override
  String toString() => 'Vector($x, $y, $z)';
}

class Money {
  double amount;
  String currency;

  Money(this.amount, this.currency);

  Money operator +(Money other) {
    if (currency != other.currency) {
      throw Exception('ভিন্ন মুদ্রা যোগ করা যাবে না!');
    }
    return Money(amount + other.amount, currency);
  }

  bool operator >(Money other) => amount > other.amount;
  bool operator <(Money other) => amount < other.amount;

  @override
  String toString() => '$amount $currency';
}

void main() {
  Vector v1 = Vector(1, 2, 3);
  Vector v2 = Vector(4, 5, 6);

  print(v1 + v2);    // Vector(5.0, 7.0, 9.0)
  print(v1 - v2);    // Vector(-3.0, -3.0, -3.0)
  print(v1 * 2);     // Vector(2.0, 4.0, 6.0)
  print(v1 == v2);   // false
  print(v1[0]);      // 1.0

  Money m1 = Money(500, 'BDT');
  Money m2 = Money(300, 'BDT');
  print(m1 + m2);    // 800.0 BDT
  print(m1 > m2);    // true
}
```

---

## ফ্যাক্টরি কনস্ট্রাক্টর

### ফ্যাক্টরি কনস্ট্রাক্টর কী?
সবসময় নতুন ইনস্ট্যান্স তৈরি না করে বিদ্যমান ইনস্ট্যান্স ফেরত দিতে বা বিভিন্ন লজিকে অবজেক্ট তৈরি করতে পারে।

```dart
class Logger2 {
  static Logger2? _instance;
  String _name;

  // প্রাইভেট কনস্ট্রাক্টর
  Logger2._internal(this._name);

  // ফ্যাক্টরি কনস্ট্রাক্টর – Singleton প্যাটার্ন
  factory Logger2(String name) {
    _instance ??= Logger2._internal(name);
    return _instance!;
  }

  void log(String message) {
    print('[$_name] $message');
  }
}

// ফ্যাক্টরি দিয়ে JSON থেকে অবজেক্ট তৈরি
class User {
  String name;
  String email;
  int age;
  String role;

  User({
    required this.name,
    required this.email,
    required this.age,
    required this.role,
  });

  // JSON থেকে User তৈরি
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      name: json['name'] ?? '',
      email: json['email'] ?? '',
      age: json['age'] ?? 0,
      role: json['role'] ?? 'user',
    );
  }

  // প্রশাসক তৈরির ফ্যাক্টরি
  factory User.admin(String name, String email) {
    return User(
      name: name,
      email: email,
      age: 0,
      role: 'admin',
    );
  }

  // অতিথি তৈরির ফ্যাক্টরি
  factory User.guest() {
    return User(
      name: 'অতিথি',
      email: 'guest@example.com',
      age: 0,
      role: 'guest',
    );
  }

  Map<String, dynamic> toJson() {
    return {'name': name, 'email': email, 'age': age, 'role': role};
  }

  @override
  String toString() => 'User(name: $name, role: $role)';
}

void main() {
  // Singleton
  Logger2 log1 = Logger2('অ্যাপ');
  Logger2 log2 = Logger2('ডেটাবেজ');
  print(identical(log1, log2)); // true – একই ইনস্ট্যান্স

  // JSON থেকে
  Map<String, dynamic> json = {
    'name': 'করিম',
    'email': 'karim@email.com',
    'age': 30,
    'role': 'user',
  };
  User user = User.fromJson(json);
  print(user); // User(name: করিম, role: user)

  User admin = User.admin('সুমাইয়া', 'admin@app.com');
  User guest = User.guest();
  print(admin);
  print(guest);
}
```

---

## কলেবল ক্লাস

### কলেবল ক্লাস কী?
`call()` মেথড সংজ্ঞায়িত করে ক্লাসকে ফাংশনের মতো কল করা যায়।

```dart
class Multiplier {
  double factor;

  Multiplier(this.factor);

  // call মেথড – ক্লাসকে ফাংশনের মতো কল করা যায়
  double call(double value) {
    return value * factor;
  }
}

class Validator {
  bool call(String value) {
    return value.isNotEmpty && value.length >= 3;
  }
}

class Calculator {
  double call(double a, String operator, double b) {
    switch (operator) {
      case '+': return a + b;
      case '-': return a - b;
      case '*': return a * b;
      case '/': return b != 0 ? a / b : throw Exception('শূন্য দিয়ে ভাগ!');
      default: throw Exception('অবৈধ অপারেটর!');
    }
  }
}

void main() {
  Multiplier double_ = Multiplier(2);
  Multiplier triple = Multiplier(3);

  print(double_(5));   // 10.0 – ফাংশনের মতো কল
  print(triple(5));    // 15.0

  Validator validate = Validator();
  print(validate('ab'));     // false
  print(validate('abc'));    // true

  Calculator calc = Calculator();
  print(calc(10, '+', 5));   // 15.0
  print(calc(10, '*', 3));   // 30.0
}
```

---

## এনাম

### এনাম (Enum) কী?
নামযুক্ত কনস্ট্যান্টের একটি সেট। ডার্ট ৩.০-তে এনামে মেথড, প্রপার্টি এবং ইন্টারফেস যোগ করা যায়।

```dart
// সাধারণ এনাম
enum Direction {
  north,
  south,
  east,
  west,
}

// উন্নত এনাম (Dart 2.17+)
enum Planet {
  mercury(3.303e+23, 2.4397e6),
  venus(4.869e+24, 6.0518e6),
  earth(5.976e+24, 6.37814e6),
  mars(6.421e+23, 3.3972e6);

  final double mass;
  final double radius;

  const Planet(this.mass, this.radius);

  static const double G = 6.67430e-11;

  double get surfaceGravity => G * mass / (radius * radius);
  double surfaceWeight(double otherMass) => otherMass * surfaceGravity;
}

// মেথড সহ এনাম
enum OrderStatus {
  pending('অপেক্ষারত'),
  confirmed('নিশ্চিত'),
  processing('প্রক্রিয়াধীন'),
  shipped('প্রেরিত'),
  delivered('বিতরিত'),
  cancelled('বাতিল');

  final String displayName;

  const OrderStatus(this.displayName);

  bool get isActive => this != OrderStatus.cancelled && this != OrderStatus.delivered;

  OrderStatus? get next {
    final values = OrderStatus.values;
    final index = values.indexOf(this);
    if (index < values.length - 1 && this != OrderStatus.cancelled) {
      return values[index + 1];
    }
    return null;
  }
}

void main() {
  // সাধারণ এনাম
  Direction dir = Direction.north;
  print(dir);          // Direction.north
  print(dir.name);     // north
  print(dir.index);    // 0

  // সব মান
  for (Direction d in Direction.values) {
    print(d);
  }

  // উন্নত এনাম
  print(Planet.earth.surfaceGravity);              // 9.80...
  print(Planet.earth.surfaceWeight(75.0));          // 735...

  // OrderStatus
  OrderStatus status = OrderStatus.pending;
  print(status.displayName);  // অপেক্ষারত
  print(status.isActive);     // true
  print(status.next);         // OrderStatus.confirmed
}
```

---

## ডিজাইন প্যাটার্ন

### ১. সিঙ্গেলটন প্যাটার্ন (Singleton Pattern)
একটি ক্লাসের শুধুমাত্র একটি ইনস্ট্যান্স নিশ্চিত করে।

```dart
class AppConfig {
  static AppConfig? _instance;

  String appName;
  String version;
  bool isDevelopment;

  AppConfig._internal({
    required this.appName,
    required this.version,
    required this.isDevelopment,
  });

  factory AppConfig({
    String appName = 'আমার অ্যাপ',
    String version = '1.0.0',
    bool isDevelopment = false,
  }) {
    _instance ??= AppConfig._internal(
      appName: appName,
      version: version,
      isDevelopment: isDevelopment,
    );
    return _instance!;
  }

  void printConfig() {
    print('অ্যাপ: $appName, ভার্সন: $version, Dev: $isDevelopment');
  }
}
```

### ২. ফ্যাক্টরি মেথড প্যাটার্ন (Factory Method Pattern)

```dart
abstract class Animal3 {
  String name;
  Animal3(this.name);

  void makeSound();
  void move();

  // ফ্যাক্টরি মেথড
  factory Animal3.create(String type, String name) {
    switch (type) {
      case 'dog': return Dog2(name);
      case 'cat': return Cat2(name);
      case 'bird': return Bird(name);
      default: throw Exception('অজানা প্রাণীর ধরন: $type');
    }
  }
}

class Dog2 extends Animal3 {
  Dog2(String name) : super(name);
  @override void makeSound() => print('$name: ঘেউ ঘেউ!');
  @override void move() => print('$name দৌড়াচ্ছে!');
}

class Cat2 extends Animal3 {
  Cat2(String name) : super(name);
  @override void makeSound() => print('$name: মিয়াও!');
  @override void move() => print('$name হাঁটছে!');
}

class Bird extends Animal3 {
  Bird(String name) : super(name);
  @override void makeSound() => print('$name: কিচিরমিচির!');
  @override void move() => print('$name উড়ছে!');
}

void main() {
  List<Animal3> animals = [
    Animal3.create('dog', 'বাদল'),
    Animal3.create('cat', 'মিনু'),
    Animal3.create('bird', 'টিয়া'),
  ];

  for (Animal3 a in animals) {
    a.makeSound();
    a.move();
  }
}
```

### ৩. অবজার্ভার প্যাটার্ন (Observer Pattern)

```dart
// অবজার্ভার ইন্টারফেস
abstract class Observer {
  void update(String event, dynamic data);
}

// সাবজেক্ট
class EventEmitter {
  final Map<String, List<Observer>> _listeners = {};

  void on(String event, Observer observer) {
    _listeners.putIfAbsent(event, () => []);
    _listeners[event]!.add(observer);
  }

  void off(String event, Observer observer) {
    _listeners[event]?.remove(observer);
  }

  void emit(String event, [dynamic data]) {
    _listeners[event]?.forEach((observer) {
      observer.update(event, data);
    });
  }
}

// কংক্রিট অবজার্ভার
class UIUpdater implements Observer {
  @override
  void update(String event, dynamic data) {
    print('UI আপডেট হচ্ছে: ঘটনা=$event, ডেটা=$data');
  }
}

class Logger3 implements Observer {
  @override
  void update(String event, dynamic data) {
    print('লগ: [${DateTime.now()}] $event - $data');
  }
}

void main() {
  EventEmitter emitter = EventEmitter();
  UIUpdater ui = UIUpdater();
  Logger3 logger = Logger3();

  emitter.on('user_login', ui);
  emitter.on('user_login', logger);
  emitter.on('purchase', ui);

  emitter.emit('user_login', {'userId': 123, 'name': 'রহিম'});
  emitter.emit('purchase', {'amount': 500, 'item': 'বই'});
}
```

### ৪. ডেকোরেটর প্যাটার্ন (Decorator Pattern)

```dart
abstract class Coffee {
  String get description;
  double get cost;
}

class SimpleCoffee implements Coffee {
  @override
  String get description => 'সাধারণ কফি';

  @override
  double get cost => 30.0;
}

abstract class CoffeeDecorator implements Coffee {
  final Coffee _coffee;
  CoffeeDecorator(this._coffee);
}

class MilkDecorator extends CoffeeDecorator {
  MilkDecorator(Coffee coffee) : super(coffee);

  @override
  String get description => '${_coffee.description} + দুধ';

  @override
  double get cost => _coffee.cost + 15.0;
}

class SugarDecorator extends CoffeeDecorator {
  SugarDecorator(Coffee coffee) : super(coffee);

  @override
  String get description => '${_coffee.description} + চিনি';

  @override
  double get cost => _coffee.cost + 5.0;
}

class WhipDecorator extends CoffeeDecorator {
  WhipDecorator(Coffee coffee) : super(coffee);

  @override
  String get description => '${_coffee.description} + হুইপড ক্রিম';

  @override
  double get cost => _coffee.cost + 20.0;
}

void main() {
  Coffee coffee = SimpleCoffee();
  print('${coffee.description}: ${coffee.cost} টাকা');

  coffee = MilkDecorator(coffee);
  print('${coffee.description}: ${coffee.cost} টাকা');

  coffee = SugarDecorator(coffee);
  print('${coffee.description}: ${coffee.cost} টাকা');

  coffee = WhipDecorator(coffee);
  print('${coffee.description}: ${coffee.cost} টাকা');
}
```

### ৫. বিল্ডার প্যাটার্ন (Builder Pattern)

```dart
class Pizza {
  String size;
  String crust;
  List<String> toppings;
  bool extraCheese;
  bool extraSauce;

  Pizza._({
    required this.size,
    required this.crust,
    required this.toppings,
    required this.extraCheese,
    required this.extraSauce,
  });

  @override
  String toString() {
    return '''পিজ্জা: $size সাইজ
ক্রাস্ট: $crust
টপিংস: ${toppings.join(', ')}
অতিরিক্ত চিজ: $extraCheese
অতিরিক্ত সস: $extraSauce''';
  }
}

class PizzaBuilder {
  String _size = 'মাঝারি';
  String _crust = 'পাতলা';
  List<String> _toppings = [];
  bool _extraCheese = false;
  bool _extraSauce = false;

  PizzaBuilder size(String size) {
    _size = size;
    return this;
  }

  PizzaBuilder crust(String crust) {
    _crust = crust;
    return this;
  }

  PizzaBuilder addTopping(String topping) {
    _toppings.add(topping);
    return this;
  }

  PizzaBuilder withExtraCheese() {
    _extraCheese = true;
    return this;
  }

  PizzaBuilder withExtraSauce() {
    _extraSauce = true;
    return this;
  }

  Pizza build() {
    return Pizza._(
      size: _size,
      crust: _crust,
      toppings: _toppings,
      extraCheese: _extraCheese,
      extraSauce: _extraSauce,
    );
  }
}

void main() {
  Pizza pizza = PizzaBuilder()
      .size('বড়')
      .crust('মোটা')
      .addTopping('পেঁয়াজ')
      .addTopping('মাশরুম')
      .addTopping('চিজ')
      .withExtraCheese()
      .withExtraSauce()
      .build();

  print(pizza);
}
```

---

## SOLID নীতি

### SOLID কী?
সফটওয়্যার ডিজাইনের পাঁচটি মূল নীতি যা কোড রক্ষণাবেক্ষণযোগ্য ও সম্প্রসারণযোগ্য রাখে।

### ১. S – Single Responsibility Principle (একক দায়িত্ব নীতি)
একটি ক্লাসের শুধুমাত্র একটি কাজ থাকবে এবং পরিবর্তনের একটিমাত্র কারণ থাকবে।

```dart
// ❌ ভুল – একটি ক্লাসে অনেক দায়িত্ব
class BadUserManager {
  void saveUser(Map user) { /* ডেটাবেজে সংরক্ষণ */ }
  void sendEmail(String email) { /* ইমেইল পাঠানো */ }
  void generateReport() { /* রিপোর্ট তৈরি */ }
  void logActivity() { /* লগ করা */ }
}

// ✅ সঠিক – প্রতিটি ক্লাসের একটি দায়িত্ব
class UserRepository {
  void save(Map user) => print('ব্যবহারকারী সংরক্ষণ হয়েছে');
  Map? findById(int id) => null;
}

class EmailService {
  void send(String to, String subject, String body) {
    print('ইমেইল পাঠানো হয়েছে $to এ');
  }
}

class ReportGenerator {
  void generate(List data) => print('রিপোর্ট তৈরি হয়েছে');
}

class ActivityLogger {
  void log(String activity) => print('লগ: $activity');
}
```

### ২. O – Open/Closed Principle (খোলা/বন্ধ নীতি)
ক্লাস সম্প্রসারণের জন্য খোলা থাকবে কিন্তু পরিবর্তনের জন্য বন্ধ।

```dart
// ✅ সঠিক
abstract class DiscountCalculator {
  double calculate(double price);
}

class RegularDiscount extends DiscountCalculator {
  @override
  double calculate(double price) => price * 0.05; // ৫% ছাড়
}

class PremiumDiscount extends DiscountCalculator {
  @override
  double calculate(double price) => price * 0.15; // ১৫% ছাড়
}

class SeasonalDiscount extends DiscountCalculator {
  @override
  double calculate(double price) => price * 0.25; // ২৫% ছাড়
}

// নতুন ছাড় যোগ করতে বিদ্যমান কোড পরিবর্তন দরকার নেই
class FlashSaleDiscount extends DiscountCalculator {
  @override
  double calculate(double price) => price * 0.50; // ৫০% ছাড়
}
```

### ৩. L – Liskov Substitution Principle (লিস্কভ প্রতিস্থাপন নীতি)
সাব-ক্লাসের অবজেক্ট প্যারেন্ট ক্লাসের জায়গায় ব্যবহারযোগ্য হতে হবে।

```dart
abstract class Bird2 {
  String name;
  Bird2(this.name);
  void eat() => print('$name খাচ্ছে');
}

abstract class FlyingBird extends Bird2 {
  FlyingBird(String name) : super(name);
  void fly();
}

class Parrot extends FlyingBird {
  Parrot(String name) : super(name);
  @override
  void fly() => print('$name উড়ছে!');
}

class Penguin extends Bird2 {
  Penguin(String name) : super(name);
  void swim() => print('$name সাঁতার কাটছে!');
}
```

### ৪. I – Interface Segregation Principle (ইন্টারফেস বিভাজন নীতি)
ক্লাসকে অপ্রয়োজনীয় মেথড বাস্তবায়নে বাধ্য করা উচিত নয়।

```dart
// ✅ ছোট ছোট ইন্টারফেসে বিভক্ত
abstract class Readable {
  String read();
}

abstract class Writable {
  void write(String data);
}

abstract class Deletable {
  void delete();
}

class ReadOnlyFile implements Readable {
  @override
  String read() => 'ফাইলের বিষয়বস্তু';
}

class WriteOnlyFile implements Writable {
  @override
  void write(String data) => print('লেখা হচ্ছে: $data');
}

class FullAccessFile implements Readable, Writable, Deletable {
  @override
  String read() => 'ফাইলের বিষয়বস্তু';

  @override
  void write(String data) => print('লেখা হচ্ছে: $data');

  @override
  void delete() => print('মুছে ফেলা হচ্ছে');
}
```

### ৫. D – Dependency Inversion Principle (নির্ভরতা বিপরীত নীতি)
উচ্চ-স্তরের মডিউল নিম্ন-স্তরের মডিউলের উপর নির্ভর করবে না; উভয়ই অ্যাবস্ট্রাকশনের উপর নির্ভর করবে।

```dart
// অ্যাবস্ট্রাকশন
abstract class MessageSender {
  void send(String message, String recipient);
}

// নিম্ন-স্তরের বাস্তবায়ন
class EmailSender implements MessageSender {
  @override
  void send(String message, String recipient) {
    print('ইমেইল পাঠানো হচ্ছে $recipient এ: $message');
  }
}

class SMSSender implements MessageSender {
  @override
  void send(String message, String recipient) {
    print('SMS পাঠানো হচ্ছে $recipient এ: $message');
  }
}

// উচ্চ-স্তরের ক্লাস – অ্যাবস্ট্রাকশনের উপর নির্ভর করে
class NotificationService {
  final MessageSender _sender;

  // Dependency Injection
  NotificationService(this._sender);

  void notify(String message, String recipient) {
    _sender.send(message, recipient);
  }
}

void main() {
  NotificationService emailService = NotificationService(EmailSender());
  NotificationService smsService = NotificationService(SMSSender());

  emailService.notify('স্বাগতম!', 'user@email.com');
  smsService.notify('OTP: 123456', '01712345678');
}
```

---

## সম্পূর্ণ উদাহরণ – লাইব্রেরি ম্যানেজমেন্ট সিস্টেম

```dart
// সম্পূর্ণ OOP ব্যবহার করে একটি লাইব্রেরি সিস্টেম

abstract class LibraryItem {
  final String id;
  final String title;
  final int year;
  bool _isAvailable = true;

  LibraryItem({required this.id, required this.title, required this.year});

  bool get isAvailable => _isAvailable;

  void checkout() {
    if (!_isAvailable) throw Exception('আইটেম পাওয়া যাচ্ছে না!');
    _isAvailable = false;
    print('$title চেকআউট করা হয়েছে।');
  }

  void returnItem() {
    _isAvailable = true;
    print('$title ফেরত দেওয়া হয়েছে।');
  }

  String get details;
}

mixin Searchable {
  String get searchableText;

  bool matches(String query) {
    return searchableText.toLowerCase().contains(query.toLowerCase());
  }
}

class Book extends LibraryItem with Searchable {
  final String author;
  final String isbn;
  final String genre;

  Book({
    required String id,
    required String title,
    required int year,
    required this.author,
    required this.isbn,
    required this.genre,
  }) : super(id: id, title: title, year: year);

  @override
  String get details => 'বই: $title | লেখক: $author | ISBN: $isbn | ধরন: $genre';

  @override
  String get searchableText => '$title $author $genre';
}

class DVD extends LibraryItem with Searchable {
  final String director;
  final int duration;

  DVD({
    required String id,
    required String title,
    required int year,
    required this.director,
    required this.duration,
  }) : super(id: id, title: title, year: year);

  @override
  String get details => 'DVD: $title | পরিচালক: $director | সময়কাল: $duration মিনিট';

  @override
  String get searchableText => '$title $director';
}

class Member {
  final String memberId;
  final String name;
  final String email;
  final List<LibraryItem> _checkedOut = [];

  Member({required this.memberId, required this.name, required this.email});

  List<LibraryItem> get checkedOutItems => List.unmodifiable(_checkedOut);

  void borrowItem(LibraryItem item) {
    if (_checkedOut.length >= 5) {
      throw Exception('সর্বোচ্চ ৫টি আইটেম ধার নেওয়া যাবে!');
    }
    item.checkout();
    _checkedOut.add(item);
  }

  void returnItem(LibraryItem item) {
    item.returnItem();
    _checkedOut.remove(item);
  }
}

class Library {
  final String name;
  final Map<String, LibraryItem> _catalog = {};
  final Map<String, Member> _members = {};

  Library(this.name);

  void addItem(LibraryItem item) {
    _catalog[item.id] = item;
    print('যোগ করা হয়েছে: ${item.title}');
  }

  void registerMember(Member member) {
    _members[member.memberId] = member;
    print('সদস্য নিবন্ধিত: ${member.name}');
  }

  List<LibraryItem> search(String query) {
    return _catalog.values
        .whereType<Searchable>()
        .where((item) => (item as Searchable).matches(query))
        .cast<LibraryItem>()
        .toList();
  }

  List<LibraryItem> get availableItems =>
      _catalog.values.where((item) => item.isAvailable).toList();

  void printCatalog() {
    print('\n=== $name এর ক্যাটালগ ===');
    for (LibraryItem item in _catalog.values) {
      print('${item.isAvailable ? '✓' : '✗'} ${item.details}');
    }
  }
}

void main() {
  Library library = Library('ঢাকা পাবলিক লাইব্রেরি');

  // আইটেম যোগ করা
  library.addItem(Book(
    id: 'B001', title: 'আমার দেশ আমার মা', year: 2020,
    author: 'রবীন্দ্রনাথ', isbn: '978-0-00-000001-1', genre: 'কবিতা',
  ));
  library.addItem(Book(
    id: 'B002', title: 'শেষের কবিতা', year: 1929,
    author: 'রবীন্দ্রনাথ ঠাকুর', isbn: '978-0-00-000002-2', genre: 'উপন্যাস',
  ));
  library.addItem(DVD(
    id: 'D001', title: 'পদ্মা নদীর মাঝি', year: 1993,
    director: 'গৌতম ঘোষ', duration: 150,
  ));

  // সদস্য নিবন্ধন
  Member member = Member(
    memberId: 'M001', name: 'আহমেদ করিম', email: 'karim@email.com',
  );
  library.registerMember(member);

  // ক্যাটালগ দেখা
  library.printCatalog();

  // ধার নেওয়া
  LibraryItem book = library._catalog['B001']!;
  member.borrowItem(book);

  // অনুসন্ধান
  List<LibraryItem> results = library.search('রবীন্দ্রনাথ');
  print('\nঅনুসন্ধান ফলাফল:');
  for (LibraryItem item in results) {
    print(item.details);
  }

  // আপডেটেড ক্যাটালগ
  library.printCatalog();
}
```

---

## পরবর্তী ধাপ

এই সিলেবাস সম্পন্ন করার পর আপনি প্রস্তুত থাকবেন:

১. **ফ্লাটার উইজেট** তৈরিতে OOP ব্যবহার করতে
২. **স্টেট ম্যানেজমেন্ট** (Provider, Bloc, Riverpod) শিখতে
৩. **REST API** সংযোগ এবং ডেটা মডেলিং করতে
৪. **ক্লিন আর্কিটেকচার** অনুসরণ করে বড় অ্যাপ তৈরি করতে
৫. **ডিজাইন প্যাটার্ন** গভীরভাবে শিখতে
৬. **টেস্টিং** (Unit Test, Widget Test) লিখতে

---

## রিসোর্সসমূহ

- **অফিসিয়াল ডার্ট ডকুমেন্টেশন:** https://dart.dev/guides
- **ডার্ট OOP গাইড:** https://dart.dev/language/classes
- **ফ্লাটার ডকুমেন্টেশন:** https://flutter.dev/docs
- **DartPad (অনলাইন এডিটর):** https://dartpad.dev
- **ডার্ট প্যাকেজ:** https://pub.dev

---

**নোট:** OOP শেখার সবচেয়ে ভালো উপায় হলো বাস্তব প্রজেক্টে প্রয়োগ করা। প্রতিটি ধারণা বোঝার পর নিজে কোড লিখে অনুশীলন করুন। ছোট ছোট প্রজেক্ট দিয়ে শুরু করুন এবং ধীরে ধীরে জটিল সমস্যা সমাধান করুন।
