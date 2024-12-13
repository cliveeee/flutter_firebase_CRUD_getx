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

## **Book Controller**

### **Controller FirstCode**

```dart

class BookController extends GetxController {
  final FirebaseFirestore db = FirebaseFirestore.instance;

  RxList<BookModel> bookData = RxList<BookModel>();

  final TextEditingController title = TextEditingController();
  final TextEditingController des = TextEditingController();
  final TextEditingController auth = TextEditingController();
  final TextEditingController price = TextEditingController();

  @override
  void onInit() {
    super.onInit();
    getAllBooks();
  }
}
```

---

### **CREATE Book**

```dart

void createBook() async {
  try {
    var newBook = BookModel(
      title: title.text,
      description: des.text,
      author: auth.text,
      price: int.parse(price.text),
    );

    await db.collection("Books").add(newBook.toJson());

    title.clear();
    des.clear();
    auth.clear();
    price.clear();

    Get.snackbar("Success", "Book added to the database");
  } catch (e) {
    Get.snackbar("Error", "Failed to add book: $e");
  }
}
```

---

### **READ Book**

```dart

void getAllBooks() async {
  try {
    bookData.clear();
    var books = await db.collection("Books").get();
    for (var book in books.docs) {
      bookData.add(BookModel.fromJson(book.data()));
    }
  } catch (e) {
    Get.snackbar("Error", "Failed to fetch books: $e");
  }
} 

```

---

### **UPDATE Book**

```dart

void updateBook(String bookId) async {
  try {
    var updatedBook = BookModel(
      title: title.text,
      description: description.text,
      author: author.text,
      price: int.parse(price.text),
    );

    await db.collection("Books").doc(bookId).update(updatedBook.toJson());

    title.clear();
    description.clear();
    author.clear();
    price.clear();

    Get.snackbar("Success", "Book updated successfully");
  } catch (e) {
    Get.snackbar("Error", "Failed to update book: $e");
  }
}

```

---

### **DELETE Book**

```dart

void deleteBook(String bookId) async {
  try {
    await db.collection("Books").doc(bookId).delete();
    Get.snackbar("Success", "Book deleted successfully");
  } catch (e) {
    Get.snackbar("Error", "Failed to delete book: $e");
  }
}

```

---
