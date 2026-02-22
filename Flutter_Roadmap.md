# Flutter A to Z সম্পূর্ণ গাইড (বাংলা)

Flutter হলো Google-এর একটি ওপেন-সোর্স UI ফ্রেমওয়ার্ক যা একটি কোডবেস থেকে Android, iOS, Web, Desktop সহ সব প্ল্যাটফর্মে অ্যাপ তৈরি করতে দেয়। এটি Dart প্রোগ্রামিং ভাষা ব্যবহার করে।

---

## বিষয়সূচি

1. [Flutter পরিচিতি](#flutter-পরিচিতি)
2. [পরিবেশ সেটআপ](#পরিবেশ-সেটআপ)
3. [প্রথম প্রজেক্ট তৈরি](#প্রথম-প্রজেক্ট-তৈরি)
4. [Flutter আর্কিটেকচার](#flutter-আর্কিটেকচার)
5. [উইজেট পরিচিতি](#উইজেট-পরিচিতি)
6. [StatelessWidget](#statelesswidget)
7. [StatefulWidget](#statefulwidget)
8. [লেআউট উইজেট](#লেআউট-উইজেট)
9. [টেক্সট ও স্টাইলিং](#টেক্সট-ও-স্টাইলিং)
10. [বাটন উইজেট](#বাটন-উইজেট)
11. [ইনপুট উইজেট](#ইনপুট-উইজেট)
12. [ইমেজ ও আইকন](#ইমেজ-ও-আইকন)
13. [লিস্ট ও গ্রিড](#লিস্ট-ও-গ্রিড)
14. [নেভিগেশন ও রাউটিং](#নেভিগেশন-ও-রাউটিং)
15. [স্ক্রল ও সোয়াইপ](#স্ক্রল-ও-সোয়াইপ)
16. [ডায়ালগ ও স্ন্যাকবার](#ডায়ালগ-ও-স্ন্যাকবার)
17. [থিম ও ডার্ক মোড](#থিম-ও-ডার্ক-মোড)
18. [অ্যানিমেশন](#অ্যানিমেশন)
19. [হেস্চার ডিটেকশন](#জেস্চার-ডিটেকশন)
20. [ফর্ম ও ভ্যালিডেশন](#ফর্ম-ও-ভ্যালিডেশন)
21. [HTTP রিকোয়েস্ট ও API](#http-রিকোয়েস্ট-ও-api)
22. [JSON পার্সিং](#json-পার্সিং)
23. [লোকাল স্টোরেজ](#লোকাল-স্টোরেজ)
24. [স্টেট ম্যানেজমেন্ট](#স্টেট-ম্যানেজমেন্ট)
25. [Provider](#provider)
26. [Riverpod](#riverpod)
27. [BLoC প্যাটার্ন](#bloc-প্যাটার্ন)
28. [Firebase ইন্টিগ্রেশন](#firebase-ইন্টিগ্রেশন)
29. [পুশ নোটিফিকেশন](#পুশ-নোটিফিকেশন)
30. [প্ল্যাটফর্ম চ্যানেল](#প্ল্যাটফর্ম-চ্যানেল)
31. [টেস্টিং](#টেস্টিং)
32. [পারফরম্যান্স অপটিমাইজেশন](#পারফরম্যান্স-অপটিমাইজেশন)
33. [অ্যাপ প্রকাশ](#অ্যাপ-প্রকাশ)
34. [সম্পূর্ণ প্রজেক্ট উদাহরণ](#সম্পূর্ণ-প্রজেক্ট-উদাহরণ)

---

## Flutter পরিচিতি

### Flutter কী?
Flutter হলো Google-এর তৈরি একটি ক্রস-প্ল্যাটফর্ম UI ফ্রেমওয়ার্ক। এটি দিয়ে একটি কোড লিখেই Android, iOS, Web, Windows, macOS এবং Linux-এ অ্যাপ চালানো যায়।

### Flutter কেন ব্যবহার করবেন?
- **একক কোডবেস** – একবার লিখুন, সব জায়গায় চালান
- **দ্রুত উন্নয়ন** – Hot Reload ও Hot Restart সুবিধা
- **সুন্দর UI** – Material Design ও Cupertino উইজেট
- **উচ্চ পারফরম্যান্স** – Native-এর মতো পারফরম্যান্স
- **বড় কমিউনিটি** – প্রচুর প্যাকেজ ও রিসোর্স

### Flutter vs React Native vs Xamarin

| বৈশিষ্ট্য | Flutter | React Native | Xamarin |
|---------|---------|-------------|---------|
| ভাষা | Dart | JavaScript | C# |
| পারফরম্যান্স | উচ্চ | মধ্যম | মধ্যম |
| UI রেন্ডারিং | নিজস্ব ইঞ্জিন | নেটিভ কম্পোনেন্ট | নেটিভ কম্পোনেন্ট |
| কমিউনিটি | বড় | সবচেয়ে বড় | ছোট |
| Google সমর্থন | হ্যাঁ | মেটা | মাইক্রোসফট |

### Flutter আর্কিটেকচার সংক্ষেপ
```
┌─────────────────────────────┐
│         Flutter App         │ ← আপনার কোড (Dart)
├─────────────────────────────┤
│       Flutter Framework     │ ← উইজেট, অ্যানিমেশন, জেস্চার
├─────────────────────────────┤
│         Flutter Engine      │ ← Skia/Impeller রেন্ডারিং
├─────────────────────────────┤
│     Platform (Android/iOS)  │ ← অপারেটিং সিস্টেম
└─────────────────────────────┘
```

---

## পরিবেশ সেটআপ

### ১. Flutter SDK ইনস্টল করুন

**Windows:**
```powershell
# winget ব্যবহার করে
winget install Google.Flutter

# অথবা সরাসরি ডাউনলোড করুন
# https://docs.flutter.dev/get-started/install/windows
```

**macOS:**
```bash
# Homebrew ব্যবহার করে
brew install flutter

# অথবা সরাসরি ডাউনলোড করুন
# https://docs.flutter.dev/get-started/install/macos
```

**Linux:**
```bash
sudo snap install flutter --classic
```

### ২. পরিবেশ যাচাই করুন
```bash
flutter doctor
```

এটি সমস্যাগুলো দেখাবে। যেমন:
```
Doctor summary:
[✓] Flutter (Channel stable, 3.x.x)
[✓] Android toolchain
[✓] Android Studio
[✓] VS Code
[!] Chrome - (অনুপস্থিত - web এর জন্য প্রয়োজন)
```

### ৩. IDE সেটআপ

**VS Code (সুপারিশকৃত):**
- Flutter এক্সটেনশন ইনস্টল করুন
- Dart এক্সটেনশন ইনস্টল করুন

**Android Studio:**
- Flutter Plugin ইনস্টল করুন
- Dart Plugin ইনস্টল করুন

### ৪. Android এমুলেটর বা ডিভাইস সেটআপ

```bash
# উপলব্ধ ডিভাইস দেখুন
flutter devices

# এমুলেটর চালু করুন
flutter emulators --launch <emulator_id>
```

---

## প্রথম প্রজেক্ট তৈরি

### নতুন প্রজেক্ট তৈরি করুন
```bash
# প্রজেক্ট তৈরি
flutter create আমার_অ্যাপ
cd আমার_অ্যাপ

# অ্যাপ চালু করুন
flutter run
```

### প্রজেক্ট কাঠামো
```
আমার_অ্যাপ/
├── android/          ← Android নির্দিষ্ট ফাইল
├── ios/              ← iOS নির্দিষ্ট ফাইল
├── lib/              ← আপনার Dart কোড (মূল স্থান)
│   └── main.dart     ← অ্যাপের প্রবেশ বিন্দু
├── web/              ← Web নির্দিষ্ট ফাইল
├── test/             ← টেস্ট ফাইল
├── assets/           ← ইমেজ, ফন্ট ইত্যাদি
└── pubspec.yaml      ← প্রজেক্ট কনফিগারেশন
```

### pubspec.yaml পরিচিতি
```yaml
name: আমার_অ্যাপ
description: আমার প্রথম Flutter অ্যাপ
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  # নতুন প্যাকেজ এখানে যোগ করুন
  http: ^1.1.0
  provider: ^6.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^2.0.0

flutter:
  uses-material-design: true
  assets:
    - assets/images/
  fonts:
    - family: Hind Siliguri
      fonts:
        - asset: assets/fonts/HindSiliguri-Regular.ttf
```

### প্রথম অ্যাপ – main.dart
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'আমার প্রথম অ্যাপ',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),
        useMaterial3: true,
      ),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('স্বাগতম Flutter-এ!'),
        backgroundColor: Colors.blue,
      ),
      body: const Center(
        child: Text(
          'আমার প্রথম Flutter অ্যাপ 🎉',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

### Hot Reload ও Hot Restart
```bash
# অ্যাপ চালু থাকা অবস্থায়:
# r → Hot Reload (দ্রুত, state সংরক্ষিত থাকে)
# R → Hot Restart (ধীর, state রিসেট হয়)
# q → বের হন
```

---

## Flutter আর্কিটেকচার

### Widget Tree (উইজেট গাছ)
Flutter-এ সবকিছুই উইজেট। উইজেটগুলো একটি গাছের মতো সাজানো থাকে।

```
MaterialApp
└── Scaffold
    ├── AppBar
    │   └── Text ("শিরোনাম")
    ├── Body
    │   └── Column
    │       ├── Text ("বিষয়বস্তু ১")
    │       └── Text ("বিষয়বস্তু ২")
    └── FloatingActionButton
        └── Icon
```

### তিনটি গাছ
Flutter তিনটি গাছ ব্যবহার করে:

**১. Widget Tree** – কনফিগারেশন/ব্লুপ্রিন্ট (immutable, পুনর্নির্মাণ হয়)

**২. Element Tree** – Widget Tree-র জীবন্ত উদাহরণ (mutable, state ধরে)

**৩. Render Tree** – স্ক্রিনে আঁকার নির্দেশনা (layout, paint)

### BuildContext কী?
BuildContext হলো উইজেটের অবস্থান নির্দেশকারী একটি হ্যান্ডেল। এর মাধ্যমে উইজেট তার পূর্বপুরুষ খুঁজে পায়।

```dart
Widget build(BuildContext context) {
  // context ব্যবহার করে থিম পাওয়া
  final theme = Theme.of(context);
  
  // context ব্যবহার করে নেভিগেট করা
  Navigator.of(context).push(...);
  
  // context ব্যবহার করে মিডিয়া কোয়েরি করা
  final screenWidth = MediaQuery.of(context).size.width;
  
  return Container();
}
```

---

## উইজেট পরিচিতি

### উইজেট কী?
Flutter-এ UI-এর প্রতিটি উপাদানই একটি উইজেট। বাটন, টেক্সট, ইমেজ, লেআউট – সবকিছুই উইজেট।

### উইজেটের ধরন

```dart
// ১. StatelessWidget – অপরিবর্তনীয় উইজেট
class GreetingWidget extends StatelessWidget {
  final String name;
  const GreetingWidget({required this.name, super.key});

  @override
  Widget build(BuildContext context) {
    return Text('স্বাগতম, $name!');
  }
}

// ২. StatefulWidget – পরিবর্তনযোগ্য উইজেট
class CounterWidget extends StatefulWidget {
  const CounterWidget({super.key});

  @override
  State<CounterWidget> createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _count = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('গণনা: $_count'),
        ElevatedButton(
          onPressed: () => setState(() => _count++),
          child: const Text('বাড়ান'),
        ),
      ],
    );
  }
}
```

### গুরুত্বপূর্ণ বেসিক উইজেট

```dart
// Container – বহুমুখী বাক্স উইজেট
Container(
  width: 200,
  height: 100,
  margin: const EdgeInsets.all(8),
  padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(12),
    boxShadow: [
      BoxShadow(
        color: Colors.black26,
        blurRadius: 6,
        offset: Offset(0, 3),
      )
    ],
  ),
  child: const Text('কন্টেইনার উইজেট', style: TextStyle(color: Colors.white)),
)

// SizedBox – নির্দিষ্ট আকারের বাক্স / ফাঁকা জায়গা
const SizedBox(width: 16, height: 16)

// Padding – প্যাডিং দেওয়া
Padding(
  padding: const EdgeInsets.all(16),
  child: Text('প্যাডিং সহ টেক্সট'),
)

// Center – কেন্দ্রে রাখা
Center(
  child: Text('কেন্দ্রে আছি'),
)
```

---

## StatelessWidget

### StatelessWidget কী?
যে উইজেট একবার তৈরি হলে আর পরিবর্তন হয় না। এটি শুধু তার প্রপার্টি (parameters) থেকে UI তৈরি করে।

```dart
// কাস্টম কার্ড উইজেট
class ProductCard extends StatelessWidget {
  final String name;
  final double price;
  final String imageUrl;
  final VoidCallback onTap;

  const ProductCard({
    super.key,
    required this.name,
    required this.price,
    required this.imageUrl,
    required this.onTap,
  });

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onTap,
      child: Card(
        elevation: 4,
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Image.network(imageUrl, height: 150, width: double.infinity, fit: BoxFit.cover),
            Padding(
              padding: const EdgeInsets.all(8),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(name, style: const TextStyle(fontSize: 16, fontWeight: FontWeight.bold)),
                  const SizedBox(height: 4),
                  Text('৳${price.toStringAsFixed(2)}', style: const TextStyle(color: Colors.green, fontSize: 14)),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

// ব্যবহার
ProductCard(
  name: 'আম',
  price: 120.0,
  imageUrl: 'https://example.com/mango.jpg',
  onTap: () => print('কার্ডে ক্লিক হয়েছে'),
)
```

### StatelessWidget লাইফসাইকেল
```dart
class MyStateless extends StatelessWidget {
  const MyStateless({super.key});

  @override
  Widget build(BuildContext context) {
    // প্রতিবার পুনর্নির্মাণের সময় কল হয়
    // এখানে কোনো state নেই
    return const Text('আমি পরিবর্তন হই না');
  }
}
```

---

## StatefulWidget

### StatefulWidget কী?
যে উইজেট পরিবর্তন হতে পারে। State পরিবর্তন হলে `setState()` কল করতে হয়, যা উইজেট পুনর্নির্মাণ করে।

### লাইফসাইকেল মেথড
```dart
class FullLifecycleWidget extends StatefulWidget {
  const FullLifecycleWidget({super.key});

  @override
  State<FullLifecycleWidget> createState() => _FullLifecycleWidgetState();
}

class _FullLifecycleWidgetState extends State<FullLifecycleWidget> {
  int _counter = 0;

  @override
  void initState() {
    super.initState();
    // উইজেট প্রথমবার তৈরি হওয়ার সময়
    // API কল, Timer শুরু করুন এখানে
    print('initState: উইজেট শুরু হয়েছে');
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    // নির্ভরতা পরিবর্তন হলে (যেমন থিম, ভাষা)
    print('didChangeDependencies কল হয়েছে');
  }

  @override
  void didUpdateWidget(FullLifecycleWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    // প্যারেন্ট উইজেট পুনর্নির্মাণ করলে
    print('didUpdateWidget: প্যারামিটার পরিবর্তন হয়েছে');
  }

  @override
  Widget build(BuildContext context) {
    // UI তৈরি করা
    return Column(
      children: [
        Text('গণনা: $_counter'),
        ElevatedButton(
          onPressed: () {
            setState(() {
              // setState() ছাড়া UI আপডেট হবে না
              _counter++;
            });
          },
          child: const Text('বাড়ান'),
        ),
      ],
    );
  }

  @override
  void deactivate() {
    // উইজেট গাছ থেকে সরানো হলে
    print('deactivate: উইজেট সরানো হয়েছে');
    super.deactivate();
  }

  @override
  void dispose() {
    // উইজেট স্থায়ীভাবে ধ্বংস হলে
    // Controller, Timer, Stream বন্ধ করুন এখানে
    print('dispose: উইজেট মুছে গেছে');
    super.dispose();
  }
}
```

### setState() সঠিক ব্যবহার
```dart
// ❌ ভুল – async কাজের মাঝে setState
Future<void> loadData() async {
  final data = await fetchData();
  setState(() {
    _data = data; // mounted না হলে ক্র্যাশ হতে পারে
  });
}

// ✅ সঠিক – mounted যাচাই করুন
Future<void> loadData() async {
  final data = await fetchData();
  if (mounted) {
    setState(() {
      _data = data;
    });
  }
}
```

---

## লেআউট উইজেট

### Column – উল্লম্ব সজ্জা
```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,      // উল্লম্ব অক্ষে
  crossAxisAlignment: CrossAxisAlignment.start,     // আনুভূমিক অক্ষে
  mainAxisSize: MainAxisSize.min,                   // ন্যূনতম আকার
  children: [
    const Text('প্রথম'),
    const SizedBox(height: 8),
    const Text('দ্বিতীয়'),
    const SizedBox(height: 8),
    const Text('তৃতীয়'),
  ],
)
```

### Row – আনুভূমিক সজ্জা
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceBetween,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    const Icon(Icons.star, color: Colors.amber),
    const Text('রেটিং: ৪.৫'),
    ElevatedButton(
      onPressed: () {},
      child: const Text('কিনুন'),
    ),
  ],
)
```

### Stack – উপরে রাখা
```dart
Stack(
  alignment: Alignment.center,
  children: [
    // নিচে থাকবে
    Container(
      width: 200,
      height: 200,
      color: Colors.blue,
    ),
    // উপরে থাকবে
    const Text(
      'উপরে আছি',
      style: TextStyle(color: Colors.white, fontSize: 20),
    ),
    // নির্দিষ্ট অবস্থানে রাখা
    Positioned(
      top: 10,
      right: 10,
      child: Container(
        padding: const EdgeInsets.all(4),
        decoration: const BoxDecoration(color: Colors.red, shape: BoxShape.circle),
        child: const Text('৩', style: TextStyle(color: Colors.white)),
      ),
    ),
  ],
)
```

### Expanded ও Flexible
```dart
Row(
  children: [
    // উপলব্ধ স্থান সমানভাবে ভাগ করে নেয়
    Expanded(
      flex: 2,  // ২ ভাগ পাবে
      child: Container(color: Colors.blue, height: 50),
    ),
    const SizedBox(width: 8),
    Expanded(
      flex: 1,  // ১ ভাগ পাবে
      child: Container(color: Colors.red, height: 50),
    ),
  ],
)

// Flexible – প্রয়োজন অনুযায়ী নেয়, জোর করে না
Row(
  children: [
    Flexible(
      child: Text('এটি লম্বা হতে পারলে ছোট হয়ে যায়'),
    ),
    const Icon(Icons.info),
  ],
)
```

### Wrap – স্বয়ংক্রিয় লাইন ভাঙা
```dart
Wrap(
  spacing: 8,         // আনুভূমিক ফাঁক
  runSpacing: 8,      // উল্লম্ব ফাঁক
  children: [
    Chip(label: const Text('Flutter')),
    Chip(label: const Text('Dart')),
    Chip(label: const Text('Firebase')),
    Chip(label: const Text('Provider')),
    Chip(label: const Text('BLoC')),
  ],
)
```

### Align ও FractionallySizedBox
```dart
Align(
  alignment: Alignment.topRight,
  child: const Text('উপরে ডানে'),
)

// আনুপাতিক আকার
FractionallySizedBox(
  widthFactor: 0.8,  // প্যারেন্টের ৮০%
  heightFactor: 0.5,
  child: Container(color: Colors.green),
)
```

### ConstrainedBox ও AspectRatio
```dart
ConstrainedBox(
  constraints: const BoxConstraints(
    minWidth: 100,
    maxWidth: 300,
    minHeight: 50,
    maxHeight: 200,
  ),
  child: Container(color: Colors.orange),
)

AspectRatio(
  aspectRatio: 16 / 9,  // প্রস্থ:উচ্চতা অনুপাত
  child: Container(color: Colors.purple),
)
```

---

## টেক্সট ও স্টাইলিং

### Text উইজেট
```dart
// সাধারণ টেক্সট
const Text('সহজ টেক্সট')

// স্টাইল করা টেক্সট
Text(
  'স্টাইল করা টেক্সট',
  style: TextStyle(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    fontStyle: FontStyle.italic,
    color: Colors.deepPurple,
    letterSpacing: 1.5,
    wordSpacing: 3,
    height: 1.5,           // লাইনের উচ্চতা (লাইন হাইট)
    decoration: TextDecoration.underline,
    decorationColor: Colors.red,
    shadows: [
      Shadow(color: Colors.black26, blurRadius: 4, offset: Offset(2, 2)),
    ],
  ),
  textAlign: TextAlign.center,
  maxLines: 2,
  overflow: TextOverflow.ellipsis,  // ... দিয়ে কাটবে
)
```

### RichText – মিশ্র স্টাইল
```dart
RichText(
  text: TextSpan(
    style: const TextStyle(color: Colors.black, fontSize: 16),
    children: [
      const TextSpan(text: 'এটি '),
      TextSpan(
        text: 'লাল',
        style: const TextStyle(color: Colors.red, fontWeight: FontWeight.bold),
      ),
      const TextSpan(text: ' এবং এটি '),
      TextSpan(
        text: 'নীল',
        style: const TextStyle(color: Colors.blue, decoration: TextDecoration.underline),
        recognizer: TapGestureRecognizer()..onTap = () {
          print('নীল টেক্সটে ক্লিক!');
        },
      ),
      const TextSpan(text: ' টেক্সট।'),
    ],
  ),
)
```

### SelectableText – নির্বাচনযোগ্য টেক্সট
```dart
SelectableText(
  'এই টেক্সট কপি করা যাবে',
  style: const TextStyle(fontSize: 16),
  showCursor: true,
)
```

---

## বাটন উইজেট

### বিভিন্ন ধরনের বাটন
```dart
// ElevatedButton – উঁচু বাটন
ElevatedButton(
  onPressed: () => print('ক্লিক হয়েছে'),
  style: ElevatedButton.styleFrom(
    backgroundColor: Colors.blue,
    foregroundColor: Colors.white,
    padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 12),
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
    elevation: 4,
  ),
  child: const Text('উঁচু বাটন'),
)

// TextButton – সাদামাটা বাটন
TextButton(
  onPressed: () {},
  child: const Text('টেক্সট বাটন'),
)

// OutlinedButton – বর্ডার বাটন
OutlinedButton(
  onPressed: () {},
  style: OutlinedButton.styleFrom(
    side: const BorderSide(color: Colors.blue, width: 2),
  ),
  child: const Text('আউটলাইন বাটন'),
)

// IconButton – শুধু আইকন
IconButton(
  onPressed: () {},
  icon: const Icon(Icons.favorite),
  color: Colors.red,
  tooltip: 'পছন্দ করুন',
)

// FloatingActionButton
FloatingActionButton(
  onPressed: () {},
  backgroundColor: Colors.blue,
  child: const Icon(Icons.add),
)

// FloatingActionButton.extended – লেখা সহ
FloatingActionButton.extended(
  onPressed: () {},
  icon: const Icon(Icons.add),
  label: const Text('নতুন যোগ করুন'),
)
```

### নিষ্ক্রিয় বাটন
```dart
ElevatedButton(
  onPressed: null,  // null মানে নিষ্ক্রিয়
  child: const Text('নিষ্ক্রিয় বাটন'),
)
```

### লোডিং বাটন
```dart
class LoadingButton extends StatefulWidget {
  const LoadingButton({super.key});

  @override
  State<LoadingButton> createState() => _LoadingButtonState();
}

class _LoadingButtonState extends State<LoadingButton> {
  bool _isLoading = false;

  Future<void> _onPressed() async {
    setState(() => _isLoading = true);
    await Future.delayed(const Duration(seconds: 2));
    if (mounted) setState(() => _isLoading = false);
  }

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: _isLoading ? null : _onPressed,
      child: _isLoading
          ? const SizedBox(
              width: 20, height: 20,
              child: CircularProgressIndicator(strokeWidth: 2, color: Colors.white),
            )
          : const Text('জমা দিন'),
    );
  }
}
```

---

## ইনপুট উইজেট

### TextField
```dart
class TextFieldExample extends StatefulWidget {
  const TextFieldExample({super.key});

  @override
  State<TextFieldExample> createState() => _TextFieldExampleState();
}

class _TextFieldExampleState extends State<TextFieldExample> {
  final _controller = TextEditingController();
  final _focusNode = FocusNode();
  String _value = '';

  @override
  void dispose() {
    _controller.dispose();
    _focusNode.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        TextField(
          controller: _controller,
          focusNode: _focusNode,
          keyboardType: TextInputType.text,
          textInputAction: TextInputAction.done,
          maxLength: 100,
          obscureText: false,  // পাসওয়ার্ডের জন্য true
          onChanged: (value) => setState(() => _value = value),
          onSubmitted: (value) => print('জমা: $value'),
          decoration: InputDecoration(
            labelText: 'নাম লিখুন',
            hintText: 'আপনার পুরো নাম',
            prefixIcon: const Icon(Icons.person),
            suffixIcon: IconButton(
              icon: const Icon(Icons.clear),
              onPressed: () => _controller.clear(),
            ),
            border: OutlineInputBorder(borderRadius: BorderRadius.circular(8)),
            filled: true,
            fillColor: Colors.grey.shade100,
            errorText: _value.isEmpty ? 'নাম প্রয়োজন' : null,
          ),
        ),
        Text('লেখা: $_value'),
      ],
    );
  }
}
```

### Checkbox, Radio, Switch
```dart
class ToggleWidgets extends StatefulWidget {
  const ToggleWidgets({super.key});

  @override
  State<ToggleWidgets> createState() => _ToggleWidgetsState();
}

class _ToggleWidgetsState extends State<ToggleWidgets> {
  bool _checkValue = false;
  int _radioValue = 1;
  bool _switchValue = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Checkbox
        CheckboxListTile(
          title: const Text('আমি শর্তাবলীতে সম্মত'),
          value: _checkValue,
          onChanged: (val) => setState(() => _checkValue = val!),
        ),

        // Radio Button
        RadioListTile<int>(
          title: const Text('পুরুষ'),
          value: 1,
          groupValue: _radioValue,
          onChanged: (val) => setState(() => _radioValue = val!),
        ),
        RadioListTile<int>(
          title: const Text('মহিলা'),
          value: 2,
          groupValue: _radioValue,
          onChanged: (val) => setState(() => _radioValue = val!),
        ),

        // Switch
        SwitchListTile(
          title: const Text('নোটিফিকেশন চালু'),
          value: _switchValue,
          onChanged: (val) => setState(() => _switchValue = val),
        ),
      ],
    );
  }
}
```

### Slider ও RangeSlider
```dart
class SliderExample extends StatefulWidget {
  const SliderExample({super.key});

  @override
  State<SliderExample> createState() => _SliderExampleState();
}

class _SliderExampleState extends State<SliderExample> {
  double _value = 50;
  RangeValues _range = const RangeValues(20, 80);

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Slider(
          value: _value,
          min: 0,
          max: 100,
          divisions: 10,
          label: _value.round().toString(),
          onChanged: (val) => setState(() => _value = val),
        ),
        Text('মান: ${_value.round()}'),
        RangeSlider(
          values: _range,
          min: 0,
          max: 100,
          divisions: 20,
          labels: RangeLabels(
            _range.start.round().toString(),
            _range.end.round().toString(),
          ),
          onChanged: (val) => setState(() => _range = val),
        ),
        Text('পরিসর: ${_range.start.round()} - ${_range.end.round()}'),
      ],
    );
  }
}
```

### DropdownButton
```dart
class DropdownExample extends StatefulWidget {
  const DropdownExample({super.key});

  @override
  State<DropdownExample> createState() => _DropdownExampleState();
}

class _DropdownExampleState extends State<DropdownExample> {
  String? _selected = 'ঢাকা';
  final _cities = ['ঢাকা', 'চট্টগ্রাম', 'সিলেট', 'রাজশাহী', 'খুলনা'];

  @override
  Widget build(BuildContext context) {
    return DropdownButtonFormField<String>(
      value: _selected,
      decoration: const InputDecoration(
        labelText: 'বিভাগ নির্বাচন করুন',
        border: OutlineInputBorder(),
      ),
      items: _cities
          .map((city) => DropdownMenuItem(value: city, child: Text(city)))
          .toList(),
      onChanged: (val) => setState(() => _selected = val),
    );
  }
}
```

---

## ইমেজ ও আইকন

### Image উইজেট
```dart
// নেটওয়ার্ক থেকে
Image.network(
  'https://example.com/image.jpg',
  width: 200,
  height: 150,
  fit: BoxFit.cover,
  loadingBuilder: (context, child, loadingProgress) {
    if (loadingProgress == null) return child;
    return CircularProgressIndicator(
      value: loadingProgress.expectedTotalBytes != null
          ? loadingProgress.cumulativeBytesLoaded / loadingProgress.expectedTotalBytes!
          : null,
    );
  },
  errorBuilder: (context, error, stackTrace) {
    return const Icon(Icons.broken_image, size: 50);
  },
)

// Assets থেকে
Image.asset(
  'assets/images/logo.png',
  width: 100,
  height: 100,
  fit: BoxFit.contain,
)

// গোলাকার ছবি
CircleAvatar(
  radius: 50,
  backgroundImage: NetworkImage('https://example.com/avatar.jpg'),
  backgroundColor: Colors.grey,
  child: const Text('AB'),  // ছবি না থাকলে
)

// BoxFit বিকল্পসমূহ
// BoxFit.cover    – আবৃত করে (ছাঁটা হতে পারে)
// BoxFit.contain  – সম্পূর্ণ দেখায় (ফাঁকা থাকতে পারে)
// BoxFit.fill     – প্রসারিত করে
// BoxFit.fitWidth – প্রস্থ পূর্ণ করে
// BoxFit.fitHeight– উচ্চতা পূর্ণ করে
// BoxFit.none     – মূল আকার
```

### cached_network_image প্যাকেজ
```yaml
dependencies:
  cached_network_image: ^3.3.0
```

```dart
import 'package:cached_network_image/cached_network_image.dart';

CachedNetworkImage(
  imageUrl: 'https://example.com/image.jpg',
  placeholder: (context, url) => const CircularProgressIndicator(),
  errorWidget: (context, url, error) => const Icon(Icons.error),
  fit: BoxFit.cover,
)
```

### Icon উইজেট
```dart
// Material Icons
const Icon(Icons.home, size: 30, color: Colors.blue)
const Icon(Icons.favorite, color: Colors.red)
const Icon(Icons.search)

// Cupertino Icons (iOS স্টাইল)
import 'package:flutter/cupertino.dart';
const Icon(CupertinoIcons.home)
const Icon(CupertinoIcons.heart)

// কাস্টম আইকন (SVG)
// pubspec.yaml: flutter_svg: ^2.0.0
import 'package:flutter_svg/flutter_svg.dart';

SvgPicture.asset(
  'assets/icons/logo.svg',
  width: 50,
  height: 50,
)
```

---

## লিস্ট ও গ্রিড

### ListView
```dart
// সাধারণ ListView
ListView(
  children: [
    ListTile(leading: Icon(Icons.home), title: Text('হোম')),
    ListTile(leading: Icon(Icons.person), title: Text('প্রোফাইল')),
    ListTile(leading: Icon(Icons.settings), title: Text('সেটিংস')),
  ],
)

// ListView.builder – বড় তালিকার জন্য (অলসভাবে তৈরি)
ListView.builder(
  itemCount: 100,
  itemBuilder: (context, index) {
    return ListTile(
      leading: CircleAvatar(child: Text('${index + 1}')),
      title: Text('আইটেম ${index + 1}'),
      subtitle: Text('বিবরণ ${index + 1}'),
      trailing: const Icon(Icons.arrow_forward_ios),
      onTap: () => print('আইটেম $index ক্লিক হয়েছে'),
    );
  },
)

// ListView.separated – বিভাজক সহ
ListView.separated(
  itemCount: items.length,
  separatorBuilder: (context, index) => const Divider(),
  itemBuilder: (context, index) {
    return ListTile(title: Text(items[index]));
  },
)
```

### GridView
```dart
// GridView.count – নির্দিষ্ট কলাম সংখ্যা
GridView.count(
  crossAxisCount: 2,          // ২টি কলাম
  crossAxisSpacing: 8,
  mainAxisSpacing: 8,
  childAspectRatio: 1,        // বর্গক্ষেত্র
  padding: const EdgeInsets.all(8),
  children: List.generate(20, (index) {
    return Card(
      child: Center(child: Text('কার্ড $index')),
    );
  }),
)

// GridView.builder – বড় ডেটার জন্য
GridView.builder(
  gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 3,
    crossAxisSpacing: 4,
    mainAxisSpacing: 4,
    childAspectRatio: 0.75,
  ),
  itemCount: products.length,
  itemBuilder: (context, index) {
    return ProductCard(product: products[index]);
  },
)

// GridView.extent – সর্বোচ্চ প্রস্থ নির্দিষ্ট
GridView.extent(
  maxCrossAxisExtent: 200,  // প্রতিটি আইটেম সর্বোচ্চ ২০০px চওড়া
  children: [...],
)
```

### CustomScrollView ও Sliver
```dart
CustomScrollView(
  slivers: [
    // স্ক্রল করলে ছোট হয়ে যায়
    SliverAppBar(
      expandedHeight: 200,
      floating: false,
      pinned: true,
      flexibleSpace: FlexibleSpaceBar(
        title: const Text('আমার অ্যাপ'),
        background: Image.network('https://example.com/header.jpg', fit: BoxFit.cover),
      ),
    ),
    // স্ক্রলযোগ্য লিস্ট
    SliverList(
      delegate: SliverChildBuilderDelegate(
        (context, index) => ListTile(title: Text('আইটেম $index')),
        childCount: 50,
      ),
    ),
    // স্ক্রলযোগ্য গ্রিড
    SliverGrid(
      gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 2),
      delegate: SliverChildBuilderDelegate(
        (context, index) => Card(child: Center(child: Text('গ্রিড $index'))),
        childCount: 20,
      ),
    ),
  ],
)
```

---

## নেভিগেশন ও রাউটিং

### নামবিহীন রাউটিং (Imperative)
```dart
// নতুন স্ক্রিনে যাওয়া
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const DetailScreen()),
);

// ডেটা পাঠিয়ে যাওয়া
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(id: '123', name: 'পণ্য'),
  ),
);

// বর্তমান স্ক্রিন সরিয়ে নতুন স্ক্রিনে যাওয়া
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => const HomeScreen()),
);

// সব স্ক্রিন সরিয়ে নতুনে যাওয়া
Navigator.pushAndRemoveUntil(
  context,
  MaterialPageRoute(builder: (context) => const LoginScreen()),
  (route) => false,
);

// ফিরে যাওয়া
Navigator.pop(context);

// ডেটা ফিরিয়ে দেওয়া
Navigator.pop(context, 'ব্যবহারকারী নির্বাচিত');

// ডেটা ফিরে পাওয়া
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const SelectionScreen()),
);
print('ফলাফল: $result');
```

### নামযুক্ত রাউটিং (Named Routes)
```dart
// MaterialApp-এ রাউট নির্ধারণ
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => const HomeScreen(),
    '/details': (context) => const DetailScreen(),
    '/profile': (context) => const ProfileScreen(),
    '/settings': (context) => const SettingsScreen(),
  },
)

// রাউটে যাওয়া
Navigator.pushNamed(context, '/details');

// আর্গুমেন্ট পাঠানো
Navigator.pushNamed(
  context,
  '/details',
  arguments: {'id': '123', 'name': 'পণ্যের নাম'},
);

// আর্গুমেন্ট গ্রহণ করা
class DetailScreen extends StatelessWidget {
  const DetailScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final args = ModalRoute.of(context)!.settings.arguments as Map;
    final id = args['id'];
    final name = args['name'];

    return Scaffold(
      appBar: AppBar(title: Text(name)),
      body: Center(child: Text('ID: $id')),
    );
  }
}
```

### GoRouter (সুপারিশকৃত)
```yaml
dependencies:
  go_router: ^13.0.0
```

```dart
import 'package:go_router/go_router.dart';

final _router = GoRouter(
  initialLocation: '/',
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
    ),
    GoRoute(
      path: '/details/:id',
      builder: (context, state) {
        final id = state.pathParameters['id']!;
        return DetailScreen(id: id);
      },
    ),
    GoRoute(
      path: '/profile',
      builder: (context, state) => const ProfileScreen(),
      routes: [
        GoRoute(
          path: 'edit',
          builder: (context, state) => const EditProfileScreen(),
        ),
      ],
    ),
  ],
);

// MaterialApp-এ ব্যবহার
MaterialApp.router(
  routerConfig: _router,
)

// নেভিগেট করা
context.go('/details/123');
context.push('/profile');
context.pop();
```

### Bottom Navigation Bar
```dart
class MainScreen extends StatefulWidget {
  const MainScreen({super.key});

  @override
  State<MainScreen> createState() => _MainScreenState();
}

class _MainScreenState extends State<MainScreen> {
  int _selectedIndex = 0;

  final _pages = [
    const HomeScreen(),
    const SearchScreen(),
    const CartScreen(),
    const ProfileScreen(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _pages[_selectedIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _selectedIndex,
        onTap: (index) => setState(() => _selectedIndex = index),
        type: BottomNavigationBarType.fixed,
        selectedItemColor: Colors.blue,
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'হোম'),
          BottomNavigationBarItem(icon: Icon(Icons.search), label: 'খুঁজুন'),
          BottomNavigationBarItem(icon: Icon(Icons.shopping_cart), label: 'কার্ট'),
          BottomNavigationBarItem(icon: Icon(Icons.person), label: 'প্রোফাইল'),
        ],
      ),
    );
  }
}
```

### Drawer (পাশ মেনু)
```dart
Scaffold(
  drawer: Drawer(
    child: ListView(
      padding: EdgeInsets.zero,
      children: [
        UserAccountsDrawerHeader(
          accountName: const Text('করিম সাহেব'),
          accountEmail: const Text('karim@email.com'),
          currentAccountPicture: const CircleAvatar(
            backgroundImage: NetworkImage('https://example.com/avatar.jpg'),
          ),
          decoration: const BoxDecoration(color: Colors.blue),
        ),
        ListTile(
          leading: const Icon(Icons.home),
          title: const Text('হোম'),
          onTap: () {
            Navigator.pop(context);  // ড্রয়ার বন্ধ করুন
            Navigator.pushNamed(context, '/');
          },
        ),
        ListTile(
          leading: const Icon(Icons.settings),
          title: const Text('সেটিংস'),
          onTap: () => Navigator.pushNamed(context, '/settings'),
        ),
        const Divider(),
        ListTile(
          leading: const Icon(Icons.logout),
          title: const Text('লগ আউট'),
          onTap: () {},
        ),
      ],
    ),
  ),
)
```

---

## স্ক্রল ও সোয়াইপ

### SingleChildScrollView
```dart
SingleChildScrollView(
  scrollDirection: Axis.vertical,  // Axis.horizontal আনুভূমিক
  physics: const BouncingScrollPhysics(),  // iOS বাউন্স ইফেক্ট
  child: Column(
    children: [
      // অনেক উইজেট যা স্ক্রিনে নাও ধরতে পারে
    ],
  ),
)
```

### RefreshIndicator – টেনে রিফ্রেশ
```dart
RefreshIndicator(
  onRefresh: () async {
    await Future.delayed(const Duration(seconds: 1));
    // ডেটা রিলোড করুন
  },
  child: ListView.builder(
    itemCount: items.length,
    itemBuilder: (context, index) => ListTile(title: Text(items[index])),
  ),
)
```

### PageView – পেজ স্লাইড
```dart
class PageViewExample extends StatefulWidget {
  const PageViewExample({super.key});

  @override
  State<PageViewExample> createState() => _PageViewExampleState();
}

class _PageViewExampleState extends State<PageViewExample> {
  final _controller = PageController();
  int _currentPage = 0;

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Expanded(
          child: PageView(
            controller: _controller,
            onPageChanged: (index) => setState(() => _currentPage = index),
            children: const [
              Center(child: Text('পেজ ১', style: TextStyle(fontSize: 30))),
              Center(child: Text('পেজ ২', style: TextStyle(fontSize: 30))),
              Center(child: Text('পেজ ৩', style: TextStyle(fontSize: 30))),
            ],
          ),
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: List.generate(3, (index) {
            return Container(
              margin: const EdgeInsets.all(4),
              width: _currentPage == index ? 16 : 8,
              height: 8,
              decoration: BoxDecoration(
                color: _currentPage == index ? Colors.blue : Colors.grey,
                borderRadius: BorderRadius.circular(4),
              ),
            );
          }),
        ),
      ],
    );
  }
}
```

### Dismissible – সোয়াইপ করে মুছুন
```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return Dismissible(
      key: Key(items[index]),
      direction: DismissDirection.endToStart,
      background: Container(
        color: Colors.red,
        alignment: Alignment.centerRight,
        padding: const EdgeInsets.only(right: 16),
        child: const Icon(Icons.delete, color: Colors.white),
      ),
      onDismissed: (direction) {
        setState(() => items.removeAt(index));
        ScaffoldMessenger.of(context).showSnackBar(
          const SnackBar(content: Text('মুছে ফেলা হয়েছে')),
        );
      },
      child: ListTile(title: Text(items[index])),
    );
  },
)
```

---

## ডায়ালগ ও স্ন্যাকবার

### AlertDialog
```dart
showDialog(
  context: context,
  barrierDismissible: false,  // বাইরে ক্লিক করলে বন্ধ হবে না
  builder: (context) {
    return AlertDialog(
      title: const Text('নিশ্চিত করুন'),
      content: const Text('আপনি কি এটি মুছতে চান?'),
      actions: [
        TextButton(
          onPressed: () => Navigator.pop(context, false),
          child: const Text('না'),
        ),
        ElevatedButton(
          onPressed: () => Navigator.pop(context, true),
          child: const Text('হ্যাঁ'),
        ),
      ],
    );
  },
).then((result) {
  if (result == true) print('মুছে ফেলা হচ্ছে...');
});
```

### BottomSheet
```dart
// Modal Bottom Sheet
showModalBottomSheet(
  context: context,
  isScrollControlled: true,  // কীবোর্ড উঠলেও দেখা যাবে
  shape: const RoundedRectangleBorder(
    borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
  ),
  builder: (context) {
    return Padding(
      padding: EdgeInsets.only(
        bottom: MediaQuery.of(context).viewInsets.bottom,
      ),
      child: Container(
        padding: const EdgeInsets.all(16),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            Container(width: 40, height: 4, color: Colors.grey.shade300),
            const SizedBox(height: 16),
            const Text('বিকল্প নির্বাচন করুন', style: TextStyle(fontSize: 18)),
            const SizedBox(height: 16),
            ListTile(
              leading: const Icon(Icons.camera_alt),
              title: const Text('ক্যামেরা'),
              onTap: () => Navigator.pop(context),
            ),
            ListTile(
              leading: const Icon(Icons.photo),
              title: const Text('গ্যালারি'),
              onTap: () => Navigator.pop(context),
            ),
          ],
        ),
      ),
    );
  },
);
```

### SnackBar
```dart
// সহজ SnackBar
ScaffoldMessenger.of(context).showSnackBar(
  const SnackBar(content: Text('সফলভাবে সংরক্ষিত হয়েছে!')),
);

