# CRUD Operations with GetX and Firebase

This document provides a complete implementation of CRUD operations using GetX and Firebase in Flutter. The coding style aligns with a simple and understandable format for students.

---

## **BookModel**

### **Model Code**
```dart

class BookModel {
  String title;
  String description;
  String author;
  int price;

  BookModel({
    required this.title,
    required this.description,
    required this.author,
    required this.price,
  });

  Map<String, dynamic> toJson() {
    return {
      'title': title,
      'description': description,
      'author': author,
      'price': price,
    };
  }

  factory BookModel.fromJson(Map<String, dynamic> json) {
    return BookModel(
      title: json['title'],
      description: json['description'],
      author: json['author'],
      price: json['price'],
    );
  }
}
```

---
