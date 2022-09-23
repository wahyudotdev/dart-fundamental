# Null Safety

## Nullable type
Tipe data yang tidak bertipe nullable (?) harus memiliki nilai awal selain null

```dart
void main() {
    String name; // compile error
    String? nameNullable; // nullable type, ok
    String name = 'crocodic'; // ok

    print(nameNullable); // null
    print(name); // crocodic
}
```

## Late Keyword
Berfungsi untuk memberi tahu compiler bahwa variabel akan diinisialisasi nanti dan tidak akan bernilai null
```dart

void main() {
    late String name; // ok
    name = 'crocodic';
    print(name.length); // 8
}

```

## Null Operator
Berfungsi untuk mengembalikan nilai default ketika nilai disebelah kiri operator bernilai null
```dart
void main() {
    String? name;
    print(name ?? 'crocodic'); // crocodic

    name = 'dash';
    print(name ?? 'crocodic'); // dash
}
```

## Null Aware Assignment
Berfungsi untuk memberikan nilai default ketika variabel bernilai null. Namun jika nilainya bukan null maka nilai variabel tidak akan berubah.
```dart
void main() {
    String? name;

    name ??= 'crocodic';

    print(name); // crocodic

    name ??= 'dash';

    print(name); // crocodic
}
```

## Null Aware Invocation
Berfungsi untuk mengakses property dan method sebuah objek yang berpotensi bernilai null secara aman
```dart

void main() {
    String? name;

    print(name?.length); // null

    name = 'crocodic';

    print(name?.length); // 8
}

```

## Null Aware Spread Operator
Berfungsi untuk secara aman menyalin array nullable ke dalam array lain menggunakan spread operator

```dart

List<int>? even;

var number = [1,2,...?even]; // ok
print(number); // [1,2]


```

## Null Assertion
Jika Anda yakin bahwa nilai nullable yang diproses tidak akan bernilai null, maka Anda dapat menggunakan operator null assertion (!). **Berhati-hatilah saat menggunakan null assertion**

```dart

void main() {
    String? name;
    String? throwError;
    
    name = 'crocodic';


    print(name!.length); // 7
    print(throwError!.length); // Unhandled exception : Null check operator used on a null value
}

```