// কাস্টম SnackBar
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: const Text('ইন্টারনেট সংযোগ নেই'),
    backgroundColor: Colors.red,
    duration: const Duration(seconds: 3),
    behavior: SnackBarBehavior.floating,
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
    action: SnackBarAction(
      label: 'পুনরায় চেষ্টা',
      textColor: Colors.white,
      onPressed: () => print('পুনরায় চেষ্টা হচ্ছে'),
    ),
  ),
);
```

---

## থিম ও ডার্ক মোড

### Theme সেটআপ
```dart
MaterialApp(
  theme: ThemeData(
    useMaterial3: true,
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.blue,
      brightness: Brightness.light,
    ),
    // টেক্সট থিম
    textTheme: const TextTheme(
      headlineLarge: TextStyle(fontSize: 32, fontWeight: FontWeight.bold),
      headlineMedium: TextStyle(fontSize: 24, fontWeight: FontWeight.w600),
      bodyLarge: TextStyle(fontSize: 16),
      bodyMedium: TextStyle(fontSize: 14),
    ),
    // AppBar থিম
    appBarTheme: const AppBarTheme(
      centerTitle: true,
      elevation: 0,
      backgroundColor: Colors.blue,
      foregroundColor: Colors.white,
    ),
    // বাটন থিম
    elevatedButtonTheme: ElevatedButtonThemeData(
      style: ElevatedButton.styleFrom(
        padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 12),
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
      ),
    ),
    // Card থিম
    cardTheme: CardTheme(
      elevation: 2,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
    ),
  ),
  darkTheme: ThemeData(
    useMaterial3: true,
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.blue,
      brightness: Brightness.dark,
    ),
  ),
  themeMode: ThemeMode.system,  // সিস্টেম সেটিং অনুসরণ
)
```

### থিম ব্যবহার করা
```dart
Widget build(BuildContext context) {
  final theme = Theme.of(context);
  final colorScheme = theme.colorScheme;

  return Container(
    color: colorScheme.surface,
    child: Text(
      'থিম রঙ',
      style: theme.textTheme.headlineMedium?.copyWith(
        color: colorScheme.primary,
      ),
    ),
  );
}
```

### Dynamic Theme (ডার্ক/লাইট টগল)
```dart
class ThemeProvider extends ChangeNotifier {
  ThemeMode _themeMode = ThemeMode.system;

