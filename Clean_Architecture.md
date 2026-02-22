# Flutter Clean Architecture with GetX — সম্পূর্ণ গাইড (বাংলা)

> **Clean Architecture** হলো Robert C. Martin (Uncle Bob) এর তৈরি একটি সফটওয়্যার ডিজাইন নীতি যেখানে কোডকে স্তরে স্তরে ভাগ করা হয়, যাতে প্রতিটি স্তর স্বাধীনভাবে কাজ করতে পারে, পরীক্ষা করা যায় এবং পরিবর্তন করা যায়। **GetX** হলো Flutter-এর সবচেয়ে জনপ্রিয় State Management, Navigation ও Dependency Injection সমাধান।

---

## বিষয়সূচি

1. [Clean Architecture কী এবং কেন?](#১-clean-architecture-কী-এবং-কেন)
2. [GetX কী এবং কেন?](#২-getx-কী-এবং-কেন)
3. [প্রজেক্ট স্তর বোঝা](#৩-প্রজেক্ট-স্তর-বোঝা)
4. [ফোল্ডার স্ট্রাকচার](#৪-ফোল্ডার-স্ট্রাকচার)
5. [pubspec.yaml সেটআপ](#৫-pubspecyaml-সেটআপ)
6. [Domain Layer — Entity](#৬-domain-layer--entity)
7. [Domain Layer — Repository (Abstract)](#৭-domain-layer--repository-abstract)
8. [Domain Layer — Use Case](#৮-domain-layer--use-case)
9. [Data Layer — Model](#৯-data-layer--model)
10. [Data Layer — Data Source](#১০-data-layer--data-source)
11. [Data Layer — Repository Implementation](#১১-data-layer--repository-implementation)
12. [Presentation Layer — GetX Controller](#১২-presentation-layer--getx-controller)
13. [Presentation Layer — Binding](#১৩-presentation-layer--binding)
14. [Presentation Layer — View (UI)](#১৪-presentation-layer--view-ui)
15. [GetX Routes সেটআপ](#১৫-getx-routes-সেটআপ)
16. [Dependency Injection (GetX)](#১৬-dependency-injection-getx)
17. [Error Handling](#১৭-error-handling)
18. [API Service Layer](#১৮-api-service-layer)
19. [Local Storage Service](#১৯-local-storage-service)
20. [Auth Flow সম্পূর্ণ উদাহরণ](#২০-auth-flow-সম্পূর্ণ-উদাহরণ)
21. [GetX State Management — Rx বিস্তারিত](#২১-getx-state-management--rx-বিস্তারিত)
22. [GetX Navigation বিস্তারিত](#২২-getx-navigation-বিস্তারিত)
23. [GetX Snackbar, Dialog, BottomSheet](#২৩-getx-snackbar-dialog-bottomsheet)
24. [Internationalization (i18n) with GetX](#২৪-internationalization-i18n-with-getx)
25. [Theme Management with GetX](#২৫-theme-management-with-getx)
26. [Unit Testing Clean Architecture](#২৬-unit-testing-clean-architecture)
27. [সম্পূর্ণ প্রজেক্ট — Todo App](#২৭-সম্পূর্ণ-প্রজেক্ট--todo-app)
28. [Best Practices ও সাধারণ ভুল](#২৮-best-practices-ও-সাধারণ-ভুল)

---

## ১. Clean Architecture কী এবং কেন?

### কী?
Clean Architecture হলো একটি কোড সাজানোর পদ্ধতি যেখানে অ্যাপকে তিনটি মূল স্তরে ভাগ করা হয়:

```
┌─────────────────────────────────────────────┐
│           Presentation Layer                │  ← UI, Controller (GetX)
│         (কী দেখাবো, ব্যবহারকারী কী করে)    │
├─────────────────────────────────────────────┤
│              Domain Layer                   │  ← Business Logic, Use Cases
│         (ব্যবসায়িক নিয়মকানুন)              │
├─────────────────────────────────────────────┤
│               Data Layer                    │  ← API, Database, Repository
│         (ডেটা কোথা থেকে আসে)              │
└─────────────────────────────────────────────┘
```

### কেন ব্যবহার করবেন?

**সমস্যা (Clean Architecture ছাড়া):**
```dart
// ❌ খারাপ — সব কিছু একসাথে
class HomeScreen extends StatefulWidget {
  @override
  Widget build(BuildContext context) {
    // UI-এর ভেতরে API কল — ভুল!
    final response = await http.get('https://api.example.com/users');
    final users = jsonDecode(response.body);
    // UI-এর ভেতরে ডেটাবেজ কল — ভুল!
    final db = await openDatabase('app.db');
    return ListView(...);
  }
}
```

**সমস্যাগুলো:**
- UI পরিবর্তন করলে API কোড ভাঙে
- API পরিবর্তন করলে UI ভাঙে
- টেস্ট করা কঠিন
- কোড পুনর্ব্যবহার করা যায় না
- দলে কাজ করা কঠিন

**সমাধান (Clean Architecture সহ):**
- প্রতিটি স্তর স্বাধীন — একটি পরিবর্তন করলে অন্যটি ভাঙে না
- টেস্ট করা সহজ — প্রতিটি ক্লাস আলাদাভাবে পরীক্ষা করা যায়
- কোড পুনর্ব্যবহারযোগ্য — একই Use Case অনেক জায়গায় ব্যবহার করা যায়
- স্কেলযোগ্য — বড় টিমে সহজে কাজ করা যায়
- রক্ষণাবেক্ষণ সহজ — বছরের পর বছর পরেও বোঝা যায়

### নির্ভরতার নিয়ম (Dependency Rule)
```
Presentation → Domain ← Data
```
**গুরুত্বপূর্ণ:** নির্ভরতা সবসময় ভেতরের দিকে যায়।
- Presentation জানে Domain সম্পর্কে, Data সম্পর্কে নয়
- Domain কাউকেই চেনে না (সবচেয়ে বিশুদ্ধ)
- Data জানে Domain সম্পর্কে, Presentation সম্পর্কে নয়

---

## ২. GetX কী এবং কেন?

### GetX কী?
GetX হলো Flutter-এর একটি শক্তিশালী প্যাকেজ যা তিনটি কাজ করে:

```
GetX
├── State Management  → Rx variables, GetxController
├── Navigation        → Get.to(), Get.back(), Get.offAll()
└── Dependency Injection → Get.put(), Get.find(), Binding
```

### কেন GetX?

| বৈশিষ্ট্য | GetX | Provider | BLoC |
|---------|------|----------|------|
| শেখা সহজ | ✅ | মধ্যম | কঠিন |
| কোডের পরিমাণ | কম | মধ্যম | বেশি |
| পারফরম্যান্স | উচ্চ | ভালো | ভালো |
| Navigation | built-in | আলাদা | আলাদা |
| DI | built-in | আলাদা | আলাদা |
| Clean Architecture | ✅ | ✅ | ✅ |

### GetX মূল ধারণা
```dart
// ১. Controller — ব্যবসায়িক লজিক
class UserController extends GetxController {
  var users = <User>[].obs;  // obs = observable (পরিবর্তন পর্যবেক্ষণ)
}

// ২. View — UI দেখায়
class UserView extends GetView<UserController> {
  @override
  Widget build(BuildContext context) {
    return Obx(() => Text('${controller.users.length} জন ব্যবহারকারী'));
    // Obx — controller পরিবর্তন হলে স্বয়ংক্রিয় পুনর্নির্মাণ
  }
}

// ৩. Binding — নির্ভরতা ব্যবস্থাপনা
class UserBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut(() => UserController());
  }
}
```

---

## ৩. প্রজেক্ট স্তর বোঝা

প্রতিটি ফিচারের জন্য তিনটি স্তর থাকবে। ধরুন আমরা "User" ফিচার বানাচ্ছি:

```
Feature: User
├── domain/           ← ব্যবসায়িক নিয়ম (Framework-independent)
│   ├── entities/     ← বিশুদ্ধ Dart অবজেক্ট (User কী?)
│   ├── repositories/ ← abstract contract (কী কী করা যাবে?)
│   └── usecases/     ← একটি নির্দিষ্ট কাজ (GetUser, CreateUser)
│
├── data/             ← ডেটা সংগ্রহ ও সরবরাহ
│   ├── models/       ← JSON ↔ Object রূপান্তর
│   ├── datasources/  ← API/Database থেকে ডেটা নেওয়া
│   └── repositories/ ← domain repository-র বাস্তব রূপ
│
└── presentation/     ← UI দেখানো ও ব্যবহারকারীর সাথে কথা
    ├── controllers/  ← GetX controller (state management)
    ├── bindings/     ← dependency injection
    └── views/        ← Widget/Screen (শুধু দেখানো)
```

### ডেটার প্রবাহ (Data Flow)

```
ব্যবহারকারী ক্লিক করে
        ↓
    View (UI)
        ↓
  Controller (GetX)
        ↓
    Use Case (Domain)
        ↓
  Repository (Abstract)
        ↓
Repository Implementation (Data)
        ↓
  Data Source (API/DB)
        ↓
    ডেটা ফিরে আসে (same path উল্টো দিকে)
```

---

## ৪. ফোল্ডার স্ট্রাকচার

```
lib/
├── main.dart                          ← অ্যাপের প্রবেশ বিন্দু
│
├── app/                               ← অ্যাপ-স্তরের কনফিগারেশন
│   ├── app.dart                       ← GetMaterialApp সেটআপ
│   ├── routes/
│   │   ├── app_pages.dart             ← সব রাউট তালিকা
│   │   └── app_routes.dart            ← রাউট নামের constant
│   └── bindings/
│       └── initial_binding.dart       ← অ্যাপ শুরুর নির্ভরতা
│
├── core/                              ← সব ফিচারে ব্যবহৃত জিনিস
│   ├── constants/
│   │   ├── api_constants.dart         ← API URL, endpoints
│   │   ├── app_constants.dart         ← অ্যাপের constant মান
│   │   └── string_constants.dart      ← টেক্সট/ইরর মেসেজ
│   ├── errors/
│   │   ├── failures.dart              ← Failure ক্লাস (domain-এর ত্রুটি)
│   │   └── exceptions.dart            ← Exception ক্লাস (data-এর ত্রুটি)
│   ├── network/
│   │   ├── api_client.dart            ← Dio/http সেটআপ
│   │   └── network_info.dart          ← ইন্টারনেট সংযোগ যাচাই
│   ├── storage/
│   │   └── local_storage.dart         ← SharedPreferences র‍্যাপার
│   ├── theme/
│   │   ├── app_theme.dart             ← Light/Dark থিম
│   │   └── app_colors.dart            ← রঙের palette
│   ├── utils/
│   │   ├── validators.dart            ← ফর্ম ভ্যালিডেশন
│   │   └── date_utils.dart            ← তারিখ ফরম্যাট
│   └── widgets/                       ← পুনর্ব্যবহারযোগ্য উইজেট
│       ├── custom_button.dart
│       ├── custom_text_field.dart
│       └── loading_widget.dart
│
└── features/                          ← প্রতিটি ফিচার আলাদা ফোল্ডারে
    ├── auth/                          ← লগইন/নিবন্ধন ফিচার
    │   ├── domain/
    │   │   ├── entities/
    │   │   │   └── user_entity.dart
    │   │   ├── repositories/
    │   │   │   └── auth_repository.dart       (abstract)
    │   │   └── usecases/
    │   │       ├── login_usecase.dart
    │   │       ├── register_usecase.dart
    │   │       └── logout_usecase.dart
    │   ├── data/
    │   │   ├── models/
    │   │   │   └── user_model.dart
    │   │   ├── datasources/
    │   │   │   ├── auth_remote_datasource.dart
    │   │   │   └── auth_local_datasource.dart
    │   │   └── repositories/
    │   │       └── auth_repository_impl.dart
    │   └── presentation/
    │       ├── controllers/
    │       │   └── auth_controller.dart
    │       ├── bindings/
    │       │   └── auth_binding.dart
    │       └── views/
    │           ├── login_view.dart
    │           └── register_view.dart
    │
    └── products/                      ← পণ্য ফিচার
        ├── domain/
        │   ├── entities/
        │   │   └── product_entity.dart
        │   ├── repositories/
        │   │   └── product_repository.dart
        │   └── usecases/
        │       ├── get_products_usecase.dart
        │       ├── get_product_by_id_usecase.dart
        │       └── create_product_usecase.dart
        ├── data/
        │   ├── models/
        │   │   └── product_model.dart
        │   ├── datasources/
        │   │   └── product_remote_datasource.dart
        │   └── repositories/
        │       └── product_repository_impl.dart
        └── presentation/
            ├── controllers/
            │   └── product_controller.dart
            ├── bindings/
            │   └── product_binding.dart
            └── views/
                ├── product_list_view.dart
                └── product_detail_view.dart
```

---

## ৫. pubspec.yaml সেটআপ

```yaml
name: clean_arch_getx
description: Flutter Clean Architecture with GetX
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter

  # ─── GetX (State, Navigation, DI) ───
  get: ^4.6.6

  # ─── Networking ───
  dio: ^5.4.0              # HTTP ক্লায়েন্ট
  connectivity_plus: ^5.0.2 # ইন্টারনেট চেক

  # ─── Local Storage ───
  shared_preferences: ^2.2.2  # সহজ key-value
  hive: ^2.2.3                # দ্রুত NoSQL
  hive_flutter: ^1.1.0

  # ─── Dependency Injection ───
  get_it: ^7.6.7              # (ঐচ্ছিক — GetX-এর নিজস্ব DI আছে)

  # ─── Functional Programming (Either, Option) ───
  dartz: ^0.10.1              # Left = Failure, Right = Success

  # ─── Utilities ───
  equatable: ^2.0.5           # == operator সহজ করে
  intl: ^0.19.0               # তারিখ ও সংখ্যা ফরম্যাট
  flutter_secure_storage: ^9.0.0  # নিরাপদ টোকেন সংরক্ষণ

  # ─── UI ───
  cached_network_image: ^3.3.1
  shimmer: ^3.0.0
  lottie: ^3.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  mockito: ^5.4.4           # Mock object তৈরি
  build_runner: ^2.4.8      # কোড জেনারেশন
  hive_generator: ^2.0.1

flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/animations/
    - assets/icons/
```

---

## ৬. Domain Layer — Entity

**Entity কী?** বিশুদ্ধ Dart অবজেক্ট। কোনো Flutter package নেই, কোনো JSON নেই। শুধু ব্যবসায়িক ডেটার সংজ্ঞা।

**কখন?** ব্যবসায়িক নিয়ম বোঝাতে। API response কেমন তা নয়, ব্যবসায়িক দৃষ্টিকোণে User মানে কী তা বোঝাতে।

**কেন?** Entity পরিবর্তন হয় শুধু ব্যবসায়িক নিয়ম পরিবর্তে। API বদলালেও Entity বদলায় না।

```dart
// lib/features/auth/domain/entities/user_entity.dart

import 'package:equatable/equatable.dart';

// Equatable ব্যবহার করি যাতে == দিয়ে তুলনা করা যায়
// এটি testing-এ অনেক কাজে লাগে
class UserEntity extends Equatable {
  // ─── Field ───
  // final মানে একবার সেট করলে আর পরিবর্তন হবে না
  // Entity immutable (অপরিবর্তনীয়) হওয়া উচিত
  final String id;
  final String name;
  final String email;
  final String? phone;        // ? মানে nullable — ফোন নাও থাকতে পারে
  final String? profileImage;
  final UserRole role;         // enum ব্যবহার করি — magic string এড়াই
  final DateTime createdAt;
  final bool isVerified;

  // ─── Constructor ───
  const UserEntity({
    required this.id,
    required this.name,
    required this.email,
    this.phone,
    this.profileImage,
    required this.role,
    required this.createdAt,
    required this.isVerified,
  });

  // ─── Business Logic ───
  // Entity-র ভেতরে ব্যবসায়িক নিয়ম রাখতে পারি
  bool get isAdmin => role == UserRole.admin;
  bool get hasPhone => phone != null && phone!.isNotEmpty;
  String get displayName => name.trim().isEmpty ? email : name;

  // copyWith — নতুন মান দিয়ে নতুন Entity তৈরি
  // (Immutability বজায় রাখতে)
  UserEntity copyWith({
    String? id,
    String? name,
    String? email,
    String? phone,
    String? profileImage,
    UserRole? role,
    DateTime? createdAt,
    bool? isVerified,
  }) {
    return UserEntity(
      id: id ?? this.id,
      name: name ?? this.name,
      email: email ?? this.email,
      phone: phone ?? this.phone,
      profileImage: profileImage ?? this.profileImage,
      role: role ?? this.role,
      createdAt: createdAt ?? this.createdAt,
      isVerified: isVerified ?? this.isVerified,
    );
  }

  // Equatable-এর জন্য — কোন field দিয়ে তুলনা হবে
  @override
  List<Object?> get props => [id, name, email, phone, role, isVerified];

  @override
  String toString() => 'UserEntity(id: $id, name: $name, email: $email)';
}

// ব্যবহারকারীর ভূমিকা — enum ব্যবহার করা ভালো অভ্যাস
enum UserRole { user, admin, moderator }
```

```dart
// lib/features/products/domain/entities/product_entity.dart

import 'package:equatable/equatable.dart';

class ProductEntity extends Equatable {
  final String id;
  final String name;
  final String description;
  final double price;
  final int stock;
  final String category;
  final List<String> images;    // একাধিক ছবি
  final double rating;
  final int reviewCount;
  final bool isActive;

  const ProductEntity({
    required this.id,
    required this.name,
    required this.description,
    required this.price,
    required this.stock,
    required this.category,
    required this.images,
    required this.rating,
    required this.reviewCount,
    required this.isActive,
  });

  // ব্যবসায়িক নিয়ম Entity-তে থাকে
  bool get isInStock => stock > 0;
  bool get isLowStock => stock > 0 && stock <= 5;
  bool get hasThumbnail => images.isNotEmpty;
  String get thumbnail => images.isNotEmpty ? images.first : '';
  String get formattedPrice => '৳${price.toStringAsFixed(2)}';

  ProductEntity copyWith({
    String? id,
    String? name,
    String? description,
    double? price,
    int? stock,
    String? category,
    List<String>? images,
    double? rating,
    int? reviewCount,
    bool? isActive,
  }) {
    return ProductEntity(
      id: id ?? this.id,
      name: name ?? this.name,
      description: description ?? this.description,
      price: price ?? this.price,
      stock: stock ?? this.stock,
      category: category ?? this.category,
      images: images ?? this.images,
      rating: rating ?? this.rating,
      reviewCount: reviewCount ?? this.reviewCount,
      isActive: isActive ?? this.isActive,
    );
  }

  @override
  List<Object?> get props => [id, name, price, stock, isActive];
}
```

---

## ৭. Domain Layer — Repository (Abstract)

**Repository কী?** একটি চুক্তিপত্র (contract)। এটি ঘোষণা করে কী কী অপারেশন করা যাবে, কিন্তু কীভাবে করা যাবে তা বলে না।

**কখন?** Domain layer-এ abstract class হিসেবে। বাস্তব implementation Data layer-এ।

**কেন?** Domain layer জানে না ডেটা কোথা থেকে আসে — API থেকে, নাকি ডেটাবেজ থেকে। এই বিচ্ছেদই Clean Architecture-এর মূল শক্তি।

```dart
// lib/features/auth/domain/repositories/auth_repository.dart

import 'package:dartz/dartz.dart';
import '../../../../core/errors/failures.dart';
import '../entities/user_entity.dart';

// abstract — এটি সরাসরি ব্যবহার করা যাবে না
// Data layer-এ implement করতে হবে
abstract class AuthRepository {

  // Either<Failure, Success> — dartz প্যাকেজ থেকে
  // Left = ব্যর্থতা (Failure)
  // Right = সাফল্য (UserEntity)
  // এটি Exception throw না করে ত্রুটি handle করে — functional approach

  Future<Either<Failure, UserEntity>> login({
    required String email,
    required String password,
  });

  Future<Either<Failure, UserEntity>> register({
    required String name,
    required String email,
    required String password,
  });

  Future<Either<Failure, void>> logout();

  Future<Either<Failure, UserEntity?>> getCurrentUser();

  Future<Either<Failure, UserEntity>> updateProfile({
    required String name,
    String? phone,
    String? profileImage,
  });

  Future<Either<Failure, void>> changePassword({
    required String currentPassword,
    required String newPassword,
  });

  Future<Either<Failure, void>> forgotPassword({
    required String email,
  });

  // Token সংরক্ষিত আছে কিনা — অনেক সময় sync method যথেষ্ট
  bool get isLoggedIn;
}
```

```dart
// lib/features/products/domain/repositories/product_repository.dart

import 'package:dartz/dartz.dart';
import '../../../../core/errors/failures.dart';
import '../entities/product_entity.dart';

abstract class ProductRepository {
  Future<Either<Failure, List<ProductEntity>>> getProducts({
    int page = 1,
    int limit = 20,
    String? category,
    String? search,
    String? sortBy,
  });

  Future<Either<Failure, ProductEntity>> getProductById(String id);

  Future<Either<Failure, ProductEntity>> createProduct(ProductEntity product);

  Future<Either<Failure, ProductEntity>> updateProduct(ProductEntity product);

  Future<Either<Failure, void>> deleteProduct(String id);

  Future<Either<Failure, List<String>>> getCategories();
}
```

---

## ৮. Domain Layer — Use Case

**Use Case কী?** একটি ক্লাস = একটি কাজ। "LoginUseCase" শুধু লগইনের কাজ করে। আর কিছু না।

**কখন?** প্রতিটি ব্যবসায়িক অপারেশনের জন্য আলাদা Use Case।

**কেন?** 
- Single Responsibility — একটি কারণে পরিবর্তন হয়
- পুনর্ব্যবহারযোগ্য — Controller ও Test দুটোই ব্যবহার করতে পারে
- পরীক্ষাযোগ্য — সহজে Mock করা যায়

```dart
// lib/core/usecases/usecase.dart

import 'package:dartz/dartz.dart';
import '../errors/failures.dart';

// Base UseCase — সব Use Case এটি extend করবে
// Type = return type (যেমন UserEntity)
// Params = parameter type (যেমন LoginParams)
abstract class UseCase<Type, Params> {
  // call() মেথড — এটি থাকলে UseCase-কে function-এর মতো ডাকা যায়
  // loginUseCase(params) — সরাসরি ডাকা যাবে
  Future<Either<Failure, Type>> call(Params params);
}

// Parameter-বিহীন Use Case-এর জন্য
class NoParams {
  const NoParams();
}
```

```dart
// lib/features/auth/domain/usecases/login_usecase.dart

import 'package:dartz/dartz.dart';
import 'package:equatable/equatable.dart';
import '../../../../core/errors/failures.dart';
import '../../../../core/usecases/usecase.dart';
import '../entities/user_entity.dart';
import '../repositories/auth_repository.dart';

// LoginUseCase — শুধু লগইনের কাজ
class LoginUseCase implements UseCase<UserEntity, LoginParams> {
  // Repository inject হয় — সরাসরি তৈরি করে না (DI নীতি)
  final AuthRepository repository;

  const LoginUseCase(this.repository);

  // call() — UseCase-কে function-এর মতো ডাকা যাবে
  @override
  Future<Either<Failure, UserEntity>> call(LoginParams params) async {
    // শুধু repository ডাকে, ব্যবসায়িক validation করতে পারে
    return await repository.login(
      email: params.email,
      password: params.password,
    );
  }
}

// LoginParams — Use Case-এর input
// Equatable দিয়ে test-এ তুলনা সহজ হয়
class LoginParams extends Equatable {
  final String email;
  final String password;

  const LoginParams({required this.email, required this.password});

  @override
  List<Object> get props => [email, password];
}
```

```dart
// lib/features/auth/domain/usecases/register_usecase.dart

import 'package:dartz/dartz.dart';
import 'package:equatable/equatable.dart';
import '../../../../core/errors/failures.dart';
import '../../../../core/usecases/usecase.dart';
import '../entities/user_entity.dart';
import '../repositories/auth_repository.dart';

class RegisterUseCase implements UseCase<UserEntity, RegisterParams> {
  final AuthRepository repository;

  const RegisterUseCase(this.repository);

  @override
  Future<Either<Failure, UserEntity>> call(RegisterParams params) async {
    // ব্যবসায়িক validation — পাসওয়ার্ড মিলছে কিনা
    if (params.password != params.confirmPassword) {
      return Left(ValidationFailure('পাসওয়ার্ড দুটি মিলছে না'));
    }

    return await repository.register(
      name: params.name,
      email: params.email,
      password: params.password,
    );
  }
}

class RegisterParams extends Equatable {
  final String name;
  final String email;
  final String password;
  final String confirmPassword;

  const RegisterParams({
    required this.name,
    required this.email,
    required this.password,
    required this.confirmPassword,
  });

  @override
  List<Object> get props => [name, email, password, confirmPassword];
}
```

```dart
// lib/features/auth/domain/usecases/logout_usecase.dart

import 'package:dartz/dartz.dart';
import '../../../../core/errors/failures.dart';
import '../../../../core/usecases/usecase.dart';
import '../repositories/auth_repository.dart';

// Parameter ছাড়া Use Case — NoParams ব্যবহার করি
class LogoutUseCase implements UseCase<void, NoParams> {
  final AuthRepository repository;

  const LogoutUseCase(this.repository);

  @override
  Future<Either<Failure, void>> call(NoParams params) async {
    return await repository.logout();
  }
}
```

```dart
// lib/features/products/domain/usecases/get_products_usecase.dart

import 'package:dartz/dartz.dart';
import 'package:equatable/equatable.dart';
import '../../../../core/errors/failures.dart';
import '../../../../core/usecases/usecase.dart';
import '../entities/product_entity.dart';
import '../repositories/product_repository.dart';

class GetProductsUseCase implements UseCase<List<ProductEntity>, GetProductsParams> {
  final ProductRepository repository;

  const GetProductsUseCase(this.repository);

  @override
  Future<Either<Failure, List<ProductEntity>>> call(GetProductsParams params) {
    return repository.getProducts(
      page: params.page,
      limit: params.limit,
      category: params.category,
      search: params.search,
    );
  }
}

class GetProductsParams extends Equatable {
  final int page;
  final int limit;
  final String? category;
  final String? search;

  const GetProductsParams({
    this.page = 1,
    this.limit = 20,
    this.category,
    this.search,
  });

  @override
  List<Object?> get props => [page, limit, category, search];
}
```

---

## ৯. Data Layer — Model

**Model কী?** Entity-র মতোই, কিন্তু JSON থেকে তৈরি ও JSON-এ রূপান্তর করতে পারে।

**কখন?** Data layer-এ। API বা ডেটাবেজ থেকে আসা ডেটা রূপান্তরের জন্য।

**কেন?** Entity-কে JSON parsing জানতে হবে না। Model সেই কাজ করে এবং Entity-তে রূপান্তরিত হয়।

```dart
// lib/features/auth/data/models/user_model.dart

import '../../domain/entities/user_entity.dart';

// UserModel — UserEntity extend করে
// Entity-র সব ব্যবসায়িক নিয়ম পায়, তার উপরে JSON parsing যোগ হয়
class UserModel extends UserEntity {
  const UserModel({
    required super.id,
    required super.name,
    required super.email,
    super.phone,
    super.profileImage,
    required super.role,
    required super.createdAt,
    required super.isVerified,
  });

  // ─── JSON থেকে তৈরি ───
  // factory — নতুন instance তৈরি করে
  factory UserModel.fromJson(Map<String, dynamic> json) {
    return UserModel(
      // ?? — null হলে default মান
      id: json['id']?.toString() ?? '',
      name: json['name'] ?? '',
      email: json['email'] ?? '',
      phone: json['phone'],
      profileImage: json['profile_image'] ?? json['avatar'],

      // JSON-এ string আসতে পারে, enum-এ রূপান্তর
      role: _parseRole(json['role']),

      // ISO 8601 string থেকে DateTime
      createdAt: json['created_at'] != null
          ? DateTime.parse(json['created_at'])
          : DateTime.now(),

      isVerified: json['is_verified'] ?? json['email_verified'] ?? false,
    );
  }

  // ─── JSON-এ রূপান্তর ───
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
      'phone': phone,
      'profile_image': profileImage,
      'role': role.name,
      'created_at': createdAt.toIso8601String(),
      'is_verified': isVerified,
    };
  }

  // ─── Entity থেকে Model তৈরি (উল্টো দিকে) ───
  factory UserModel.fromEntity(UserEntity entity) {
    return UserModel(
      id: entity.id,
      name: entity.name,
      email: entity.email,
      phone: entity.phone,
      profileImage: entity.profileImage,
      role: entity.role,
      createdAt: entity.createdAt,
      isVerified: entity.isVerified,
    );
  }

  // Private helper — role string থেকে enum
  static UserRole _parseRole(dynamic role) {
    switch (role?.toString().toLowerCase()) {
      case 'admin':
        return UserRole.admin;
      case 'moderator':
        return UserRole.moderator;
      default:
        return UserRole.user;
    }
  }

  @override
  String toString() => 'UserModel(id: $id, name: $name)';
}
```

```dart
// lib/features/products/data/models/product_model.dart

import '../../domain/entities/product_entity.dart';

class ProductModel extends ProductEntity {
  const ProductModel({
    required super.id,
    required super.name,
    required super.description,
    required super.price,
    required super.stock,
    required super.category,
    required super.images,
    required super.rating,
    required super.reviewCount,
    required super.isActive,
  });

  factory ProductModel.fromJson(Map<String, dynamic> json) {
    // images field বিভিন্ন API-তে বিভিন্ন ভাবে আসতে পারে
    List<String> parseImages() {
      final raw = json['images'];
      if (raw == null) return [];
      if (raw is List) return raw.map((e) => e.toString()).toList();
      if (raw is String) return [raw];
      return [];
    }

    return ProductModel(
      id: json['id']?.toString() ?? '',
      name: json['name'] ?? '',
      description: json['description'] ?? '',
      // num → double রূপান্তর নিরাপদভাবে
      price: (json['price'] as num?)?.toDouble() ?? 0.0,
      stock: (json['stock'] as num?)?.toInt() ?? 0,
      category: json['category'] ?? '',
      images: parseImages(),
      rating: (json['rating'] as num?)?.toDouble() ?? 0.0,
      reviewCount: (json['review_count'] ?? json['reviews_count'] ?? 0) as int,
      isActive: json['is_active'] ?? json['active'] ?? true,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'description': description,
      'price': price,
      'stock': stock,
      'category': category,
      'images': images,
      'rating': rating,
      'review_count': reviewCount,
      'is_active': isActive,
    };
  }

  factory ProductModel.fromEntity(ProductEntity entity) {
    return ProductModel(
      id: entity.id,
      name: entity.name,
      description: entity.description,
      price: entity.price,
      stock: entity.stock,
      category: entity.category,
      images: entity.images,
      rating: entity.rating,
      reviewCount: entity.reviewCount,
      isActive: entity.isActive,
    );
  }
}
```

---

## ১০. Data Layer — Data Source

**Data Source কী?** সরাসরি API বা ডেটাবেজের সাথে কথা বলে। শুধু raw data নেয় ও দেয়।

**কখন?** Remote (API) ও Local (Database/Cache) — দুটো আলাদা Data Source।

**কেন?** Repository সিদ্ধান্ত নেবে কোন Source থেকে ডেটা নেবে। Data Source সেই সিদ্ধান্ত জানে না।

```dart
// lib/features/auth/data/datasources/auth_remote_datasource.dart

import '../../../../core/constants/api_constants.dart';
import '../../../../core/errors/exceptions.dart';
import '../../../../core/network/api_client.dart';
import '../models/user_model.dart';

// abstract — ভবিষ্যতে mock করা সহজ হয়
abstract class AuthRemoteDataSource {
  Future<UserModel> login({required String email, required String password});
  Future<UserModel> register({required String name, required String email, required String password});
  Future<void> logout();
  Future<UserModel> getProfile();
  Future<UserModel> updateProfile({required String name, String? phone, String? profileImage});
}

// বাস্তব implementation
class AuthRemoteDataSourceImpl implements AuthRemoteDataSource {
  // ApiClient inject হয় — সরাসরি Dio তৈরি করে না
  final ApiClient apiClient;

  AuthRemoteDataSourceImpl({required this.apiClient});

  @override
  Future<UserModel> login({
    required String email,
    required String password,
  }) async {
    try {
      final response = await apiClient.post(
        ApiConstants.loginEndpoint,
        data: {'email': email, 'password': password},
      );

      // API response থেকে token সংরক্ষণ (ApiClient করে)
      // Model তৈরি করে return করি
      return UserModel.fromJson(response.data['user'] ?? response.data);
    } on ServerException {
      rethrow;  // আবার ছুড়ে দেই — Repository handle করবে
    } catch (e) {
      throw ServerException(message: 'লগইন ব্যর্থ হয়েছে: $e');
    }
  }

  @override
  Future<UserModel> register({
    required String name,
    required String email,
    required String password,
  }) async {
    try {
      final response = await apiClient.post(
        ApiConstants.registerEndpoint,
        data: {'name': name, 'email': email, 'password': password},
      );
      return UserModel.fromJson(response.data['user'] ?? response.data);
    } catch (e) {
      throw ServerException(message: 'নিবন্ধন ব্যর্থ হয়েছে: $e');
    }
  }

  @override
  Future<void> logout() async {
    try {
      await apiClient.post(ApiConstants.logoutEndpoint);
    } catch (e) {
      // লগআউটে error হলেও চলতে দেই
      throw ServerException(message: 'লগআউট ব্যর্থ হয়েছে');
    }
  }

  @override
  Future<UserModel> getProfile() async {
    try {
      final response = await apiClient.get(ApiConstants.profileEndpoint);
      return UserModel.fromJson(response.data);
    } catch (e) {
      throw ServerException(message: 'প্রোফাইল লোড ব্যর্থ হয়েছে');
    }
  }

  @override
  Future<UserModel> updateProfile({
    required String name,
    String? phone,
    String? profileImage,
  }) async {
    final data = <String, dynamic>{'name': name};
    if (phone != null) data['phone'] = phone;
    if (profileImage != null) data['profile_image'] = profileImage;

    final response = await apiClient.put(
      ApiConstants.profileEndpoint,
      data: data,
    );
    return UserModel.fromJson(response.data);
  }
}
```

```dart
// lib/features/auth/data/datasources/auth_local_datasource.dart

import '../../../../core/storage/local_storage.dart';
import '../models/user_model.dart';
import 'dart:convert';

abstract class AuthLocalDataSource {
  Future<void> cacheUser(UserModel user);
  Future<UserModel?> getCachedUser();
  Future<void> clearUser();
  Future<void> saveToken(String token);
  Future<String?> getToken();
  Future<void> clearToken();
}

class AuthLocalDataSourceImpl implements AuthLocalDataSource {
  final LocalStorage localStorage;

  // Key constants — typo থেকে বাঁচায়
  static const String _userKey = 'cached_user';
  static const String _tokenKey = 'auth_token';

  AuthLocalDataSourceImpl({required this.localStorage});

  @override
  Future<void> cacheUser(UserModel user) async {
    // Object → JSON string → সংরক্ষণ
    await localStorage.setString(_userKey, jsonEncode(user.toJson()));
  }

  @override
  Future<UserModel?> getCachedUser() async {
    final jsonStr = await localStorage.getString(_userKey);
    if (jsonStr == null) return null;
    // JSON string → Map → Model
    return UserModel.fromJson(jsonDecode(jsonStr));
  }

  @override
  Future<void> clearUser() => localStorage.remove(_userKey);

  @override
  Future<void> saveToken(String token) => localStorage.setString(_tokenKey, token);

  @override
  Future<String?> getToken() => localStorage.getString(_tokenKey);

  @override
  Future<void> clearToken() => localStorage.remove(_tokenKey);
}
```

---

## ১১. Data Layer — Repository Implementation

**Repository Implementation কী?** Domain-এর abstract Repository-র বাস্তব রূপ। Data Source-দের একসাথে পরিচালনা করে।

**কখন?** Data layer-এ। ইন্টারনেট আছে কিনা দেখে — Remote বা Local Data Source ডাকে।

**কেন?** Exception → Failure রূপান্তর এখানে হয়। Domain layer exception জানে না, Failure জানে।

```dart
// lib/features/auth/data/repositories/auth_repository_impl.dart

import 'package:dartz/dartz.dart';
import '../../../../core/errors/exceptions.dart';
import '../../../../core/errors/failures.dart';
import '../../../../core/network/network_info.dart';
import '../../domain/entities/user_entity.dart';
import '../../domain/repositories/auth_repository.dart';
import '../datasources/auth_local_datasource.dart';
import '../datasources/auth_remote_datasource.dart';
import '../models/user_model.dart';

class AuthRepositoryImpl implements AuthRepository {
  final AuthRemoteDataSource remoteDataSource;
  final AuthLocalDataSource localDataSource;
  final NetworkInfo networkInfo;  // ইন্টারনেট আছে কিনা

  AuthRepositoryImpl({
    required this.remoteDataSource,
    required this.localDataSource,
    required this.networkInfo,
  });

  @override
  Future<Either<Failure, UserEntity>> login({
    required String email,
    required String password,
  }) async {
    // ইন্টারনেট আছে কিনা যাচাই
    if (!await networkInfo.isConnected) {
      return Left(NetworkFailure('ইন্টারনেট সংযোগ নেই'));
    }

    try {
      // Remote Data Source থেকে ডেটা নেই
      final userModel = await remoteDataSource.login(
        email: email,
        password: password,
      );

      // সফল হলে local-এ cache করি (offline support)
      await localDataSource.cacheUser(userModel);

      // Right = সাফল্য, Model → Entity (Domain বুঝবে)
      return Right(userModel);
    } on ServerException catch (e) {
      // Exception → Failure রূপান্তর
      return Left(ServerFailure(e.message));
    } on UnauthorizedException catch (e) {
      return Left(AuthFailure(e.message));
    }
  }

  @override
  Future<Either<Failure, UserEntity>> register({
    required String name,
    required String email,
    required String password,
  }) async {
    if (!await networkInfo.isConnected) {
      return Left(NetworkFailure('নিবন্ধনের জন্য ইন্টারনেট প্রয়োজন'));
    }

    try {
      final userModel = await remoteDataSource.register(
        name: name,
        email: email,
        password: password,
      );
      await localDataSource.cacheUser(userModel);
      return Right(userModel);
    } on ServerException catch (e) {
      return Left(ServerFailure(e.message));
    }
  }

  @override
  Future<Either<Failure, void>> logout() async {
    try {
      // ইন্টারনেট থাকলে সার্ভারে লগআউট করি
      if (await networkInfo.isConnected) {
        await remoteDataSource.logout();
      }
      // সবসময় local ডেটা মুছি
      await localDataSource.clearUser();
      await localDataSource.clearToken();
      return const Right(null);
    } on ServerException catch (e) {
      return Left(ServerFailure(e.message));
    }
  }

  @override
  Future<Either<Failure, UserEntity?>> getCurrentUser() async {
    // প্রথমে cached user দেখি
    try {
      final cachedUser = await localDataSource.getCachedUser();
      if (cachedUser != null) {
        // Background-এ fresh data আনি (কিন্তু wait করি না)
        _refreshUserInBackground();
        return Right(cachedUser);
      }

      // Cache নেই — remote থেকে আনি
      if (!await networkInfo.isConnected) {
        return const Right(null);  // কেউ নেই
      }

      final userModel = await remoteDataSource.getProfile();
      await localDataSource.cacheUser(userModel);
      return Right(userModel);
    } on ServerException catch (e) {
      return Left(ServerFailure(e.message));
    }
  }

  // Background refresh — UI ব্লক করে না
  void _refreshUserInBackground() async {
    try {
      if (await networkInfo.isConnected) {
        final fresh = await remoteDataSource.getProfile();
        await localDataSource.cacheUser(fresh);
      }
    } catch (_) {
      // Background error নীরবে উপেক্ষা করি
    }
  }

  @override
  Future<Either<Failure, UserEntity>> updateProfile({
    required String name,
    String? phone,
    String? profileImage,
  }) async {
    if (!await networkInfo.isConnected) {
      return Left(NetworkFailure('ইন্টারনেট সংযোগ নেই'));
    }

    try {
      final updated = await remoteDataSource.updateProfile(
        name: name,
        phone: phone,
        profileImage: profileImage,
      );
      await localDataSource.cacheUser(updated);
      return Right(updated);
    } on ServerException catch (e) {
      return Left(ServerFailure(e.message));
    }
  }

  @override
  Future<Either<Failure, void>> changePassword({
    required String currentPassword,
    required String newPassword,
  }) async {
    // implementation...
    return const Right(null);
  }

  @override
  Future<Either<Failure, void>> forgotPassword({required String email}) async {
    // implementation...
    return const Right(null);
  }

  @override
  bool get isLoggedIn {
    // Sync check — token আছে কিনা
    // এই implementation synchronous হওয়া উচিত
    return false; // LocalStorage থেকে sync check
  }
}
```

---

## ১২. Presentation Layer — GetX Controller

**Controller কী?** GetX-এর মূল ক্লাস। State রাখে, Use Case ডাকে, UI-কে জানায়।

**কখন?** প্রতিটি ফিচারের জন্য একটি (বা একাধিক) Controller।

**কেন?** UI (View) শুধু দেখায়। Controller সব logic পরিচালনা করে। এই বিচ্ছেদ UI টেস্টকে সহজ করে।

```dart
// lib/features/auth/presentation/controllers/auth_controller.dart

import 'package:get/get.dart';
import '../../../../app/routes/app_routes.dart';
import '../../../../core/errors/failures.dart';
import '../../domain/entities/user_entity.dart';
import '../../domain/usecases/login_usecase.dart';
import '../../domain/usecases/logout_usecase.dart';
import '../../domain/usecases/register_usecase.dart';
import '../../../../core/usecases/usecase.dart';

class AuthController extends GetxController {
  // ─── Use Cases (inject হয়) ───
  final LoginUseCase loginUseCase;
  final RegisterUseCase registerUseCase;
  final LogoutUseCase logoutUseCase;

  AuthController({
    required this.loginUseCase,
    required this.registerUseCase,
    required this.logoutUseCase,
  });

  // ─── Observable State ───
  // .obs লাগালে Obx() স্বয়ংক্রিয় পুনর্নির্মাণ করে
  final _currentUser = Rxn<UserEntity>();   // Rxn = nullable Rx
  final _isLoading = false.obs;
  final _errorMessage = ''.obs;

  // ─── Getters (বাইরে থেকে পড়া) ───
  UserEntity? get currentUser => _currentUser.value;
  bool get isLoading => _isLoading.value;
  String get errorMessage => _errorMessage.value;
  bool get isLoggedIn => _currentUser.value != null;

  // ─── Lifecycle ───
  @override
  void onInit() {
    super.onInit();
    // Controller তৈরি হওয়ার সময় — user আছে কিনা দেখি
    print('AuthController initialized');
  }

  @override
  void onReady() {
    super.onReady();
    // UI render হওয়ার পরে — API call করুন এখানে
  }

  @override
  void onClose() {
    // Controller মুছে যাওয়ার সময় — cleanup করুন
    print('AuthController disposed');
    super.onClose();
  }

  // ─── Actions ───
  Future<void> login({
    required String email,
    required String password,
  }) async {
    // Loading শুরু, error পরিষ্কার
    _isLoading.value = true;
    _errorMessage.value = '';

    // Use Case ডাকি
    final result = await loginUseCase(
      LoginParams(email: email, password: password),
    );

    // dartz Either fold — Left বা Right handle করি
    result.fold(
      // Left = Failure (ব্যর্থতা)
      (failure) {
        _errorMessage.value = _mapFailureToMessage(failure);
        // GetX দিয়ে Snackbar দেখাই
        Get.snackbar(
          'লগইন ব্যর্থ',
          _errorMessage.value,
          snackPosition: SnackPosition.BOTTOM,
        );
      },
      // Right = Success (সাফল্য)
      (user) {
        _currentUser.value = user;
        // সাফল্যের পরে HomeScreen-এ যাই
        // offAllNamed — back stack পরিষ্কার করে (লগইনে ফিরে যাওয়া যাবে না)
        Get.offAllNamed(AppRoutes.home);
      },
    );

    _isLoading.value = false;
  }

  Future<void> register({
    required String name,
    required String email,
    required String password,
    required String confirmPassword,
  }) async {
    _isLoading.value = true;
    _errorMessage.value = '';

    final result = await registerUseCase(
      RegisterParams(
        name: name,
        email: email,
        password: password,
        confirmPassword: confirmPassword,
      ),
    );

    result.fold(
      (failure) {
        _errorMessage.value = _mapFailureToMessage(failure);
        Get.snackbar('নিবন্ধন ব্যর্থ', _errorMessage.value,
            snackPosition: SnackPosition.BOTTOM);
      },
      (user) {
        _currentUser.value = user;
        Get.offAllNamed(AppRoutes.home);
      },
    );

    _isLoading.value = false;
  }

  Future<void> logout() async {
    _isLoading.value = true;

    final result = await logoutUseCase(const NoParams());

    result.fold(
      (failure) {
        // লগআউট error হলেও local থেকে clear করি
        _currentUser.value = null;
      },
      (_) {
        _currentUser.value = null;
      },
    );

    Get.offAllNamed(AppRoutes.login);
    _isLoading.value = false;
  }

  // Failure → বাংলা মেসেজ রূপান্তর
  String _mapFailureToMessage(Failure failure) {
    if (failure is NetworkFailure) return 'ইন্টারনেট সংযোগ নেই';
    if (failure is ServerFailure) return failure.message;
    if (failure is AuthFailure) return 'ইমেইল বা পাসওয়ার্ড ভুল';
    if (failure is ValidationFailure) return failure.message;
    return 'অপ্রত্যাশিত সমস্যা হয়েছে';
  }
}
```

```dart
// lib/features/products/presentation/controllers/product_controller.dart

import 'package:get/get.dart';
import '../../domain/entities/product_entity.dart';
import '../../domain/usecases/get_products_usecase.dart';
import '../../domain/usecases/get_product_by_id_usecase.dart';
import '../../../../core/errors/failures.dart';

class ProductController extends GetxController {
  final GetProductsUseCase getProductsUseCase;
  final GetProductByIdUseCase getProductByIdUseCase;

  ProductController({
    required this.getProductsUseCase,
    required this.getProductByIdUseCase,
  });

  // ─── State ───
  final _products = <ProductEntity>[].obs;
  final _selectedProduct = Rxn<ProductEntity>();
  final _isLoading = false.obs;
  final _isLoadingMore = false.obs;  // pagination
  final _errorMessage = ''.obs;
  final _searchQuery = ''.obs;
  final _selectedCategory = ''.obs;
  final _currentPage = 1.obs;
  final _hasMore = true.obs;

  // ─── Getters ───
  List<ProductEntity> get products => _products;
  ProductEntity? get selectedProduct => _selectedProduct.value;
  bool get isLoading => _isLoading.value;
  bool get isLoadingMore => _isLoadingMore.value;
  String get errorMessage => _errorMessage.value;
  bool get hasMore => _hasMore.value;

  // computed — filter করা তালিকা
  List<ProductEntity> get filteredProducts {
    var list = _products.toList();
    if (_searchQuery.value.isNotEmpty) {
      list = list.where((p) =>
        p.name.toLowerCase().contains(_searchQuery.value.toLowerCase())
      ).toList();
    }
    return list;
  }

  @override
  void onInit() {
    super.onInit();
    fetchProducts();  // শুরুতেই পণ্য লোড করি

    // Search debounce — টাইপ করার ৫০০ms পরে search করি
    debounce(
      _searchQuery,
      (_) => fetchProducts(reset: true),
      time: const Duration(milliseconds: 500),
    );
  }

  // ─── Actions ───
  Future<void> fetchProducts({bool reset = false}) async {
    if (reset) {
      _currentPage.value = 1;
      _hasMore.value = true;
      _products.clear();
    }

    if (!_hasMore.value) return;  // আর নেই

    if (_currentPage.value == 1) {
      _isLoading.value = true;
    } else {
      _isLoadingMore.value = true;
    }

    _errorMessage.value = '';

    final result = await getProductsUseCase(
      GetProductsParams(
        page: _currentPage.value,
        limit: 20,
        category: _selectedCategory.value.isEmpty ? null : _selectedCategory.value,
        search: _searchQuery.value.isEmpty ? null : _searchQuery.value,
      ),
    );

    result.fold(
      (failure) => _errorMessage.value = _mapFailureToMessage(failure),
      (newProducts) {
        if (newProducts.isEmpty || newProducts.length < 20) {
          _hasMore.value = false;  // আর নেই
        }
        _products.addAll(newProducts);
        _currentPage.value++;
      },
    );

    _isLoading.value = false;
    _isLoadingMore.value = false;
  }

  // পরবর্তী পেজ লোড (pagination)
  void loadMore() {
    if (!_isLoadingMore.value && _hasMore.value) {
      fetchProducts();
    }
  }

  // Search
  void search(String query) => _searchQuery.value = query;

  // Category filter
  void filterByCategory(String category) {
    _selectedCategory.value = category;
    fetchProducts(reset: true);
  }

  // নির্দিষ্ট পণ্যের বিস্তারিত
  Future<void> fetchProductById(String id) async {
    _isLoading.value = true;

    final result = await getProductByIdUseCase(GetProductByIdParams(id: id));

    result.fold(
      (failure) {
        _errorMessage.value = _mapFailureToMessage(failure);
        Get.snackbar('সমস্যা', _errorMessage.value);
      },
      (product) => _selectedProduct.value = product,
    );

    _isLoading.value = false;
  }

  // Refresh
  Future<void> refresh() => fetchProducts(reset: true);

  String _mapFailureToMessage(Failure failure) {
    if (failure is NetworkFailure) return 'ইন্টারনেট সংযোগ নেই';
    if (failure is ServerFailure) return failure.message;
    return 'পণ্য লোড ব্যর্থ হয়েছে';
  }
}
```

---

## ১৩. Presentation Layer — Binding

**Binding কী?** নির্দিষ্ট Screen-এর জন্য প্রয়োজনীয় সব নির্ভরতা তৈরি করে।

**কখন?** Route নির্ধারণের সময়। Screen খোলার আগে Binding চলে।

**কেন?** Screen বন্ধ হলে Controller স্বয়ংক্রিয় মুছে যায় — memory leak নেই।

```dart
// lib/features/auth/presentation/bindings/auth_binding.dart

import 'package:get/get.dart';
import '../../data/datasources/auth_local_datasource.dart';
import '../../data/datasources/auth_remote_datasource.dart';
import '../../data/repositories/auth_repository_impl.dart';
import '../../domain/repositories/auth_repository.dart';
import '../../domain/usecases/login_usecase.dart';
import '../../domain/usecases/logout_usecase.dart';
import '../../domain/usecases/register_usecase.dart';
import '../controllers/auth_controller.dart';

class AuthBinding extends Bindings {
  @override
  void dependencies() {
    // ─── Data Sources ───
    // lazyPut — প্রথমবার ব্যবহারের সময় তৈরি হয়
    Get.lazyPut<AuthRemoteDataSource>(
      () => AuthRemoteDataSourceImpl(
        apiClient: Get.find(),  // ApiClient আগে থেকেই আছে (InitialBinding-এ)
      ),
    );

    Get.lazyPut<AuthLocalDataSource>(
      () => AuthLocalDataSourceImpl(
        localStorage: Get.find(),
      ),
    );

    // ─── Repository ───
    Get.lazyPut<AuthRepository>(
      () => AuthRepositoryImpl(
        remoteDataSource: Get.find(),
        localDataSource: Get.find(),
        networkInfo: Get.find(),
      ),
    );

    // ─── Use Cases ───
    Get.lazyPut(() => LoginUseCase(Get.find()));
    Get.lazyPut(() => RegisterUseCase(Get.find()));
    Get.lazyPut(() => LogoutUseCase(Get.find()));

    // ─── Controller ───
    Get.lazyPut(
      () => AuthController(
        loginUseCase: Get.find(),
        registerUseCase: Get.find(),
        logoutUseCase: Get.find(),
      ),
    );
  }
}
```

```dart
// lib/features/products/presentation/bindings/product_binding.dart

import 'package:get/get.dart';
import '../../data/datasources/product_remote_datasource.dart';
import '../../data/repositories/product_repository_impl.dart';
import '../../domain/repositories/product_repository.dart';
import '../../domain/usecases/get_product_by_id_usecase.dart';
import '../../domain/usecases/get_products_usecase.dart';
import '../controllers/product_controller.dart';

class ProductBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut<ProductRemoteDataSource>(
      () => ProductRemoteDataSourceImpl(apiClient: Get.find()),
    );

    Get.lazyPut<ProductRepository>(
      () => ProductRepositoryImpl(
        remoteDataSource: Get.find(),
        networkInfo: Get.find(),
      ),
    );

    Get.lazyPut(() => GetProductsUseCase(Get.find()));
    Get.lazyPut(() => GetProductByIdUseCase(Get.find()));

    Get.lazyPut(
      () => ProductController(
        getProductsUseCase: Get.find(),
        getProductByIdUseCase: Get.find(),
      ),
    );
  }
}
```

---

## ১৪. Presentation Layer — View (UI)

**View কী?** শুধু দেখানোর কাজ। Controller-এর state দেখায়, Controller-এর action ডাকে।

**কখন?** সব Widget/Screen।

**কেন?** View-তে কোনো business logic নেই — শুধু দেখানো। এটি Controller-কে পরীক্ষাযোগ্য রাখে।

```dart
// lib/features/auth/presentation/views/login_view.dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../../../../core/widgets/custom_button.dart';
import '../../../../core/widgets/custom_text_field.dart';
import '../../../../app/routes/app_routes.dart';
import '../controllers/auth_controller.dart';

// GetView<T> — controller সরাসরি পাওয়া যায়
class LoginView extends GetView<AuthController> {
  const LoginView({super.key});

  @override
  Widget build(BuildContext context) {
    // Form controller — GetX-এ TextEditingController স্বাভাবিকভাবে ব্যবহার করুন
    final emailCtrl = TextEditingController();
    final passwordCtrl = TextEditingController();
    final formKey = GlobalKey<FormState>();

    return Scaffold(
      body: SafeArea(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(24),
          child: Form(
            key: formKey,
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: [
                const SizedBox(height: 60),

                // Logo
                const Icon(Icons.shopping_bag, size: 80, color: Colors.green),
                const SizedBox(height: 24),

                // Title
                Text(
                  'লগইন করুন',
                  style: Get.textTheme.headlineMedium?.copyWith(
                    fontWeight: FontWeight.bold,
                  ),
                  textAlign: TextAlign.center,
                ),
                const SizedBox(height: 40),

                // Email field
                CustomTextField(
                  controller: emailCtrl,
                  label: 'ইমেইল',
                  hint: 'your@email.com',
                  keyboardType: TextInputType.emailAddress,
                  prefixIcon: Icons.email_outlined,
                  validator: (v) {
                    if (v == null || v.isEmpty) return 'ইমেইল প্রয়োজন';
                    if (!GetUtils.isEmail(v)) return 'বৈধ ইমেইল লিখুন';
                    return null;
                  },
                ),
                const SizedBox(height: 16),

                // Password field
                CustomTextField(
                  controller: passwordCtrl,
                  label: 'পাসওয়ার্ড',
                  hint: '********',
                  obscureText: true,
                  prefixIcon: Icons.lock_outlined,
                  validator: (v) {
                    if (v == null || v.isEmpty) return 'পাসওয়ার্ড প্রয়োজন';
                    if (v.length < 6) return 'কমপক্ষে ৬ অক্ষর';
                    return null;
                  },
                ),
                const SizedBox(height: 8),

                // Forgot password
                Align(
                  alignment: Alignment.centerRight,
                  child: TextButton(
                    onPressed: () => Get.toNamed(AppRoutes.forgotPassword),
                    child: const Text('পাসওয়ার্ড ভুলে গেছেন?'),
                  ),
                ),
                const SizedBox(height: 24),

                // Login Button — Obx দিয়ে loading state দেখাই
                Obx(() => CustomButton(
                  text: 'লগইন',
                  isLoading: controller.isLoading,
                  onPressed: () {
                    if (formKey.currentState!.validate()) {
                      controller.login(
                        email: emailCtrl.text.trim(),
                        password: passwordCtrl.text,
                      );
                    }
                  },
                )),
                const SizedBox(height: 24),

                // Error message
                Obx(() {
                  if (controller.errorMessage.isEmpty) {
                    return const SizedBox.shrink();
                  }
                  return Container(
                    padding: const EdgeInsets.all(12),
                    decoration: BoxDecoration(
                      color: Colors.red.shade50,
                      borderRadius: BorderRadius.circular(8),
                      border: Border.all(color: Colors.red.shade200),
                    ),
                    child: Text(
                      controller.errorMessage,
                      style: TextStyle(color: Colors.red.shade700),
                      textAlign: TextAlign.center,
                    ),
                  );
                }),

                // Register link
                Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    const Text('অ্যাকাউন্ট নেই?'),
                    TextButton(
                      onPressed: () => Get.toNamed(AppRoutes.register),
                      child: const Text('নিবন্ধন করুন'),
                    ),
                  ],
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

```dart
// lib/features/products/presentation/views/product_list_view.dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../../../../app/routes/app_routes.dart';
import '../controllers/product_controller.dart';

class ProductListView extends GetView<ProductController> {
  const ProductListView({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('পণ্যসমূহ'),
        bottom: PreferredSize(
          preferredSize: const Size.fromHeight(60),
          child: Padding(
            padding: const EdgeInsets.fromLTRB(16, 0, 16, 8),
            child: TextField(
              decoration: InputDecoration(
                hintText: 'পণ্য খুঁজুন...',
                prefixIcon: const Icon(Icons.search),
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(12),
                  borderSide: BorderSide.none,
                ),
                filled: true,
                fillColor: Colors.grey.shade100,
              ),
              onChanged: controller.search,  // debounce controller-এ আছে
            ),
          ),
        ),
      ),
      body: Obx(() {
        // Loading state
        if (controller.isLoading) {
          return const Center(child: CircularProgressIndicator());
        }

        // Error state
        if (controller.errorMessage.isNotEmpty && controller.products.isEmpty) {
          return Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                const Icon(Icons.error_outline, size: 60, color: Colors.red),
                const SizedBox(height: 16),
                Text(controller.errorMessage),
                const SizedBox(height: 16),
                ElevatedButton(
                  onPressed: controller.refresh,
                  child: const Text('পুনরায় চেষ্টা'),
                ),
              ],
            ),
          );
        }

        // Empty state
        if (controller.products.isEmpty) {
          return const Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(Icons.inventory_2_outlined, size: 60, color: Colors.grey),
                SizedBox(height: 16),
                Text('কোনো পণ্য নেই'),
              ],
            ),
          );
        }

        // Products grid
        return RefreshIndicator(
          onRefresh: controller.refresh,
          child: GridView.builder(
            padding: const EdgeInsets.all(12),
            gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
              crossAxisCount: 2,
              crossAxisSpacing: 12,
              mainAxisSpacing: 12,
              childAspectRatio: 0.72,
            ),
            itemCount: controller.products.length + (controller.hasMore ? 1 : 0),
            itemBuilder: (context, index) {
              // Loading more indicator — শেষে
              if (index == controller.products.length) {
                controller.loadMore();  // পরবর্তী পেজ লোড করি
                return const Center(
                  child: Padding(
                    padding: EdgeInsets.all(16),
                    child: CircularProgressIndicator(),
                  ),
                );
              }

              final product = controller.products[index];
              return _ProductCard(
                product: product,
                onTap: () {
                  Get.toNamed(
                    AppRoutes.productDetail,
                    arguments: product.id,
                  );
                },
              );
            },
          ),
        );
      }),
    );
  }
}

// Private widget — শুধু এই ফাইলে ব্যবহার
class _ProductCard extends StatelessWidget {
  final dynamic product;
  final VoidCallback onTap;

  const _ProductCard({required this.product, required this.onTap});

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onTap,
      child: Card(
        clipBehavior: Clip.antiAlias,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Expanded(
              child: Stack(
                fit: StackFit.expand,
                children: [
                  product.hasThumbnail
                    ? Image.network(product.thumbnail, fit: BoxFit.cover)
                    : Container(color: Colors.grey.shade200,
                        child: const Icon(Icons.image, size: 40)),
                  if (product.isLowStock)
                    Positioned(
                      top: 8, right: 8,
                      child: Container(
                        padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 4),
                        decoration: BoxDecoration(
                          color: Colors.orange,
                          borderRadius: BorderRadius.circular(12),
                        ),
                        child: const Text('কম আছে',
                          style: TextStyle(color: Colors.white, fontSize: 10)),
                      ),
                    ),
                ],
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(10),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(product.name,
                    maxLines: 2,
                    overflow: TextOverflow.ellipsis,
                    style: const TextStyle(fontWeight: FontWeight.w600)),
                  const SizedBox(height: 4),
                  Row(
                    children: [
                      const Icon(Icons.star, size: 14, color: Colors.amber),
                      Text(' ${product.rating}',
                        style: const TextStyle(fontSize: 12, color: Colors.grey)),
                    ],
                  ),
                  const SizedBox(height: 6),
                  Text(product.formattedPrice,
                    style: TextStyle(
                      color: Colors.green.shade700,
                      fontWeight: FontWeight.bold,
                      fontSize: 16,
                    )),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## ১৫. GetX Routes সেটআপ

```dart
// lib/app/routes/app_routes.dart

// সব route name এখানে — constant হিসেবে
// typo থেকে বাঁচায়
abstract class AppRoutes {
  static const initial = '/';
  static const splash = '/splash';
  static const onboarding = '/onboarding';

  // Auth
  static const login = '/login';
  static const register = '/register';
  static const forgotPassword = '/forgot-password';

  // Main
  static const home = '/home';
  static const profile = '/profile';
  static const editProfile = '/edit-profile';
  static const settings = '/settings';

  // Products
  static const productList = '/products';
  static const productDetail = '/products/detail';

  // Cart & Order
  static const cart = '/cart';
  static const checkout = '/checkout';
  static const orderHistory = '/orders';
  static const orderDetail = '/orders/detail';
}
```

```dart
// lib/app/routes/app_pages.dart

import 'package:get/get.dart';
import '../../features/auth/presentation/bindings/auth_binding.dart';
import '../../features/auth/presentation/views/login_view.dart';
import '../../features/auth/presentation/views/register_view.dart';
import '../../features/products/presentation/bindings/product_binding.dart';
import '../../features/products/presentation/views/product_list_view.dart';
import '../../features/products/presentation/views/product_detail_view.dart';
import '../bindings/initial_binding.dart';
import 'app_routes.dart';

class AppPages {
  // প্রথম route
  static const initial = AppRoutes.splash;

  // সব page-এর তালিকা
  static final routes = [
    GetPage(
      name: AppRoutes.splash,
      page: () => const SplashView(),
      binding: InitialBinding(),  // অ্যাপ শুরুর নির্ভরতা
    ),

    // ─── Auth ───
    GetPage(
      name: AppRoutes.login,
      page: () => const LoginView(),
      binding: AuthBinding(),
      // Transition
      transition: Transition.fadeIn,
      transitionDuration: const Duration(milliseconds: 300),
    ),

    GetPage(
      name: AppRoutes.register,
      page: () => const RegisterView(),
      binding: AuthBinding(),  // একই Binding — GetX শেয়ার করে
      transition: Transition.rightToLeft,
    ),

    GetPage(
      name: AppRoutes.forgotPassword,
      page: () => const ForgotPasswordView(),
      binding: AuthBinding(),
    ),

    // ─── Products ───
    GetPage(
      name: AppRoutes.productList,
      page: () => const ProductListView(),
      binding: ProductBinding(),
      // Middleware — লগইন না থাকলে redirect
      middlewares: [AuthMiddleware()],
    ),

    GetPage(
      name: AppRoutes.productDetail,
      page: () => const ProductDetailView(),
      binding: ProductBinding(),
      middlewares: [AuthMiddleware()],
    ),

    // ─── Home ───
    GetPage(
      name: AppRoutes.home,
      page: () => const HomeView(),
      bindings: [
        ProductBinding(),  // একাধিক Binding
        AuthBinding(),
      ],
      middlewares: [AuthMiddleware()],
    ),
  ];
}

// Auth Middleware — লগইন না থাকলে redirect
class AuthMiddleware extends GetMiddleware {
  @override
  RouteSettings? redirect(String? route) {
    // AuthController আছে কিনা ও logged in কিনা
    final authCtrl = Get.find<AuthController>();
    if (!authCtrl.isLoggedIn) {
      return const RouteSettings(name: AppRoutes.login);
    }
    return null;  // null = redirect করো না
  }
}
```

---

## ১৬. Dependency Injection (GetX)

```dart
// lib/app/bindings/initial_binding.dart
// অ্যাপ শুরুর সময় সব global নির্ভরতা তৈরি করে

import 'package:get/get.dart';
import '../../core/network/api_client.dart';
import '../../core/network/network_info.dart';
import '../../core/storage/local_storage.dart';

class InitialBinding extends Bindings {
  @override
  void dependencies() {
    // ─── Core Services ───
    // permanentGet — কখনো মুছবে না
    Get.put<LocalStorage>(
      LocalStorageImpl(),
      permanent: true,
    );

    Get.put<NetworkInfo>(
      NetworkInfoImpl(),
      permanent: true,
    );

    Get.put<ApiClient>(
      ApiClient(
        baseUrl: 'https://api.example.com',
        localStorage: Get.find(),
      ),
      permanent: true,
    );
  }
}
```

```dart
// lib/main.dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'app/app.dart';
import 'app/bindings/initial_binding.dart';

Future<void> main() async {
  // Flutter binding initialize করি
  WidgetsFlutterBinding.ensureInitialized();

  // SharedPreferences ইত্যাদি async init
  await _initServices();

  runApp(const MyApp());
}

Future<void> _initServices() async {
  // LocalStorage initialize
  final localStorage = LocalStorageImpl();
  await localStorage.init();
  Get.put<LocalStorage>(localStorage, permanent: true);
}
```

```dart
// lib/app/app.dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'bindings/initial_binding.dart';
import 'routes/app_pages.dart';
import '../core/theme/app_theme.dart';
import '../core/translations/app_translations.dart';

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'বাংলা শপ',
      debugShowCheckedModeBanner: false,

      // Theme
      theme: AppTheme.lightTheme,
      darkTheme: AppTheme.darkTheme,
      themeMode: ThemeMode.system,

      // i18n
      translations: AppTranslations(),
      locale: const Locale('bn', 'BD'),
      fallbackLocale: const Locale('en', 'US'),

      // Navigation
      initialRoute: AppPages.initial,
      getPages: AppPages.routes,

      // Global Binding
      initialBinding: InitialBinding(),

      // Default Transition
      defaultTransition: Transition.cupertino,
    );
  }
}
```

---

## ১৭. Error Handling

```dart
// lib/core/errors/exceptions.dart
// Data layer-এ throw হয়

class ServerException implements Exception {
  final String message;
  final int? statusCode;
  const ServerException({required this.message, this.statusCode});

  @override
  String toString() => 'ServerException: $message (code: $statusCode)';
}

class UnauthorizedException implements Exception {
  final String message;
  const UnauthorizedException([this.message = 'অননুমোদিত অ্যাক্সেস']);
}

class NetworkException implements Exception {
  final String message;
  const NetworkException([this.message = 'নেটওয়ার্ক সমস্যা']);
}

class CacheException implements Exception {
  final String message;
  const CacheException([this.message = 'ক্যাশ সমস্যা']);
}
```

```dart
// lib/core/errors/failures.dart
// Domain layer-এ ব্যবহার হয়

import 'package:equatable/equatable.dart';

// Base Failure — সব Failure এটি extend করে
abstract class Failure extends Equatable {
  final String message;
  const Failure(this.message);

  @override
  List<Object> get props => [message];
}

// নির্দিষ্ট Failure ধরন
class ServerFailure extends Failure {
  const ServerFailure(super.message);
}

class NetworkFailure extends Failure {
  const NetworkFailure(super.message);
}

class AuthFailure extends Failure {
  const AuthFailure(super.message);
}

class ValidationFailure extends Failure {
  const ValidationFailure(super.message);
}

class CacheFailure extends Failure {
  const CacheFailure(super.message);
}

class NotFoundFailure extends Failure {
  const NotFoundFailure(super.message);
}
```

---

## ১৮. API Service Layer

```dart
// lib/core/network/api_client.dart

import 'package:dio/dio.dart';
import 'package:get/get.dart' as getx;
import '../constants/api_constants.dart';
import '../errors/exceptions.dart';
import '../storage/local_storage.dart';

class ApiClient {
  late final Dio _dio;
  final LocalStorage localStorage;

  ApiClient({required String baseUrl, required this.localStorage}) {
    _dio = Dio(BaseOptions(
      baseUrl: baseUrl,
      connectTimeout: const Duration(seconds: 15),
      receiveTimeout: const Duration(seconds: 15),
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
      },
    ));

    // ─── Interceptors ───
    _dio.interceptors.add(_AuthInterceptor(localStorage));
    _dio.interceptors.add(_ErrorInterceptor());

    // Development-এ logging
    _dio.interceptors.add(LogInterceptor(
      requestBody: true,
      responseBody: true,
      error: true,
    ));
  }

  // ─── HTTP Methods ───
  Future<Response> get(String path, {Map<String, dynamic>? queryParameters}) async {
    return _dio.get(path, queryParameters: queryParameters);
  }

  Future<Response> post(String path, {dynamic data}) async {
    return _dio.post(path, data: data);
  }

  Future<Response> put(String path, {dynamic data}) async {
    return _dio.put(path, data: data);
  }

  Future<Response> patch(String path, {dynamic data}) async {
    return _dio.patch(path, data: data);
  }

  Future<Response> delete(String path) async {
    return _dio.delete(path);
  }
}

// Auth Interceptor — প্রতি request-এ token যোগ করে
class _AuthInterceptor extends Interceptor {
  final LocalStorage localStorage;

  _AuthInterceptor(this.localStorage);

  @override
  void onRequest(RequestOptions options, RequestInterceptorHandler handler) async {
    final token = await localStorage.getString('auth_token');
    if (token != null) {
      options.headers['Authorization'] = 'Bearer $token';
    }
    handler.next(options);
  }

  @override
  void onResponse(Response response, ResponseInterceptorHandler handler) {
    // Response-এ নতুন token থাকলে সংরক্ষণ করি
    final newToken = response.headers.value('X-New-Token');
    if (newToken != null) {
      localStorage.setString('auth_token', newToken);
    }
    handler.next(response);
  }
}

// Error Interceptor — HTTP error → Exception রূপান্তর
class _ErrorInterceptor extends Interceptor {
  @override
  void onError(DioException err, ErrorInterceptorHandler handler) {
    switch (err.type) {
      case DioExceptionType.connectionTimeout:
      case DioExceptionType.receiveTimeout:
        throw NetworkException('সংযোগ সময়সীমা পেরিয়ে গেছে');

      case DioExceptionType.connectionError:
        throw NetworkException('ইন্টারনেট সংযোগ নেই');

      case DioExceptionType.badResponse:
        final statusCode = err.response?.statusCode;
        final message = err.response?.data?['message'] ??
                        err.response?.data?['error'] ??
                        'সার্ভার সমস্যা';

        if (statusCode == 401) {
          throw UnauthorizedException(message);
        } else if (statusCode == 422) {
          // Validation error
          throw ServerException(message: message, statusCode: statusCode);
        } else {
          throw ServerException(message: message, statusCode: statusCode);
        }

      default:
        throw ServerException(message: err.message ?? 'অজানা সমস্যা');
    }
  }
}
```

```dart
// lib/core/network/network_info.dart

import 'package:connectivity_plus/connectivity_plus.dart';

abstract class NetworkInfo {
  Future<bool> get isConnected;
}

class NetworkInfoImpl implements NetworkInfo {
  final Connectivity connectivity;

  NetworkInfoImpl() : connectivity = Connectivity();

  @override
  Future<bool> get isConnected async {
    final result = await connectivity.checkConnectivity();
    return result != ConnectivityResult.none;
  }
}
```

```dart
// lib/core/constants/api_constants.dart

abstract class ApiConstants {
  // Base URL — environment অনুযায়ী পরিবর্তন করুন
  static const baseUrl = 'https://api.yourapp.com/v1';

  // Auth
  static const loginEndpoint = '/auth/login';
  static const registerEndpoint = '/auth/register';
  static const logoutEndpoint = '/auth/logout';
  static const profileEndpoint = '/auth/profile';
  static const refreshTokenEndpoint = '/auth/refresh';

  // Products
  static const productsEndpoint = '/products';
  static const categoriesEndpoint = '/categories';

  // Orders
  static const ordersEndpoint = '/orders';
  static const cartEndpoint = '/cart';
}
```

---

## ১৯. Local Storage Service

```dart
// lib/core/storage/local_storage.dart

import 'package:shared_preferences/shared_preferences.dart';

abstract class LocalStorage {
  Future<void> init();
  Future<void> setString(String key, String value);
  Future<String?> getString(String key);
  Future<void> setBool(String key, bool value);
  Future<bool?> getBool(String key);
  Future<void> setInt(String key, int value);
  Future<int?> getInt(String key);
  Future<void> remove(String key);
  Future<void> clear();
  bool containsKey(String key);
}

class LocalStorageImpl implements LocalStorage {
  SharedPreferences? _prefs;

  @override
  Future<void> init() async {
    _prefs = await SharedPreferences.getInstance();
  }

  SharedPreferences get _instance {
    if (_prefs == null) throw Exception('LocalStorage initialize হয়নি');
    return _prefs!;
  }

  @override
  Future<void> setString(String key, String value) =>
      _instance.setString(key, value);

  @override
  Future<String?> getString(String key) async =>
      _instance.getString(key);

  @override
  Future<void> setBool(String key, bool value) =>
      _instance.setBool(key, value);

  @override
  Future<bool?> getBool(String key) async =>
      _instance.getBool(key);

  @override
  Future<void> setInt(String key, int value) =>
      _instance.setInt(key, value);

  @override
  Future<int?> getInt(String key) async =>
      _instance.getInt(key);

  @override
  Future<void> remove(String key) => _instance.remove(key);

  @override
  Future<void> clear() => _instance.clear();

  @override
  bool containsKey(String key) => _instance.containsKey(key);
}
```

---

## ২০. Auth Flow সম্পূর্ণ উদাহরণ

```dart
// ─── সম্পূর্ণ Auth Flow ───

// ১. User লগইন বাটনে ক্লিক করে (LoginView)
// ২. LoginView → AuthController.login() ডাকে
// ৩. AuthController → LoginUseCase() ডাকে
// ৪. LoginUseCase → AuthRepository.login() ডাকে (abstract)
// ৫. AuthRepositoryImpl → AuthRemoteDataSource.login() ডাকে
// ৬. AuthRemoteDataSourceImpl → ApiClient.post('/auth/login') ডাকে
// ৭. Dio → সার্ভারে HTTP POST করে
// ৮. সার্ভার → JSON response পাঠায়
// ৯. ApiClient → Dio Response পায়
// ১০. AuthRemoteDataSourceImpl → UserModel.fromJson() তৈরি করে return করে
// ১১. AuthRepositoryImpl → UserModel পায়, cache করে, Right(userModel) return করে
// ১২. LoginUseCase → Right(userModel) পায়, return করে
// ১৩. AuthController → fold() — Right তাই user set করে, HomeScreen-এ navigate করে
// ১৪. LoginView → Obx() — isLoading false হয়, UI আপডেট হয়

// Splash Screen — Auto-login চেক
class SplashView extends GetView<AuthController> {
  const SplashView({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.green,
      body: Center(
        child: FutureBuilder(
          future: _checkAuth(),
          builder: (context, snapshot) {
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: const [
                Icon(Icons.shopping_bag, size: 100, color: Colors.white),
                SizedBox(height: 24),
                Text('বাংলা শপ',
                  style: TextStyle(color: Colors.white, fontSize: 32,
                    fontWeight: FontWeight.bold)),
                SizedBox(height: 48),
                CircularProgressIndicator(color: Colors.white),
              ],
            );
          },
        ),
      ),
    );
  }

  Future<void> _checkAuth() async {
    await Future.delayed(const Duration(seconds: 2));  // Splash দেখানো
    // Token আছে কিনা চেক করি
    final result = await Get.find<GetCurrentUserUseCase>()(const NoParams());
    result.fold(
      (_) => Get.offAllNamed(AppRoutes.login),
      (user) {
        if (user != null) {
          Get.offAllNamed(AppRoutes.home);
        } else {
          Get.offAllNamed(AppRoutes.login);
        }
      },
    );
  }
}
```

---

## ২১. GetX State Management — Rx বিস্তারিত

```dart
// GetX-এ State পরিচালনার সব পদ্ধতি

class ExampleController extends GetxController {

  // ─── Rx Types ───
  final count = 0.obs;                    // RxInt
  final name = ''.obs;                    // RxString
  final isLoading = false.obs;            // RxBool
  final price = 0.0.obs;                  // RxDouble
  final items = <String>[].obs;           // RxList<String>
  final user = Rxn<UserEntity>();         // Rxn (nullable) = RxnT
  final map = <String, dynamic>{}.obs;    // RxMap

  // ─── Rx পড়া ───
  void readValues() {
    print(count.value);     // .value দিয়ে পড়ি
    print(name.value);
    print(items.length);    // List-এর জন্য সরাসরি
  }

  // ─── Rx লেখা ───
  void writeValues() {
    count.value++;          // int increment
    count.value = 10;       // সরাসরি set
    name.value = 'করিম';
    isLoading.toggle();     // bool toggle

    // List operations
    items.add('নতুন আইটেম');
    items.remove('পুরানো');
    items.addAll(['এক', 'দুই']);
    items.clear();

    // Nullable
    user.value = UserEntity(...);
    user.value = null;  // clear করা
  }

  // ─── Workers ───
  @override
  void onInit() {
    super.onInit();

    // ever — প্রতিবার পরিবর্তনে
    ever(count, (val) => print('count পরিবর্তন হয়েছে: $val'));

    // once — শুধু প্রথমবার
    once(count, (val) => print('প্রথম পরিবর্তন: $val'));

    // debounce — পরিবর্তনের ৫০০ms পরে
    debounce(name, (val) => searchUser(val),
        time: const Duration(milliseconds: 500));

    // interval — সর্বোচ্চ ১ সেকেন্ডে একবার
    interval(count, (val) => updateServer(val),
        time: const Duration(seconds: 1));
  }

  void searchUser(String query) {}
  void updateServer(int val) {}
}

// ─── UI-তে Rx ব্যবহার ───
class ExampleView extends GetView<ExampleController> {
  const ExampleView({super.key});

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Obx — সবচেয়ে বেশি ব্যবহৃত
        Obx(() => Text('গণনা: ${controller.count}')),

        // GetX — Controller এবং context দুটো পাওয়া যায়
        GetX<ExampleController>(
          builder: (ctrl) => Text('নাম: ${ctrl.name}'),
        ),

        // Obx — শুধু নির্দিষ্ট Rx observe করে (পারফরম্যান্স ভালো)
        Obx(() => controller.isLoading
          ? const CircularProgressIndicator()
          : const Text('লোড হয়েছে')
        ),

        // GetBuilder — setState-এর মতো (manual update)
        // GetX-এর Rx না থাকলে
        GetBuilder<ExampleController>(
          builder: (ctrl) => Text('manual: ${ctrl.count}'),
        ),
      ],
    );
  }
}
```

---

## ২২. GetX Navigation বিস্তারিত

```dart
// GetX Navigation — সব পদ্ধতি

class NavigationExamples {
  void examples() {

    // ─── Basic Navigation ───
    Get.to(() => const DetailView());          // Stack-এ push
    Get.back();                                // Pop — আগের screen
    Get.back(result: 'selected_data');         // Data নিয়ে ফিরে যাও

    // Named routes
    Get.toNamed(AppRoutes.productDetail);
    Get.toNamed(AppRoutes.productDetail, arguments: {'id': '123'});

    // ─── Stack Control ───
    Get.off(() => const HomeView());           // Current replace করে
    Get.offAll(() => const LoginView());       // সব সরিয়ে দেয়
    Get.offNamed(AppRoutes.home);
    Get.offAllNamed(AppRoutes.login);

    // Conditional
    Get.offAllNamed(
      AppRoutes.home,
      predicate: (route) => route.settings.name == AppRoutes.splash,
    );

    // ─── Arguments পাওয়া ───
    // Sending
    Get.toNamed(AppRoutes.detail, arguments: ProductEntity(...));
    Get.toNamed(AppRoutes.detail, arguments: {'id': '123', 'name': 'আম'});

    // Receiving (View-এ)
    final product = Get.arguments as ProductEntity;
    final args = Get.arguments as Map<String, dynamic>;
    final id = args['id'];

    // ─── Path Parameters ───
    Get.toNamed('/products/123');  // Route-এ /products/:id থাকলে
    final id2 = Get.parameters['id'];  // '123'

    // ─── Result পাওয়া ───
    Future<void> getResult() async {
      final result = await Get.toNamed(AppRoutes.selection);
      if (result != null) {
        print('নির্বাচিত: $result');
      }
    }

    // ─── Dialog ও BottomSheet ───
    Get.dialog(AlertDialog(
      title: const Text('নিশ্চিত করুন'),
      actions: [
        TextButton(onPressed: () => Get.back(result: false), child: const Text('না')),
        TextButton(onPressed: () => Get.back(result: true), child: const Text('হ্যাঁ')),
      ],
    ));

    Get.bottomSheet(
      Container(
        height: 200,
        child: const Center(child: Text('Bottom Sheet')),
      ),
      backgroundColor: Colors.white,
      shape: const RoundedRectangleBorder(
        borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
      ),
    );
  }
}
```

---

## ২৩. GetX Snackbar, Dialog, BottomSheet

```dart
// lib/core/utils/app_dialogs.dart
// সব জায়গায় একই স্টাইলের Snackbar/Dialog

import 'package:flutter/material.dart';
import 'package:get/get.dart';

class AppDialogs {
  // ─── Snackbars ───
  static void showSuccess(String message, {String title = 'সফল'}) {
    Get.snackbar(
      title,
      message,
      snackPosition: SnackPosition.TOP,
      backgroundColor: Colors.green.shade600,
      colorText: Colors.white,
      icon: const Icon(Icons.check_circle, color: Colors.white),
      duration: const Duration(seconds: 3),
      borderRadius: 12,
      margin: const EdgeInsets.all(16),
      isDismissible: true,
      forwardAnimationCurve: Curves.easeOutBack,
    );
  }

  static void showError(String message, {String title = 'সমস্যা'}) {
    Get.snackbar(
      title,
      message,
      snackPosition: SnackPosition.TOP,
      backgroundColor: Colors.red.shade600,
      colorText: Colors.white,
      icon: const Icon(Icons.error_outline, color: Colors.white),
      duration: const Duration(seconds: 4),
      borderRadius: 12,
      margin: const EdgeInsets.all(16),
    );
  }

  static void showInfo(String message) {
    Get.snackbar(
      'তথ্য',
      message,
      snackPosition: SnackPosition.BOTTOM,
      backgroundColor: Colors.blue.shade600,
      colorText: Colors.white,
    );
  }

  static void showWarning(String message) {
    Get.snackbar(
      'সতর্কতা',
      message,
      backgroundColor: Colors.orange.shade600,
      colorText: Colors.white,
      icon: const Icon(Icons.warning_amber, color: Colors.white),
    );
  }

  // ─── Confirmation Dialog ───
  static Future<bool> showConfirmation({
    required String title,
    required String message,
    String confirmText = 'হ্যাঁ',
    String cancelText = 'না',
  }) async {
    final result = await Get.dialog<bool>(
      AlertDialog(
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
        title: Text(title),
        content: Text(message),
        actions: [
          TextButton(
            onPressed: () => Get.back(result: false),
            child: Text(cancelText),
          ),
          ElevatedButton(
            onPressed: () => Get.back(result: true),
            style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
            child: Text(confirmText, style: const TextStyle(color: Colors.white)),
          ),
        ],
      ),
      barrierDismissible: false,
    );
    return result ?? false;
  }

  // ─── Loading Dialog ───
  static void showLoading({String message = 'অপেক্ষা করুন...'}) {
    Get.dialog(
      WillPopScope(
        onWillPop: () async => false,  // Back বাটনে বন্ধ হবে না
        child: Center(
          child: Container(
            padding: const EdgeInsets.all(24),
            decoration: BoxDecoration(
              color: Colors.white,
              borderRadius: BorderRadius.circular(12),
            ),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                const CircularProgressIndicator(),
                const SizedBox(height: 16),
                Text(message),
              ],
            ),
          ),
        ),
      ),
      barrierDismissible: false,
    );
  }

  static void hideLoading() {
    if (Get.isDialogOpen!) Get.back();
  }
}
```

---

## ২৪. Internationalization (i18n) with GetX

```dart
// lib/core/translations/app_translations.dart

import 'package:get/get.dart';

class AppTranslations extends Translations {
  @override
  Map<String, Map<String, String>> get keys => {
    'bn_BD': {
      // Common
      'app_name': 'বাংলা শপ',
      'loading': 'লোড হচ্ছে...',
      'error': 'সমস্যা হয়েছে',
      'retry': 'পুনরায় চেষ্টা',
      'cancel': 'বাতিল',
      'confirm': 'নিশ্চিত',
      'save': 'সংরক্ষণ',
      'delete': 'মুছুন',
      'edit': 'সম্পাদনা',

      // Auth
      'login': 'লগইন',
      'register': 'নিবন্ধন',
      'logout': 'লগআউট',
      'email': 'ইমেইল',
      'password': 'পাসওয়ার্ড',
      'forgot_password': 'পাসওয়ার্ড ভুলে গেছেন?',

      // Products
      'products': 'পণ্যসমূহ',
      'search_products': 'পণ্য খুঁজুন...',
      'no_products': 'কোনো পণ্য নেই',
      'add_to_cart': 'কার্টে যোগ করুন',
      'out_of_stock': 'স্টক নেই',

      // Validation
      'required_field': 'এই তথ্য প্রয়োজন',
      'invalid_email': 'বৈধ ইমেইল লিখুন',
      'short_password': 'পাসওয়ার্ড কমপক্ষে ৬ অক্ষরের হতে হবে',

      // Errors
      'network_error': 'ইন্টারনেট সংযোগ নেই',
      'server_error': 'সার্ভার সমস্যা হয়েছে',
      'unauthorized': 'অননুমোদিত অ্যাক্সেস',
    },
    'en_US': {
      'app_name': 'Bangla Shop',
      'loading': 'Loading...',
      'error': 'Error occurred',
      'login': 'Login',
      'products': 'Products',
      // ... বাকি translations
    },
  };
}

// ব্যবহার
// Text('login'.tr)  →  'লগইন' (bn) বা 'Login' (en)
// 'short_password'.tr  →  'পাসওয়ার্ড কমপক্ষে ৬ অক্ষরের হতে হবে'

// ভাষা পরিবর্তন
void changeLanguage(String langCode, String countryCode) {
  Get.updateLocale(Locale(langCode, countryCode));
}
```

---

## ২৫. Theme Management with GetX

```dart
// lib/core/theme/app_theme.dart

import 'package:flutter/material.dart';
import 'app_colors.dart';

class AppTheme {
  static ThemeData get lightTheme {
    return ThemeData(
      useMaterial3: true,
      brightness: Brightness.light,
      colorScheme: ColorScheme.fromSeed(
        seedColor: AppColors.primary,
        brightness: Brightness.light,
      ),
      appBarTheme: const AppBarTheme(
        centerTitle: true,
        elevation: 0,
        scrolledUnderElevation: 1,
      ),
      elevatedButtonTheme: ElevatedButtonThemeData(
        style: ElevatedButton.styleFrom(
          padding: const EdgeInsets.symmetric(horizontal: 32, vertical: 14),
          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
        ),
      ),
      inputDecorationTheme: InputDecorationTheme(
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(12)),
        contentPadding: const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
      ),
      cardTheme: CardTheme(
        elevation: 2,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
      ),
    );
  }

  static ThemeData get darkTheme {
    return ThemeData(
      useMaterial3: true,
      brightness: Brightness.dark,
      colorScheme: ColorScheme.fromSeed(
        seedColor: AppColors.primary,
        brightness: Brightness.dark,
      ),
    );
  }
}
```

```dart
// lib/core/controllers/theme_controller.dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../storage/local_storage.dart';

class ThemeController extends GetxController {
  final LocalStorage localStorage;
  static const String _themeKey = 'theme_mode';

  ThemeController({required this.localStorage});

  final _themeMode = ThemeMode.system.obs;
  ThemeMode get themeMode => _themeMode.value;
  bool get isDarkMode => _themeMode.value == ThemeMode.dark;

  @override
  void onInit() {
    super.onInit();
    _loadTheme();
  }

  Future<void> _loadTheme() async {
    final saved = await localStorage.getString(_themeKey);
    if (saved == 'dark') {
      _themeMode.value = ThemeMode.dark;
    } else if (saved == 'light') {
      _themeMode.value = ThemeMode.light;
    }
    Get.changeThemeMode(_themeMode.value);
  }

  Future<void> toggleTheme() async {
    if (_themeMode.value == ThemeMode.light) {
      _themeMode.value = ThemeMode.dark;
      await localStorage.setString(_themeKey, 'dark');
    } else {
      _themeMode.value = ThemeMode.light;
      await localStorage.setString(_themeKey, 'light');
    }
    Get.changeThemeMode(_themeMode.value);
  }

  Future<void> setThemeMode(ThemeMode mode) async {
    _themeMode.value = mode;
    await localStorage.setString(_themeKey, mode.name);
    Get.changeThemeMode(mode);
  }
}
```

---

## ২৬. Unit Testing Clean Architecture

```dart
// test/features/auth/domain/usecases/login_usecase_test.dart

import 'package:dartz/dartz.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:mockito/annotations.dart';
import 'package:mockito/mockito.dart';

import 'package:myapp/core/errors/failures.dart';
import 'package:myapp/features/auth/domain/entities/user_entity.dart';
import 'package:myapp/features/auth/domain/repositories/auth_repository.dart';
import 'package:myapp/features/auth/domain/usecases/login_usecase.dart';

// Mock generation — mockito
@GenerateMocks([AuthRepository])
import 'login_usecase_test.mocks.dart';

void main() {
  late LoginUseCase loginUseCase;
  late MockAuthRepository mockRepository;

  // প্রতিটি test-এর আগে নতুন instance
  setUp(() {
    mockRepository = MockAuthRepository();
    loginUseCase = LoginUseCase(mockRepository);
  });

  // Test data
  const testUser = UserEntity(
    id: '1',
    name: 'করিম',
    email: 'karim@test.com',
    role: UserRole.user,
    createdAt: DateTime(2024, 1, 1),
    isVerified: true,
  );

  const testParams = LoginParams(
    email: 'karim@test.com',
    password: '123456',
  );

  group('LoginUseCase', () {
    test('সফল লগইনে UserEntity return করে', () async {
      // ─── Arrange ───
      // Repository mock করি — সফল response দেবে
      when(mockRepository.login(
        email: testParams.email,
        password: testParams.password,
      )).thenAnswer((_) async => const Right(testUser));

      // ─── Act ───
      final result = await loginUseCase(testParams);

      // ─── Assert ───
      expect(result, const Right(testUser));
      // Repository একবার ডাকা হয়েছে কিনা
      verify(mockRepository.login(
        email: testParams.email,
        password: testParams.password,
      ));
      verifyNoMoreInteractions(mockRepository);
    });

    test('ব্যর্থ লগইনে ServerFailure return করে', () async {
      // Arrange
      when(mockRepository.login(
        email: anyNamed('email'),
        password: anyNamed('password'),
      )).thenAnswer((_) async => Left(ServerFailure('ইমেইল বা পাসওয়ার্ড ভুল')));

      // Act
      final result = await loginUseCase(testParams);

      // Assert
      expect(result, isA<Left<Failure, UserEntity>>());
      result.fold(
        (failure) => expect(failure, isA<ServerFailure>()),
        (_) => fail('Failure expected'),
      );
    });

    test('নেটওয়ার্ক না থাকলে NetworkFailure return করে', () async {
      when(mockRepository.login(
        email: anyNamed('email'),
        password: anyNamed('password'),
      )).thenAnswer((_) async => Left(NetworkFailure('ইন্টারনেট নেই')));

      final result = await loginUseCase(testParams);

      expect(result.isLeft(), true);
    });
  });
}
```

```dart
// test/features/auth/presentation/controllers/auth_controller_test.dart

import 'package:dartz/dartz.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:get/get.dart';
import 'package:mockito/annotations.dart';
import 'package:mockito/mockito.dart';

import 'package:myapp/features/auth/domain/entities/user_entity.dart';
import 'package:myapp/features/auth/domain/usecases/login_usecase.dart';
import 'package:myapp/features/auth/domain/usecases/logout_usecase.dart';
import 'package:myapp/features/auth/domain/usecases/register_usecase.dart';
import 'package:myapp/features/auth/presentation/controllers/auth_controller.dart';

@GenerateMocks([LoginUseCase, RegisterUseCase, LogoutUseCase])
import 'auth_controller_test.mocks.dart';

void main() {
  late AuthController controller;
  late MockLoginUseCase mockLoginUseCase;
  late MockRegisterUseCase mockRegisterUseCase;
  late MockLogoutUseCase mockLogoutUseCase;

  setUp(() {
    mockLoginUseCase = MockLoginUseCase();
    mockRegisterUseCase = MockRegisterUseCase();
    mockLogoutUseCase = MockLogoutUseCase();

    controller = AuthController(
      loginUseCase: mockLoginUseCase,
      registerUseCase: mockRegisterUseCase,
      logoutUseCase: mockLogoutUseCase,
    );

    // GetX test mode
    Get.testMode = true;
  });

  tearDown(() {
    Get.reset();
  });

  const testUser = UserEntity(
    id: '1', name: 'করিম', email: 'karim@test.com',
    role: UserRole.user, createdAt: DateTime.utc(2024), isVerified: true,
  );

  test('লগইন সফল হলে user set হয় ও loading false হয়', () async {
    when(mockLoginUseCase(any))
        .thenAnswer((_) async => const Right(testUser));

    expect(controller.isLoading, false);

    final future = controller.login(email: 'karim@test.com', password: '123456');

    // Loading শুরু হয়েছে কিনা (তাৎক্ষণিক)
    expect(controller.isLoading, true);

    await future;

    // শেষে loading false ও user set
    expect(controller.isLoading, false);
    expect(controller.currentUser, testUser);
    expect(controller.isLoggedIn, true);
  });

  test('লগইন ব্যর্থ হলে error message set হয়', () async {
    when(mockLoginUseCase(any))
        .thenAnswer((_) async => Left(ServerFailure('ভুল পাসওয়ার্ড')));

    await controller.login(email: 'karim@test.com', password: 'wrong');

    expect(controller.currentUser, null);
    expect(controller.isLoggedIn, false);
    expect(controller.errorMessage, isNotEmpty);
  });
}
```

---

## ২৭. সম্পূর্ণ প্রজেক্ট — Todo App

```dart
// ─── Todo App সম্পূর্ণ উদাহরণ ───

// lib/features/todo/domain/entities/todo_entity.dart
class TodoEntity extends Equatable {
  final String id;
  final String title;
  final String? description;
  final bool isCompleted;
  final TodoPriority priority;
  final DateTime? dueDate;
  final DateTime createdAt;

  const TodoEntity({
    required this.id,
    required this.title,
    this.description,
    required this.isCompleted,
    required this.priority,
    this.dueDate,
    required this.createdAt,
  });

  bool get isOverdue =>
      dueDate != null && !isCompleted && dueDate!.isBefore(DateTime.now());

  TodoEntity copyWith({...}) {...}

  @override
  List<Object?> get props => [id, title, isCompleted, priority];
}

enum TodoPriority { low, medium, high }
```

```dart
// lib/features/todo/domain/repositories/todo_repository.dart
abstract class TodoRepository {
  Future<Either<Failure, List<TodoEntity>>> getTodos({bool? completed});
  Future<Either<Failure, TodoEntity>> createTodo(TodoEntity todo);
  Future<Either<Failure, TodoEntity>> updateTodo(TodoEntity todo);
  Future<Either<Failure, void>> deleteTodo(String id);
  Future<Either<Failure, void>> toggleComplete(String id);
}
```

```dart
// lib/features/todo/presentation/controllers/todo_controller.dart
class TodoController extends GetxController {
  final GetTodosUseCase getTodosUseCase;
  final CreateTodoUseCase createTodoUseCase;
  final UpdateTodoUseCase updateTodoUseCase;
  final DeleteTodoUseCase deleteTodoUseCase;
  final ToggleTodoUseCase toggleTodoUseCase;

  TodoController({
    required this.getTodosUseCase,
    required this.createTodoUseCase,
    required this.updateTodoUseCase,
    required this.deleteTodoUseCase,
    required this.toggleTodoUseCase,
  });

  final _todos = <TodoEntity>[].obs;
  final _isLoading = false.obs;
  final _filter = TodoFilter.all.obs;

  List<TodoEntity> get todos => _todos;
  bool get isLoading => _isLoading.value;

  // Computed — filter অনুযায়ী তালিকা
  List<TodoEntity> get filteredTodos {
    switch (_filter.value) {
      case TodoFilter.active:
        return _todos.where((t) => !t.isCompleted).toList();
      case TodoFilter.completed:
        return _todos.where((t) => t.isCompleted).toList();
      default:
        return _todos.toList();
    }
  }

  int get pendingCount => _todos.where((t) => !t.isCompleted).length;

  @override
  void onInit() {
    super.onInit();
    fetchTodos();
  }

  Future<void> fetchTodos() async {
    _isLoading.value = true;
    final result = await getTodosUseCase(const NoParams());
    result.fold(
      (failure) => AppDialogs.showError(failure.message),
      (todos) => _todos.assignAll(todos),
    );
    _isLoading.value = false;
  }

  Future<void> createTodo({
    required String title,
    String? description,
    TodoPriority priority = TodoPriority.medium,
    DateTime? dueDate,
  }) async {
    final todo = TodoEntity(
      id: DateTime.now().millisecondsSinceEpoch.toString(),
      title: title,
      description: description,
      isCompleted: false,
      priority: priority,
      dueDate: dueDate,
      createdAt: DateTime.now(),
    );

    final result = await createTodoUseCase(CreateTodoParams(todo: todo));
    result.fold(
      (failure) => AppDialogs.showError(failure.message),
      (created) {
        _todos.insert(0, created);
        AppDialogs.showSuccess('কাজ যোগ হয়েছে');
      },
    );
  }

  Future<void> toggleTodo(String id) async {
    // Optimistic update — আগে UI আপডেট করি, তারপর API
    final index = _todos.indexWhere((t) => t.id == id);
    if (index == -1) return;

    final original = _todos[index];
    _todos[index] = original.copyWith(isCompleted: !original.isCompleted);

    final result = await toggleTodoUseCase(ToggleTodoParams(id: id));
    result.fold(
      (failure) {
        // ব্যর্থ হলে revert
        _todos[index] = original;
        AppDialogs.showError(failure.message);
      },
      (updated) => _todos[index] = updated,
    );
  }

  Future<void> deleteTodo(String id) async {
    final confirmed = await AppDialogs.showConfirmation(
      title: 'মুছে ফেলবেন?',
      message: 'এই কাজটি স্থায়ীভাবে মুছে যাবে',
    );
    if (!confirmed) return;

    final result = await deleteTodoUseCase(DeleteTodoParams(id: id));
    result.fold(
      (failure) => AppDialogs.showError(failure.message),
      (_) {
        _todos.removeWhere((t) => t.id == id);
        AppDialogs.showSuccess('মুছে ফেলা হয়েছে');
      },
    );
  }

  void setFilter(TodoFilter filter) => _filter.value = filter;
}

enum TodoFilter { all, active, completed }
```

```dart
// lib/features/todo/presentation/views/todo_list_view.dart
class TodoListView extends GetView<TodoController> {
  const TodoListView({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Obx(() => Text('কাজের তালিকা (${controller.pendingCount} বাকি)')),
        actions: [
          // Filter menu
          PopupMenuButton<TodoFilter>(
            onSelected: controller.setFilter,
            itemBuilder: (_) => [
              const PopupMenuItem(value: TodoFilter.all, child: Text('সব')),
              const PopupMenuItem(value: TodoFilter.active, child: Text('বাকি')),
              const PopupMenuItem(value: TodoFilter.completed, child: Text('সম্পন্ন')),
            ],
          ),
        ],
      ),
      body: Obx(() {
        if (controller.isLoading) {
          return const Center(child: CircularProgressIndicator());
        }

        if (controller.filteredTodos.isEmpty) {
          return Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                const Icon(Icons.task_alt, size: 80, color: Colors.grey),
                const SizedBox(height: 16),
                const Text('কোনো কাজ নেই', style: TextStyle(fontSize: 18, color: Colors.grey)),
                const SizedBox(height: 8),
                ElevatedButton(
                  onPressed: () => _showAddTodoDialog(context),
                  child: const Text('নতুন কাজ যোগ করুন'),
                ),
              ],
            ),
          );
        }

        return ListView.builder(
          padding: const EdgeInsets.all(16),
          itemCount: controller.filteredTodos.length,
          itemBuilder: (context, index) {
            final todo = controller.filteredTodos[index];
            return _TodoCard(
              todo: todo,
              onToggle: () => controller.toggleTodo(todo.id),
              onDelete: () => controller.deleteTodo(todo.id),
              onTap: () => Get.toNamed(AppRoutes.todoDetail, arguments: todo),
            );
          },
        );
      }),
      floatingActionButton: FloatingActionButton.extended(
        onPressed: () => _showAddTodoDialog(context),
        icon: const Icon(Icons.add),
        label: const Text('নতুন কাজ'),
      ),
    );
  }

  void _showAddTodoDialog(BuildContext context) {
    final titleCtrl = TextEditingController();
    Get.dialog(
      AlertDialog(
        title: const Text('নতুন কাজ যোগ করুন'),
        content: TextField(
          controller: titleCtrl,
          decoration: const InputDecoration(hintText: 'কাজের বিবরণ লিখুন'),
          autofocus: true,
        ),
        actions: [
          TextButton(onPressed: Get.back, child: const Text('বাতিল')),
          ElevatedButton(
            onPressed: () {
              if (titleCtrl.text.isNotEmpty) {
                controller.createTodo(title: titleCtrl.text.trim());
                Get.back();
              }
            },
            child: const Text('যোগ করুন'),
          ),
        ],
      ),
    );
  }
}

class _TodoCard extends StatelessWidget {
  final TodoEntity todo;
  final VoidCallback onToggle;
  final VoidCallback onDelete;
  final VoidCallback onTap;

  const _TodoCard({
    required this.todo,
    required this.onToggle,
    required this.onDelete,
    required this.onTap,
  });

  Color get _priorityColor {
    switch (todo.priority) {
      case TodoPriority.high: return Colors.red;
      case TodoPriority.medium: return Colors.orange;
      case TodoPriority.low: return Colors.green;
    }
  }

  @override
  Widget build(BuildContext context) {
    return Dismissible(
      key: Key(todo.id),
      direction: DismissDirection.endToStart,
      onDismissed: (_) => onDelete(),
      background: Container(
        alignment: Alignment.centerRight,
        padding: const EdgeInsets.only(right: 20),
        color: Colors.red,
        child: const Icon(Icons.delete, color: Colors.white),
      ),
      child: Card(
        margin: const EdgeInsets.only(bottom: 8),
        child: ListTile(
          onTap: onTap,
          leading: Checkbox(
            value: todo.isCompleted,
            onChanged: (_) => onToggle(),
            activeColor: Colors.green,
          ),
          title: Text(
            todo.title,
            style: TextStyle(
              decoration: todo.isCompleted ? TextDecoration.lineThrough : null,
              color: todo.isCompleted ? Colors.grey : null,
            ),
          ),
          subtitle: todo.isOverdue
              ? const Text('মেয়াদ পেরিয়ে গেছে',
                  style: TextStyle(color: Colors.red, fontSize: 12))
              : null,
          trailing: Row(
            mainAxisSize: MainAxisSize.min,
            children: [
              Container(
                width: 8, height: 8,
                decoration: BoxDecoration(
                  color: _priorityColor,
                  shape: BoxShape.circle,
                ),
              ),
              const SizedBox(width: 8),
              const Icon(Icons.chevron_right, color: Colors.grey),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## ২৮. Best Practices ও সাধারণ ভুল

### ✅ Best Practices

```dart
// ১. Controller-এ Use Case ব্যবহার করুন, Repository নয়
// ✅ সঠিক
class UserController extends GetxController {
  final GetUserUseCase getUserUseCase;  // Use Case
  UserController({required this.getUserUseCase});
}

// ❌ ভুল
class UserController extends GetxController {
  final UserRepository repository;  // Repository সরাসরি নয়
}


// ২. Entity immutable রাখুন — copyWith ব্যবহার করুন
// ✅ সঠিক
final updated = user.copyWith(name: 'নতুন নাম');

// ❌ ভুল
user.name = 'নতুন নাম';  // mutation


// ৩. Binding-এ lazyPut ব্যবহার করুন
// ✅ সঠিক — প্রয়োজনে তৈরি হয়
Get.lazyPut(() => ProductController(...));

// ❌ এড়িয়ে চলুন — সাথে সাথে তৈরি হয়
Get.put(ProductController(...));


// ৪. View শুধু দেখাবে — logic Controller-এ
// ✅ সঠিক
Obx(() => Text(controller.productCount.toString()))

// ❌ ভুল — View-এ calculation
Obx(() => Text(controller.products.where((p) => p.isActive).length.toString()))


// ৫. Error handling সব স্তরে
// Data Layer — Exception throw করুন
throw ServerException(message: 'API ব্যর্থ');

// Repository — Exception → Failure রূপান্তর
try { ... } on ServerException catch (e) {
  return Left(ServerFailure(e.message));
}

// Controller — Failure → User message
result.fold(
  (failure) => _errorMessage.value = _mapFailureToMessage(failure),
  (data) => _handleSuccess(data),
);


// ৬. Disposal — Controller মুছলে সব cleanup করুন
@override
void onClose() {
  _textController.dispose();
  _timer?.cancel();
  _subscription?.cancel();
  super.onClose();
}


// ৭. Global service — permanent: true
Get.put<ApiClient>(ApiClient(), permanent: true);

// Feature-specific — permanent ছাড়া (screen বন্ধে মুছবে)
Get.lazyPut(() => ProductController(...));
```

### ❌ সাধারণ ভুল

```dart
// ভুল ১ — Controller-এ সরাসরি UI code
class ProductController extends GetxController {
  // ❌ ভুল — Controller-এ BuildContext ব্যবহার
  void showError(BuildContext context) {
    ScaffoldMessenger.of(context).showSnackBar(...);
  }

  // ✅ সঠিক — GetX দিয়ে
  void showError(String msg) {
    Get.snackbar('সমস্যা', msg);
  }
}


// ভুল ২ — Binding ছাড়া Controller ব্যবহার
// ❌ View-এ সরাসরি Get.put
class ProductView extends StatelessWidget {
  ProductView() {
    Get.put(ProductController()); // ভুল জায়গায়
  }
}

// ✅ সঠিক — Binding-এ
class ProductBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut(() => ProductController(...));
  }
}


// ভুল ৩ — setState এবং Obx মিশানো
// GetX Controller-এ setState() ব্যবহার করবেন না
// GetView-এ StatefulWidget মিশাবেন না


// ভুল ৪ — Model-এ business logic
// ❌ ভুল
class ProductModel {
  bool get shouldDiscount => price > 1000 && stock > 100; // Business logic
}

// ✅ সঠিক — Entity-তে বা Use Case-এ
class ProductEntity {
  bool get shouldDiscount => price > 1000 && stock > 100;
}


// ভুল ৫ — Use Case skip করা
// ❌ ভুল — Controller থেকে সরাসরি Repository
final users = await repository.getUsers();

// ✅ সঠিক — Use Case দিয়ে
final result = await getUsersUseCase(const NoParams());
```

### প্রজেক্ট চেকলিস্ট

```
Domain Layer চেক:
□ Entity — শুধু Dart, কোনো package নেই
□ Repository — abstract class, Future<Either<Failure, T>>
□ Use Case — একটি কাজ, params class আলাদা
□ UseCase base class implement করা হয়েছে

Data Layer চেক:
□ Model — Entity extend করে, fromJson/toJson আছে
□ Remote DataSource — abstract + impl, Exception throw করে
□ Local DataSource — abstract + impl, cache করে
□ Repository Impl — Exception → Failure, network check করে

Presentation Layer চেক:
□ Controller — Use Case ব্যবহার করে, GetxController extend করে
□ Binding — lazyPut ব্যবহার করে, সব নির্ভরতা আছে
□ View — GetView extend করে, শুধু দেখায়, Obx ব্যবহার করে

Routes চেক:
□ AppRoutes — সব constant
□ AppPages — সব route + binding + middleware

Testing চেক:
□ Use Case test — Mock Repository দিয়ে
□ Controller test — Mock Use Case দিয়ে
□ Repository test — Mock DataSource দিয়ে
```

---

## রিসোর্সসমূহ

- **GetX GitHub:** https://github.com/jonataslaw/getx
- **GetX Documentation:** https://github.com/jonataslaw/getx/blob/master/README.md
- **Clean Architecture (Uncle Bob):** https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- **Dartz Package:** https://pub.dev/packages/dartz
- **Flutter Test Documentation:** https://docs.flutter.dev/testing

---

> **মনে রাখুন:** Clean Architecture প্রথমে জটিল মনে হয়, কিন্তু একবার অভ্যাস হলে এটিই সবচেয়ে সহজ ও রক্ষণাবেক্ষণযোগ্য কোড কাঠামো। ছোট প্রজেক্টে এটি অতিরিক্ত মনে হলেও বড় প্রজেক্টে এটি অপরিহার্য। GetX-এর সাথে Clean Architecture মিলে একটি শক্তিশালী, দ্রুত ও পরীক্ষাযোগ্য Flutter অ্যাপ তৈরির সেরা পদ্ধতি।