  ThemeMode get themeMode => _themeMode;

  void toggleTheme() {
    _themeMode = _themeMode == ThemeMode.light ? ThemeMode.dark : ThemeMode.light;
    notifyListeners();
  }
}
```

---

## অ্যানিমেশন

### AnimatedContainer
```dart
class AnimatedBoxExample extends StatefulWidget {
  const AnimatedBoxExample({super.key});

  @override
  State<AnimatedBoxExample> createState() => _AnimatedBoxExampleState();
}

class _AnimatedBoxExampleState extends State<AnimatedBoxExample> {
  bool _expanded = false;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () => setState(() => _expanded = !_expanded),
      child: AnimatedContainer(
        duration: const Duration(milliseconds: 300),
        curve: Curves.easeInOut,
        width: _expanded ? 250 : 100,
        height: _expanded ? 250 : 100,
        color: _expanded ? Colors.blue : Colors.red,
        child: Center(
          child: Text(
            _expanded ? 'বড়' : 'ছোট',
            style: const TextStyle(color: Colors.white, fontSize: 18),
          ),
        ),
      ),
    );
  }
}
```

### AnimationController ও Tween
```dart
class SpinningWidget extends StatefulWidget {
  const SpinningWidget({super.key});

  @override
  State<SpinningWidget> createState() => _SpinningWidgetState();
}

class _SpinningWidgetState extends State<SpinningWidget>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat();  // বারবার চলে

    _animation = Tween<double>(begin: 0, end: 1).animate(
      CurvedAnimation(parent: _controller, curve: Curves.linear),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return RotationTransition(
      turns: _animation,
      child: const Icon(Icons.refresh, size: 50, color: Colors.blue),
    );
  }
}
```

### Hero অ্যানিমেশন (পেজ ট্রানজিশন)
```dart
// প্রথম পেজে
GestureDetector(
  onTap: () => Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => const DetailPage()),
  ),
  child: Hero(
    tag: 'product-image-1',
    child: Image.network('https://example.com/product.jpg', height: 100),
  ),
)

// দ্বিতীয় পেজে
class DetailPage extends StatelessWidget {
  const DetailPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Hero(
        tag: 'product-image-1',
        child: Image.network('https://example.com/product.jpg'),
      ),
    );
  }
}
```

### Lottie অ্যানিমেশন
```yaml
dependencies:
  lottie: ^3.0.0
```

```dart
import 'package:lottie/lottie.dart';

// Assets থেকে
Lottie.asset(
  'assets/animations/loading.json',
  width: 200,
  height: 200,
  repeat: true,
)

// নেটওয়ার্ক থেকে
Lottie.network(
  'https://assets.lottiefiles.com/animation.json',
)
```

---

## জেস্চার ডিটেকশন

### GestureDetector
```dart
GestureDetector(
  // একক ট্যাপ
  onTap: () => print('ট্যাপ হয়েছে'),

  // দ্বিগুণ ট্যাপ
  onDoubleTap: () => print('ডাবল ট্যাপ'),

  // দীর্ঘ প্রেস
  onLongPress: () => print('দীর্ঘ প্রেস'),

  // ড্র্যাগ
  onPanStart: (details) => print('ড্র্যাগ শুরু'),
  onPanUpdate: (details) {
    print('ড্র্যাগ: ${details.delta}');
  },
  onPanEnd: (details) => print('ড্র্যাগ শেষ'),

  // স্কেল (পিঞ্চ জুম)
  onScaleUpdate: (details) => print('স্কেল: ${details.scale}'),

  child: Container(
    width: 200,
    height: 200,
    color: Colors.blue,
    child: const Center(child: Text('স্পর্শ করুন')),
  ),
)
```

### InkWell (রিপল ইফেক্ট সহ)
```dart
InkWell(
  onTap: () => print('ক্লিক'),
  borderRadius: BorderRadius.circular(8),
  splashColor: Colors.blue.withOpacity(0.3),
  child: Padding(
    padding: const EdgeInsets.all(16),
    child: const Text('রিপল ইফেক্ট'),
  ),
)
```

### ড্র্যাগেবল উইজেট
```dart
class DraggableExample extends StatefulWidget {
  const DraggableExample({super.key});

  @override
  State<DraggableExample> createState() => _DraggableExampleState();
}

class _DraggableExampleState extends State<DraggableExample> {
  String? _accepted;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Draggable<String>(
          data: 'আম',
          feedback: const Material(
            color: Colors.transparent,
            child: Icon(Icons.shopping_bag, size: 50, color: Colors.orange),
          ),
          childWhenDragging: const Opacity(opacity: 0.5, child: Icon(Icons.shopping_bag, size: 50)),
          child: const Icon(Icons.shopping_bag, size: 50, color: Colors.orange),
        ),
        DragTarget<String>(
          onAcceptWithDetails: (details) => setState(() => _accepted = details.data),
          builder: (context, candidateData, rejectedData) {
            return Container(
              width: 200,
              height: 200,
              color: candidateData.isNotEmpty ? Colors.green.shade100 : Colors.grey.shade200,
              child: Center(child: Text(_accepted ?? 'এখানে ছেড়ে দিন')),
            );
          },
        ),
      ],
    );
  }
}
```

---

## ফর্ম ও ভ্যালিডেশন

### Form উইজেট
```dart
class RegistrationForm extends StatefulWidget {
  const RegistrationForm({super.key});

  @override
  State<RegistrationForm> createState() => _RegistrationFormState();
}

class _RegistrationFormState extends State<RegistrationForm> {
  final _formKey = GlobalKey<FormState>();
  final _nameController = TextEditingController();
  final _emailController = TextEditingController();
  final _phoneController = TextEditingController();
  final _passwordController = TextEditingController();
  bool _obscurePassword = true;

  @override
  void dispose() {
    _nameController.dispose();
    _emailController.dispose();
    _phoneController.dispose();
    _passwordController.dispose();
    super.dispose();
  }

  void _submit() {
    if (_formKey.currentState!.validate()) {
      // ফর্ম বৈধ
      _formKey.currentState!.save();
      print('নাম: ${_nameController.text}');
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('নিবন্ধন সফল!')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          // নাম
          TextFormField(
            controller: _nameController,
            decoration: const InputDecoration(
              labelText: 'পুরো নাম *',
              prefixIcon: Icon(Icons.person),
              border: OutlineInputBorder(),
            ),
            validator: (value) {
              if (value == null || value.isEmpty) return 'নাম প্রয়োজন';
              if (value.length < 3) return 'নাম কমপক্ষে ৩ অক্ষরের হতে হবে';
              return null;
            },
          ),
          const SizedBox(height: 16),

          // ইমেইল
          TextFormField(
            controller: _emailController,
            keyboardType: TextInputType.emailAddress,
            decoration: const InputDecoration(
              labelText: 'ইমেইল *',
              prefixIcon: Icon(Icons.email),
              border: OutlineInputBorder(),
            ),
            validator: (value) {
              if (value == null || value.isEmpty) return 'ইমেইল প্রয়োজন';
              if (!RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(value)) {
                return 'বৈধ ইমেইল লিখুন';
              }
              return null;
            },
          ),
          const SizedBox(height: 16),

          // ফোন
          TextFormField(
            controller: _phoneController,
            keyboardType: TextInputType.phone,
            decoration: const InputDecoration(
              labelText: 'ফোন নম্বর *',
              prefixIcon: Icon(Icons.phone),
              prefixText: '+880 ',
              border: OutlineInputBorder(),
            ),
            validator: (value) {
              if (value == null || value.isEmpty) return 'ফোন নম্বর প্রয়োজন';
              if (!RegExp(r'^01[3-9]\d{8}$').hasMatch(value)) {
                return 'বৈধ বাংলাদেশি নম্বর লিখুন';
              }
              return null;
            },
          ),
          const SizedBox(height: 16),

          // পাসওয়ার্ড
          TextFormField(
            controller: _passwordController,
            obscureText: _obscurePassword,
            decoration: InputDecoration(
              labelText: 'পাসওয়ার্ড *',
              prefixIcon: const Icon(Icons.lock),
              suffixIcon: IconButton(
                icon: Icon(_obscurePassword ? Icons.visibility : Icons.visibility_off),
                onPressed: () => setState(() => _obscurePassword = !_obscurePassword),
              ),
              border: const OutlineInputBorder(),
            ),
            validator: (value) {
              if (value == null || value.isEmpty) return 'পাসওয়ার্ড প্রয়োজন';
              if (value.length < 8) return 'পাসওয়ার্ড কমপক্ষে ৮ অক্ষরের হতে হবে';
              return null;
            },
          ),
          const SizedBox(height: 24),

          // জমা বাটন
          SizedBox(
            width: double.infinity,
            child: ElevatedButton(
              onPressed: _submit,
              child: const Text('নিবন্ধন করুন'),
            ),
          ),
        ],
      ),
    );
  }
}
```

---

## HTTP রিকোয়েস্ট ও API

### http প্যাকেজ
```yaml
dependencies:
  http: ^1.1.0
```

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  static const String _baseUrl = 'https://jsonplaceholder.typicode.com';

  // GET রিকোয়েস্ট
  Future<List<dynamic>> getPosts() async {
    try {
      final response = await http.get(
        Uri.parse('$_baseUrl/posts'),
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer TOKEN',
        },
      );

      if (response.statusCode == 200) {
        return jsonDecode(response.body);
      } else {
        throw Exception('ত্রুটি: ${response.statusCode}');
      }
    } catch (e) {
      throw Exception('নেটওয়ার্ক ত্রুটি: $e');
    }
  }

  // POST রিকোয়েস্ট
  Future<Map<String, dynamic>> createPost(Map<String, dynamic> data) async {
    final response = await http.post(
      Uri.parse('$_baseUrl/posts'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode(data),
    );

    if (response.statusCode == 201) {
      return jsonDecode(response.body);
    } else {
      throw Exception('তৈরি ব্যর্থ: ${response.statusCode}');
    }
  }

  // PUT রিকোয়েস্ট
  Future<Map<String, dynamic>> updatePost(int id, Map<String, dynamic> data) async {
    final response = await http.put(
      Uri.parse('$_baseUrl/posts/$id'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode(data),
    );
    return jsonDecode(response.body);
  }

  // DELETE রিকোয়েস্ট
  Future<void> deletePost(int id) async {
    await http.delete(Uri.parse('$_baseUrl/posts/$id'));
  }
}
```

### Dio প্যাকেজ (উন্নত)
```yaml
dependencies:
  dio: ^5.4.0
```

```dart
import 'package:dio/dio.dart';

class DioApiService {
  late final Dio _dio;

  DioApiService() {
    _dio = Dio(BaseOptions(
      baseUrl: 'https://api.example.com',
      connectTimeout: const Duration(seconds: 10),
      receiveTimeout: const Duration(seconds: 10),
      headers: {'Content-Type': 'application/json'},
    ));

    // ইন্টারসেপ্টর যোগ করুন
    _dio.interceptors.add(InterceptorsWrapper(
      onRequest: (options, handler) {
        print('রিকোয়েস্ট: ${options.method} ${options.path}');
        // টোকেন যোগ করুন
        options.headers['Authorization'] = 'Bearer ${getToken()}';
        handler.next(options);
      },
      onResponse: (response, handler) {
        print('রেসপন্স: ${response.statusCode}');
        handler.next(response);
      },
      onError: (DioException error, handler) {
        print('ত্রুটি: ${error.message}');
        if (error.response?.statusCode == 401) {
          // টোকেন রিফ্রেশ করুন
        }
        handler.next(error);
      },
    ));
  }

  Future<List<dynamic>> getUsers() async {
    final response = await _dio.get('/users');
    return response.data;
  }

  String getToken() => 'your-token-here';
}
```

### FutureBuilder দিয়ে UI
```dart
class PostListScreen extends StatelessWidget {
  final ApiService _api = ApiService();

  PostListScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('পোস্টসমূহ')),
      body: FutureBuilder<List<dynamic>>(
        future: _api.getPosts(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Center(child: CircularProgressIndicator());
          }
          if (snapshot.hasError) {
            return Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  const Icon(Icons.error, size: 50, color: Colors.red),
                  const SizedBox(height: 8),
                  Text('ত্রুটি: ${snapshot.error}'),
                  ElevatedButton(
                    onPressed: () {},
                    child: const Text('পুনরায় চেষ্টা'),
                  ),
                ],
              ),
            );
          }
          final posts = snapshot.data!;
          return ListView.builder(
            itemCount: posts.length,
            itemBuilder: (context, index) {
              final post = posts[index];
              return ListTile(
                title: Text(post['title']),
                subtitle: Text(post['body'], maxLines: 2, overflow: TextOverflow.ellipsis),
              );
            },
          );
        },
      ),
    );
  }
}
```

---

## JSON পার্সিং

### মডেল ক্লাস তৈরি
```dart
class User {
  final int id;
  final String name;
  final String email;
  final String phone;
  final Address address;

  const User({
    required this.id,
    required this.name,
    required this.email,
    required this.phone,
    required this.address,
  });

  // JSON থেকে User তৈরি
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'] ?? 0,
      name: json['name'] ?? '',
      email: json['email'] ?? '',
      phone: json['phone'] ?? '',
      address: Address.fromJson(json['address'] ?? {}),
    );
  }

  // User থেকে JSON তৈরি
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
      'phone': phone,
      'address': address.toJson(),
    };
  }

  @override
  String toString() => 'User(id: $id, name: $name)';
}

class Address {
  final String street;
  final String city;
  final String country;

  const Address({required this.street, required this.city, required this.country});

  factory Address.fromJson(Map<String, dynamic> json) {
    return Address(
      street: json['street'] ?? '',
      city: json['city'] ?? '',
      country: json['country'] ?? '',
    );
  }

  Map<String, dynamic> toJson() {
    return {'street': street, 'city': city, 'country': country};
  }
}

// ব্যবহার
final jsonStr = '{"id":1,"name":"করিম","email":"karim@email.com","phone":"01711111111","address":{"street":"মিরপুর ১","city":"ঢাকা","country":"বাংলাদেশ"}}';
final user = User.fromJson(jsonDecode(jsonStr));
print(user.name);  // করিম
print(jsonEncode(user.toJson()));  // JSON স্ট্রিং
```

### json_serializable (কোড জেনারেশন)
```yaml
dependencies:
  json_annotation: ^4.8.1

dev_dependencies:
  build_runner: ^2.4.0
  json_serializable: ^6.7.0
```

```dart
import 'package:json_annotation/json_annotation.dart';
part 'product.g.dart';  // জেনারেটেড ফাইল

@JsonSerializable()
class Product {
  final int id;
  final String title;
  final double price;

  @JsonKey(name: 'image_url')  // JSON-এ ভিন্ন নাম
  final String imageUrl;

  const Product({
    required this.id,
    required this.title,
    required this.price,
    required this.imageUrl,
  });

  factory Product.fromJson(Map<String, dynamic> json) => _$ProductFromJson(json);
  Map<String, dynamic> toJson() => _$ProductToJson(this);
}

// কোড জেনারেট করুন:
// dart run build_runner build
```

---

## লোকাল স্টোরেজ

### SharedPreferences
```yaml
dependencies:
  shared_preferences: ^2.2.0
```

```dart
import 'package:shared_preferences/shared_preferences.dart';

class PreferencesService {
  static const String _tokenKey = 'auth_token';
  static const String _userIdKey = 'user_id';
  static const String _isDarkModeKey = 'is_dark_mode';

  // সংরক্ষণ
  Future<void> saveToken(String token) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString(_tokenKey, token);
  }

  // পড়া
  Future<String?> getToken() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getString(_tokenKey);
  }

  // মুছে ফেলা
  Future<void> removeToken() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.remove(_tokenKey);
  }

  // সব ডেটা মুছুন (লগ আউট)
  Future<void> clearAll() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.clear();
  }

  // ডার্ক মোড সেটিং
  Future<void> setDarkMode(bool isDark) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool(_isDarkModeKey, isDark);
  }

  Future<bool> getDarkMode() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getBool(_isDarkModeKey) ?? false;
  }
}
```

### Hive (দ্রুত NoSQL)
```yaml
dependencies:
  hive: ^2.2.3
  hive_flutter: ^1.1.0

dev_dependencies:
  hive_generator: ^2.0.0
  build_runner: ^2.4.0
```

```dart
import 'package:hive_flutter/hive_flutter.dart';

// মডেল ক্লাস
@HiveType(typeId: 0)
class Task extends HiveObject {
  @HiveField(0)
  late String title;

  @HiveField(1)
  late bool isCompleted;

  @HiveField(2)
  late DateTime createdAt;
}

// ইনিশিয়ালাইজেশন (main.dart)
Future<void> main() async {
  await Hive.initFlutter();
  Hive.registerAdapter(TaskAdapter());
  await Hive.openBox<Task>('tasks');
  runApp(const MyApp());
}

// ব্যবহার
class HiveService {
  Box<Task> get _taskBox => Hive.box<Task>('tasks');

  void addTask(Task task) => _taskBox.add(task);

  List<Task> getAllTasks() => _taskBox.values.toList();

  void updateTask(int index, Task task) => _taskBox.putAt(index, task);

  void deleteTask(int index) => _taskBox.deleteAt(index);
}
```

### SQLite (sqflite)
```yaml
dependencies:
  sqflite: ^2.3.0
  path: ^1.9.0
```

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static Database? _database;

  Future<Database> get database async {
    _database ??= await _initDB();
    return _database!;
  }

  Future<Database> _initDB() async {
    final dbPath = await getDatabasesPath();
    final path = join(dbPath, 'app.db');

    return openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute('''
          CREATE TABLE users (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            email TEXT UNIQUE NOT NULL,
            created_at TEXT DEFAULT CURRENT_TIMESTAMP
          )
        ''');
      },
    );
  }

  // ঢোকানো
  Future<int> insertUser(Map<String, dynamic> user) async {
    final db = await database;
    return db.insert('users', user, conflictAlgorithm: ConflictAlgorithm.replace);
  }

  // সব পড়া
  Future<List<Map<String, dynamic>>> getAllUsers() async {
    final db = await database;
    return db.query('users', orderBy: 'created_at DESC');
  }

  // আপডেট
  Future<int> updateUser(int id, Map<String, dynamic> user) async {
    final db = await database;
    return db.update('users', user, where: 'id = ?', whereArgs: [id]);
  }

  // মুছে ফেলা
  Future<int> deleteUser(int id) async {
    final db = await database;
    return db.delete('users', where: 'id = ?', whereArgs: [id]);
  }
}
```

---

## স্টেট ম্যানেজমেন্ট

### setState এর সীমাবদ্ধতা
```dart
// ❌ সমস্যা: ডিপ নেস্টেড উইজেটে state পাঠানো কঠিন
class GrandParent extends StatefulWidget {
  const GrandParent({super.key});
  @override
  State<GrandParent> createState() => _GrandParentState();
}

class _GrandParentState extends State<GrandParent> {
  int count = 0;

  @override
  Widget build(BuildContext context) {
    return Parent(
      count: count,
      onIncrement: () => setState(() => count++),
    );
  }
}
// count ও callback কে Parent → Child → GrandChild-এ পাঠাতে হয়
// এই সমস্যাকে "Prop Drilling" বলে
```

### InheritedWidget (মূল ভিত্তি)
```dart
class CounterInherited extends InheritedWidget {
  final int count;
  final VoidCallback onIncrement;

  const CounterInherited({
    super.key,
    required this.count,
    required this.onIncrement,
    required super.child,
  });

  static CounterInherited of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<CounterInherited>()!;
  }

  @override
  bool updateShouldNotify(CounterInherited oldWidget) {
    return count != oldWidget.count;
  }
}
```

---

## Provider

### Provider সেটআপ
```yaml
dependencies:
  provider: ^6.1.0
```

```dart
import 'package:provider/provider.dart';

// ChangeNotifier ক্লাস
class CartProvider extends ChangeNotifier {
  final List<CartItem> _items = [];

  List<CartItem> get items => List.unmodifiable(_items);
  int get itemCount => _items.length;
  double get total => _items.fold(0, (sum, item) => sum + item.price * item.quantity);

  void addItem(Product product) {
    final existing = _items.where((i) => i.product.id == product.id).firstOrNull;
    if (existing != null) {
      existing.quantity++;
    } else {
      _items.add(CartItem(product: product, quantity: 1, price: product.price));
    }
    notifyListeners();
  }

  void removeItem(int productId) {
    _items.removeWhere((item) => item.product.id == productId);
    notifyListeners();
  }

  void clear() {
    _items.clear();
    notifyListeners();
  }
}

// main.dart-এ Provider ব্যবহার
void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => CartProvider()),
        ChangeNotifierProvider(create: (_) => AuthProvider()),
        ChangeNotifierProvider(create: (_) => ThemeProvider()),
      ],
      child: const MyApp(),
    ),
  );
}

// উইজেটে ব্যবহার
class CartScreen extends StatelessWidget {
  const CartScreen({super.key});

  @override
  Widget build(BuildContext context) {
    // পড়া ও পুনর্নির্মাণ ট্রিগার করে
    final cart = context.watch<CartProvider>();

    // শুধু পড়া, পুনর্নির্মাণ ট্রিগার করে না
    // final cart = context.read<CartProvider>();

    // নির্দিষ্ট মান পড়া
    // final total = context.select<CartProvider, double>((c) => c.total);

    return Scaffold(
      appBar: AppBar(
        title: Text('কার্ট (${cart.itemCount})'),
        actions: [
          IconButton(
            icon: const Icon(Icons.delete),
            onPressed: () => context.read<CartProvider>().clear(),
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: cart.items.length,
        itemBuilder: (context, index) {
          final item = cart.items[index];
          return ListTile(
            title: Text(item.product.name),
            subtitle: Text('৳${item.price} × ${item.quantity}'),
            trailing: Text('৳${(item.price * item.quantity).toStringAsFixed(2)}'),
          );
        },
      ),
      bottomNavigationBar: BottomAppBar(
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Text('মোট: ৳${cart.total.toStringAsFixed(2)}', style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
              ElevatedButton(onPressed: () {}, child: const Text('অর্ডার দিন')),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## Riverpod

### Riverpod সেটআপ
```yaml
dependencies:
  flutter_riverpod: ^2.4.0
```

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Provider ধরনসমূহ

// ১. Provider – সাধারণ মান
final greetingProvider = Provider<String>((ref) {
  return 'স্বাগতম Flutter-এ!';
});

// ২. StateProvider – সহজ state
final counterProvider = StateProvider<int>((ref) => 0);

// ৩. StateNotifierProvider – জটিল state
class TodoNotifier extends StateNotifier<List<Todo>> {
  TodoNotifier() : super([]);

  void add(String title) {
    state = [...state, Todo(title: title, isCompleted: false)];
  }

  void toggle(int index) {
    state = [
      for (int i = 0; i < state.length; i++)
        if (i == index) state[i].copyWith(isCompleted: !state[i].isCompleted)
        else state[i],
    ];
  }

  void remove(int index) {
    state = [...state]..removeAt(index);
  }
}

final todoProvider = StateNotifierProvider<TodoNotifier, List<Todo>>((ref) {
  return TodoNotifier();
});

// ৪. FutureProvider – async ডেটা
final postsProvider = FutureProvider<List<Post>>((ref) async {
  final api = ApiService();
  return api.getPosts();
});

// main.dart
void main() {
  runApp(const ProviderScope(child: MyApp()));
}

// উইজেটে ব্যবহার (ConsumerWidget)
class TodoListScreen extends ConsumerWidget {
  const TodoListScreen({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final todos = ref.watch(todoProvider);
    final counter = ref.watch(counterProvider);

    return Scaffold(
      appBar: AppBar(title: Text('কাজের তালিকা ($counter)')),
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          final todo = todos[index];
          return CheckboxListTile(
            title: Text(todo.title),
            value: todo.isCompleted,
            onChanged: (_) => ref.read(todoProvider.notifier).toggle(index),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          ref.read(todoProvider.notifier).add('নতুন কাজ ${todos.length + 1}');
          ref.read(counterProvider.notifier).state++;
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

## BLoC প্যাটার্ন

### BLoC সেটআপ
```yaml
dependencies:
  flutter_bloc: ^8.1.3
  equatable: ^2.0.5
```

```dart
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:equatable/equatable.dart';

// ইভেন্ট
abstract class AuthEvent extends Equatable {
  const AuthEvent();
  @override
  List<Object> get props => [];
}

class LoginEvent extends AuthEvent {
  final String email;
  final String password;
  const LoginEvent({required this.email, required this.password});
  @override
  List<Object> get props => [email, password];
}

class LogoutEvent extends AuthEvent {}

// স্টেট
abstract class AuthState extends Equatable {
  const AuthState();
  @override
  List<Object?> get props => [];
}

class AuthInitial extends AuthState {}
class AuthLoading extends AuthState {}
class AuthAuthenticated extends AuthState {
  final User user;
  const AuthAuthenticated(this.user);
  @override
  List<Object> get props => [user];
}
class AuthError extends AuthState {
  final String message;
  const AuthError(this.message);
  @override
  List<Object> get props => [message];
}

// BLoC
class AuthBloc extends Bloc<AuthEvent, AuthState> {
  final AuthRepository _authRepository;

  AuthBloc({required AuthRepository authRepository})
      : _authRepository = authRepository,
        super(AuthInitial()) {

    on<LoginEvent>(_onLogin);
    on<LogoutEvent>(_onLogout);
  }

  Future<void> _onLogin(LoginEvent event, Emitter<AuthState> emit) async {
    emit(AuthLoading());
    try {
      final user = await _authRepository.login(event.email, event.password);
      emit(AuthAuthenticated(user));
    } catch (e) {
      emit(AuthError(e.toString()));
    }
  }

  void _onLogout(LogoutEvent event, Emitter<AuthState> emit) {
    emit(AuthInitial());
  }
}

// UI-তে ব্যবহার
class LoginScreen extends StatelessWidget {
  const LoginScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => AuthBloc(authRepository: AuthRepository()),
      child: BlocConsumer<AuthBloc, AuthState>(
        listener: (context, state) {
          if (state is AuthAuthenticated) {
            Navigator.pushReplacementNamed(context, '/home');
          } else if (state is AuthError) {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(content: Text(state.message)),
            );
          }
        },
        builder: (context, state) {
          if (state is AuthLoading) {
            return const Center(child: CircularProgressIndicator());
          }
          return Scaffold(
            body: Center(
              child: ElevatedButton(
                onPressed: () {
                  context.read<AuthBloc>().add(
                    const LoginEvent(email: 'test@test.com', password: '123456'),
                  );
                },
                child: const Text('লগইন'),
              ),
            ),
          );
        },
      ),
    );
  }
}
```

---

## Firebase ইন্টিগ্রেশন

### Firebase সেটআপ
```yaml
dependencies:
  firebase_core: ^2.24.0
  firebase_auth: ^4.15.0
  cloud_firestore: ^4.13.0
  firebase_storage: ^11.5.0
```

```bash
# FlutterFire CLI দিয়ে সেটআপ
dart pub global activate flutterfire_cli
flutterfire configure
```

```dart
// main.dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
  runApp(const MyApp());
}
```

### Firebase Auth
```dart
import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  final _auth = FirebaseAuth.instance;

  // ইমেইল নিবন্ধন
  Future<UserCredential> signUp(String email, String password) async {
    return _auth.createUserWithEmailAndPassword(email: email, password: password);
  }

  // ইমেইল লগইন
  Future<UserCredential> signIn(String email, String password) async {
    return _auth.signInWithEmailAndPassword(email: email, password: password);
  }

  // লগ আউট
  Future<void> signOut() => _auth.signOut();

  // বর্তমান ব্যবহারকারী
  User? get currentUser => _auth.currentUser;

  // অথ স্টেট পরিবর্তন শোনা
  Stream<User?> get authStateChanges => _auth.authStateChanges();
}
```

### Firestore
```dart
import 'package:cloud_firestore/cloud_firestore.dart';

class FirestoreService {
  final _db = FirebaseFirestore.instance;

  // ডেটা যোগ করা
  Future<void> addProduct(Map<String, dynamic> product) async {
    await _db.collection('products').add({
      ...product,
      'createdAt': FieldValue.serverTimestamp(),
    });
  }

  // সব ডেটা পড়া (রিয়েলটাইম স্ট্রিম)
  Stream<QuerySnapshot> getProducts() {
    return _db.collection('products')
        .orderBy('createdAt', descending: true)
        .snapshots();
  }

  // নির্দিষ্ট ডেটা পড়া
  Future<DocumentSnapshot> getProduct(String id) {
    return _db.collection('products').doc(id).get();
  }

  // আপডেট করা
  Future<void> updateProduct(String id, Map<String, dynamic> data) {
    return _db.collection('products').doc(id).update(data);
  }

  // মুছে ফেলা
  Future<void> deleteProduct(String id) {
    return _db.collection('products').doc(id).delete();
  }

  // কোয়েরি
  Future<QuerySnapshot> searchProducts(String category) {
    return _db.collection('products')
        .where('category', isEqualTo: category)
        .where('price', isLessThan: 1000)
        .limit(20)
        .get();
  }
}

// StreamBuilder দিয়ে রিয়েলটাইম UI
StreamBuilder<QuerySnapshot>(
  stream: FirestoreService().getProducts(),
  builder: (context, snapshot) {
    if (snapshot.hasError) return const Text('ত্রুটি হয়েছে');
    if (!snapshot.hasData) return const CircularProgressIndicator();

    final docs = snapshot.data!.docs;
    return ListView.builder(
      itemCount: docs.length,
      itemBuilder: (context, index) {
        final data = docs[index].data() as Map<String, dynamic>;
        return ListTile(
          title: Text(data['name']),
          subtitle: Text('৳${data['price']}'),
        );
      },
    );
  },
)
```

---

## পুশ নোটিফিকেশন

### Firebase Cloud Messaging (FCM)
```yaml
dependencies:
  firebase_messaging: ^14.7.0
  flutter_local_notifications: ^16.3.0
```

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

// ব্যাকগ্রাউন্ড হ্যান্ডলার (top-level function)
@pragma('vm:entry-point')
Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  await Firebase.initializeApp();
  print('ব্যাকগ্রাউন্ড নোটিফিকেশন: ${message.messageId}');
}

class NotificationService {
  final _messaging = FirebaseMessaging.instance;

  Future<void> initialize() async {
    // পারমিশন চাওয়া
    await _messaging.requestPermission(
      alert: true,
      badge: true,
      sound: true,
    );

    // ব্যাকগ্রাউন্ড হ্যান্ডলার
    FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);

    // FCM টোকেন
    final token = await _messaging.getToken();
    print('FCM Token: $token');

    // ফোরগ্রাউন্ড নোটিফিকেশন
    FirebaseMessaging.onMessage.listen((RemoteMessage message) {
      print('ফোরগ্রাউন্ড: ${message.notification?.title}');
      // লোকাল নোটিফিকেশন দেখান
    });

    // নোটিফিকেশন ক্লিক থেকে খোলা
    FirebaseMessaging.onMessageOpenedApp.listen((RemoteMessage message) {
      print('নোটিফিকেশন খুলেছে: ${message.data}');
      // নির্দিষ্ট স্ক্রিনে নেভিগেট করুন
    });
  }
}
```

---

## প্ল্যাটফর্ম চ্যানেল

### নেটিভ কোড কল করা
```dart
// Flutter পাশে
import 'package:flutter/services.dart';

class BatteryService {
  static const _channel = MethodChannel('com.example.app/battery');

  Future<int> getBatteryLevel() async {
    try {
      final batteryLevel = await _channel.invokeMethod<int>('getBatteryLevel');
      return batteryLevel ?? 0;
    } on PlatformException catch (e) {
      print('ত্রুটি: ${e.message}');
      return 0;
    }
  }
}
```

```kotlin
// Android (MainActivity.kt)
class MainActivity: FlutterActivity() {
    private val CHANNEL = "com.example.app/battery"

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler { call, result ->
            if (call.method == "getBatteryLevel") {
                val batteryLevel = getBatteryLevel()
                if (batteryLevel != -1) result.success(batteryLevel)
                else result.error("UNAVAILABLE", "Battery level not available.", null)
            } else {
                result.notImplemented()
            }
        }
    }

    private fun getBatteryLevel(): Int {
        val batteryManager = getSystemService(Context.BATTERY_SERVICE) as BatteryManager
        return batteryManager.getIntProperty(BatteryManager.BATTERY_PROPERTY_CAPACITY)
    }
}
```

---

## টেস্টিং

### Unit Test
```dart
// test/unit/cart_provider_test.dart
import 'package:test/test.dart';

void main() {
  group('CartProvider পরীক্ষা', () {
    late CartProvider cart;

    setUp(() {
      cart = CartProvider();
    });

    test('শুরুতে কার্ট খালি থাকে', () {
      expect(cart.items, isEmpty);
      expect(cart.total, equals(0.0));
    });

    test('আইটেম যোগ করা যায়', () {
      final product = Product(id: 1, name: 'আম', price: 50.0);
      cart.addItem(product);
      expect(cart.items.length, equals(1));
      expect(cart.total, equals(50.0));
    });

    test('একই আইটেম দুইবার যোগ করলে পরিমাণ বাড়ে', () {
      final product = Product(id: 1, name: 'আম', price: 50.0);
      cart.addItem(product);
      cart.addItem(product);
      expect(cart.items.length, equals(1));
      expect(cart.items[0].quantity, equals(2));
      expect(cart.total, equals(100.0));
    });

    test('আইটেম মুছে ফেলা যায়', () {
      final product = Product(id: 1, name: 'আম', price: 50.0);
      cart.addItem(product);
      cart.removeItem(1);
      expect(cart.items, isEmpty);
    });
  });
}
```

### Widget Test
```dart
// test/widget/product_card_test.dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  testWidgets('ProductCard সঠিকভাবে রেন্ডার হয়', (WidgetTester tester) async {
    bool tapped = false;

    await tester.pumpWidget(
      MaterialApp(
        home: ProductCard(
          name: 'আম',
          price: 120.0,
          imageUrl: 'https://example.com/mango.jpg',
          onTap: () => tapped = true,
        ),
      ),
    );

    // পণ্যের নাম দেখা যাচ্ছে
    expect(find.text('আম'), findsOneWidget);

    // মূল্য দেখা যাচ্ছে
    expect(find.text('৳120.00'), findsOneWidget);

    // ক্লিক কাজ করছে
    await tester.tap(find.byType(GestureDetector));
    expect(tapped, isTrue);
  });

  testWidgets('ফর্ম ভ্যালিডেশন কাজ করছে', (WidgetTester tester) async {
    await tester.pumpWidget(const MaterialApp(home: RegistrationForm()));

    // খালি ফর্ম জমা দিন
    await tester.tap(find.text('নিবন্ধন করুন'));
    await tester.pump();

    // ত্রুটি বার্তা দেখায়
    expect(find.text('নাম প্রয়োজন'), findsOneWidget);
    expect(find.text('ইমেইল প্রয়োজন'), findsOneWidget);
  });
}
```

### Integration Test
```dart
// integration_test/app_test.dart
import 'package:integration_test/integration_test.dart';
import 'package:flutter_test/flutter_test.dart';

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('সম্পূর্ণ লগইন প্রবাহ পরীক্ষা', (tester) async {
    await tester.pumpWidget(const MyApp());
    await tester.pumpAndSettle();

    // ইমেইল টাইপ করুন
    await tester.enterText(find.byKey(const Key('email_field')), 'test@test.com');

    // পাসওয়ার্ড টাইপ করুন
    await tester.enterText(find.byKey(const Key('password_field')), '123456');

    // লগইন বাটনে ক্লিক
    await tester.tap(find.byKey(const Key('login_button')));
    await tester.pumpAndSettle();

    // হোম স্ক্রিনে এসেছে কিনা যাচাই
    expect(find.byType(HomeScreen), findsOneWidget);
  });
}
```

---

## পারফরম্যান্স অপটিমাইজেশন

### const উইজেট ব্যবহার
```dart
// ❌ প্রতিবার নতুন অবজেক্ট তৈরি হয়
Widget build(BuildContext context) {
  return Column(
    children: [
      Text('স্থির টেক্সট'),  // setState()-এ পুনর্নির্মাণ হয়
    ],
  );
}

// ✅ একবার তৈরি হয়, ক্যাশে থাকে
Widget build(BuildContext context) {
  return const Column(
    children: [
      Text('স্থির টেক্সট'),  // পুনর্নির্মাণ হয় না
    ],
  );
}
```

### ListView অপটিমাইজেশন
```dart
// ❌ ছোট তালিকার জন্য ঠিক আছে, কিন্তু বড়র জন্য নয়
ListView(children: items.map((i) => ItemWidget(i)).toList())

// ✅ অলস লোডিং – স্ক্রিনে যা দেখা যায় শুধু তাই তৈরি হয়
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) => ItemWidget(items[index]),
)
```

### RepaintBoundary – রিপেইন্ট সীমানা
```dart
// ঘন ঘন আপডেট হওয়া অংশকে আলাদা রাখুন
RepaintBoundary(
  child: AnimatedWidget(),  // শুধু এই অংশ পুনরায় আঁকা হবে
)
```

### Selector দিয়ে অতিরিক্ত পুনর্নির্মাণ এড়ানো
```dart
// পুরো Provider পরিবর্তন হলেও শুধু নির্বাচিত মান পরিবর্তে পুনর্নির্মাণ
Selector<CartProvider, int>(
  selector: (_, cart) => cart.itemCount,  // শুধু itemCount দেখে
  builder: (_, count, __) => Badge(count: count),
)
```

### compute() – ভারী কাজ আলাদা Thread-এ
```dart
import 'package:flutter/foundation.dart';

// ভারী JSON পার্সিং
final parsed = await compute(_parseJson, response.body);

List<Product> _parseJson(String body) {
  final json = jsonDecode(body) as List;
  return json.map((e) => Product.fromJson(e)).toList();
}
```

### DevTools দিয়ে পারফরম্যান্স বিশ্লেষণ
```bash
# DevTools খুলুন
flutter pub global activate devtools
flutter pub global run devtools

# Performance overlay চালু করুন
MaterialApp(
  showPerformanceOverlay: true,  // ফ্রেম রেট দেখুন
)
```

---

## অ্যাপ প্রকাশ

### Android Build
```bash
# Release APK
flutter build apk --release

# App Bundle (Play Store এর জন্য)
flutter build appbundle --release

# নির্দিষ্ট আর্কিটেকচারের জন্য
flutter build apk --split-per-abi
```

### Android Signing
```bash
# Keystore তৈরি করুন
keytool -genkey -v -keystore ~/upload-keystore.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias upload

# android/key.properties ফাইল তৈরি করুন
storePassword=<পাসওয়ার্ড>
keyPassword=<পাসওয়ার্ড>
keyAlias=upload
storeFile=<keystore-এর পথ>
```

### iOS Build
```bash
# iOS Release Build
flutter build ios --release

# IPA তৈরি
flutter build ipa
```

### অ্যাপ আইকন
```yaml
dev_dependencies:
  flutter_launcher_icons: ^0.13.0

flutter_launcher_icons:
  android: true
  ios: true
  image_path: "assets/icon/icon.png"
  min_sdk_android: 21
```

```bash
dart run flutter_launcher_icons
```

### Splash Screen
```yaml
dev_dependencies:
  flutter_native_splash: ^2.3.0

flutter_native_splash:
  color: "#FFFFFF"
  image: assets/splash.png
  android: true
  ios: true
```

```bash
dart run flutter_native_splash:create
```

---

## সম্পূর্ণ প্রজেক্ট উদাহরণ

### ই-কমার্স অ্যাপ (সংক্ষিপ্ত কাঠামো)

```dart
// lib/main.dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => ProductProvider()),
        ChangeNotifierProvider(create: (_) => CartProvider()),
        ChangeNotifierProvider(create: (_) => AuthProvider()),
      ],
      child: const EcommerceApp(),
    ),
  );
}

class EcommerceApp extends StatelessWidget {
  const EcommerceApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'বাংলা শপ',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.green),
      ),
      routes: {
        '/': (ctx) => const HomeScreen(),
        '/cart': (ctx) => const CartScreen(),
        '/profile': (ctx) => const ProfileScreen(),
      },
    );
  }
}

// lib/models/product.dart
class Product {
  final String id;
  final String name;
  final double price;
  final String imageUrl;
  final String category;
  final double rating;
  final int reviews;

  const Product({
    required this.id,
    required this.name,
    required this.price,
    required this.imageUrl,
    required this.category,
    required this.rating,
    required this.reviews,
  });

  factory Product.fromJson(Map<String, dynamic> json) {
    return Product(
      id: json['id'],
      name: json['name'],
      price: (json['price'] as num).toDouble(),
      imageUrl: json['imageUrl'],
      category: json['category'],
      rating: (json['rating'] as num).toDouble(),
      reviews: json['reviews'],
    );
  }
}

// lib/providers/product_provider.dart
class ProductProvider extends ChangeNotifier {
  List<Product> _products = [];
  List<Product> _filtered = [];
  String _selectedCategory = 'সব';
  bool _isLoading = false;
  String? _error;

  List<Product> get products => _filtered;
  bool get isLoading => _isLoading;
  String? get error => _error;

  Future<void> loadProducts() async {
    _isLoading = true;
    notifyListeners();

    try {
      await Future.delayed(const Duration(seconds: 1)); // সিমুলেশন
      _products = [
        const Product(id: '1', name: 'আম', price: 120, imageUrl: 'https://example.com/mango.jpg', category: 'ফল', rating: 4.5, reviews: 128),
        const Product(id: '2', name: 'কাঁঠাল', price: 250, imageUrl: 'https://example.com/jackfruit.jpg', category: 'ফল', rating: 4.2, reviews: 87),
      ];
      _filtered = _products;
      _error = null;
    } catch (e) {
      _error = e.toString();
    } finally {
      _isLoading = false;
      notifyListeners();
    }
  }

  void filterByCategory(String category) {
    _selectedCategory = category;
    if (category == 'সব') {
      _filtered = _products;
    } else {
      _filtered = _products.where((p) => p.category == category).toList();
    }
    notifyListeners();
  }

  void search(String query) {
    if (query.isEmpty) {
      _filtered = _products;
    } else {
      _filtered = _products
          .where((p) => p.name.toLowerCase().contains(query.toLowerCase()))
          .toList();
    }
    notifyListeners();
  }
}

// lib/screens/home_screen.dart
class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  @override
  void initState() {
    super.initState();
    Future.microtask(() => context.read<ProductProvider>().loadProducts());
  }

  @override
  Widget build(BuildContext context) {
    final productProvider = context.watch<ProductProvider>();
    final cart = context.watch<CartProvider>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('বাংলা শপ 🛒'),
        actions: [
          Stack(
            children: [
              IconButton(
                icon: const Icon(Icons.shopping_cart),
                onPressed: () => Navigator.pushNamed(context, '/cart'),
              ),
              if (cart.itemCount > 0)
                Positioned(
                  right: 8,
                  top: 8,
                  child: Container(
                    padding: const EdgeInsets.all(2),
                    decoration: const BoxDecoration(color: Colors.red, shape: BoxShape.circle),
                    child: Text('${cart.itemCount}', style: const TextStyle(color: Colors.white, fontSize: 10)),
                  ),
                ),
            ],
          ),
        ],
      ),
      body: Column(
        children: [
          // সার্চ বার
          Padding(
            padding: const EdgeInsets.all(8),
            child: TextField(
              decoration: InputDecoration(
                hintText: 'পণ্য খুঁজুন...',
                prefixIcon: const Icon(Icons.search),
                border: OutlineInputBorder(borderRadius: BorderRadius.circular(12)),
                filled: true,
              ),
              onChanged: productProvider.search,
            ),
          ),
          // পণ্য তালিকা
          Expanded(
            child: productProvider.isLoading
                ? const Center(child: CircularProgressIndicator())
                : productProvider.error != null
                    ? Center(child: Text('ত্রুটি: ${productProvider.error}'))
                    : GridView.builder(
                        padding: const EdgeInsets.all(8),
                        gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                          crossAxisCount: 2,
                          crossAxisSpacing: 8,
                          mainAxisSpacing: 8,
                          childAspectRatio: 0.75,
                        ),
                        itemCount: productProvider.products.length,
                        itemBuilder: (context, index) {
                          final product = productProvider.products[index];
                          return _ProductCard(product: product);
                        },
                      ),
          ),
        ],
      ),
    );
  }
}

class _ProductCard extends StatelessWidget {
  final Product product;
  const _ProductCard({required this.product});

  @override
  Widget build(BuildContext context) {
    return Card(
      clipBehavior: Clip.antiAlias,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Expanded(
            child: Image.network(
              product.imageUrl,
              width: double.infinity,
              fit: BoxFit.cover,
              errorBuilder: (_, __, ___) => Container(
                color: Colors.grey.shade200,
                child: const Icon(Icons.image, size: 50, color: Colors.grey),
              ),
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(8),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(product.name, style: const TextStyle(fontWeight: FontWeight.bold)),
                Row(
                  children: [
                    const Icon(Icons.star, size: 14, color: Colors.amber),
                    Text('${product.rating}', style: const TextStyle(fontSize: 12)),
                    Text(' (${product.reviews})', style: TextStyle(fontSize: 12, color: Colors.grey.shade600)),
                  ],
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  children: [
                    Text('৳${product.price.toStringAsFixed(0)}', style: const TextStyle(color: Colors.green, fontWeight: FontWeight.bold)),
                    IconButton(
                      icon: const Icon(Icons.add_shopping_cart, size: 20),
                      onPressed: () {
                        context.read<CartProvider>().addItem(product);
                        ScaffoldMessenger.of(context).showSnackBar(
                          SnackBar(
                            content: Text('${product.name} কার্টে যোগ হয়েছে'),
                            duration: const Duration(seconds: 1),
                          ),
                        );
                      },
                      padding: EdgeInsets.zero,
                      constraints: const BoxConstraints(),
                    ),
                  ],
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

---

## দরকারী প্যাকেজসমূহ

### নেটওয়ার্কিং
- `http` – সহজ HTTP ক্লায়েন্ট
- `dio` – উন্নত HTTP ক্লায়েন্ট (ইন্টারসেপ্টর, ক্যান্সেলেশন)
- `retrofit` – টাইপ-নিরাপদ HTTP ক্লায়েন্ট

### স্টেট ম্যানেজমেন্ট
- `provider` – সহজ, অফিসিয়াল
- `flutter_riverpod` – উন্নত, টাইপ-নিরাপদ
- `flutter_bloc` – এন্টারপ্রাইজ গ্রেড

### স্থানীয় স্টোরেজ
- `shared_preferences` – কী-মান স্টোরেজ
- `hive` – দ্রুত NoSQL
- `sqflite` – SQLite
- `isar` – আধুনিক, দ্রুত NoSQL

### Firebase
- `firebase_core`, `firebase_auth`, `cloud_firestore`
- `firebase_storage`, `firebase_messaging`

### UI
- `cached_network_image` – ছবি ক্যাশিং
- `flutter_svg` – SVG সাপোর্ট
- `lottie` – JSON অ্যানিমেশন
- `shimmer` – লোডিং প্লেসহোল্ডার
- `fl_chart` – চার্ট ও গ্রাফ

### ইউটিলিটি
- `intl` – তারিখ/সংখ্যা ফর্ম্যাটিং
- `url_launcher` – URL খোলা
- `image_picker` – ছবি বাছাই
- `permission_handler` – পারমিশন ম্যানেজমেন্ট
- `connectivity_plus` – ইন্টারনেট সংযোগ যাচাই
- `package_info_plus` – অ্যাপ তথ্য
- `device_info_plus` – ডিভাইস তথ্য

### নেভিগেশন
- `go_router` – ডিক্লারেটিভ রাউটিং
- `auto_route` – কোড জেনারেশন সহ রাউটিং

---

## পরবর্তী ধাপ

এই গাইড সম্পন্ন করার পর আপনি প্রস্তুত থাকবেন:

১. **বাস্তব প্রজেক্ট** তৈরি করতে – ই-কমার্স, সোশ্যাল মিডিয়া, ব্যাংকিং অ্যাপ
২. **ক্লিন আর্কিটেকচার** শিখতে – Repository Pattern, Use Cases, Entities
৩. **টেস্ট-ড্রিভেন ডেভেলপমেন্ট (TDD)** অনুসরণ করতে
৪. **CI/CD পাইপলাইন** সেটআপ করতে – GitHub Actions, Fastlane
৫. **App Store ও Play Store** তে প্রকাশ করতে
৬. **Flutter Web ও Desktop** ডেভেলপমেন্ট করতে

---

## রিসোর্সসমূহ

- **অফিসিয়াল Flutter ডকুমেন্টেশন:** https://docs.flutter.dev
- **Dart ডকুমেন্টেশন:** https://dart.dev
- **Flutter প্যাকেজ:** https://pub.dev
- **DartPad (অনলাইন এডিটর):** https://dartpad.dev
- **Flutter GitHub:** https://github.com/flutter/flutter
- **Flutter YouTube চ্যানেল:** https://youtube.com/@flutterdev
- **Flutter Community:** https://flutter.dev/community
- **Awesome Flutter:** https://github.com/Solido/awesome-flutter

---

> **মনে রাখুন:** Flutter শেখার সবচেয়ে ভালো উপায় হলো বাস্তব প্রজেক্ট তৈরি করা। ছোট ছোট অ্যাপ দিয়ে শুরু করুন, ধীরে ধীরে জটিলতা বাড়ান এবং সমস্যা সমাধান করতে শিখুন। Flutter-এর কমিউনিটি অত্যন্ত সহায়ক – যেকোনো সমস্যায় Stack Overflow এবং Flutter Discord ব্যবহার করুন।
