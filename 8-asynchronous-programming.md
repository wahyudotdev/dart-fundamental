# Asynchronous Programming

## Future
Pada dart, Future digunakan untuk melakukan operasi asynchronous. Future digunakan sebagai wrapper untuk class lain yang datanya tidak dapat tersedia langsung saat itu juga. Biasanya digunakan untuk operasi IO agar tidak memblok proses lain.
```dart
Future<String> fetchNetworkData() {
    // Simulasi delay 3 detik
    return Future.delayed(Duration(seconds: 3), () {
        return 'get network data';
    });
}

void main() {
    fetchNetworkData().then((value) => print(value));
    print('Tampilkan UI');

    // output :
    // Tampilkan UI
    // get network data
}
```
Karena Future berpotensi mengembalikan error, maka kita harus menghandle error tersebut dengan menambahkan blok catchError

```dart
Future<String> fetchNetworkData() {
  return Future.delayed(Duration(seconds: 3), () {
    throw Exception('network error');
  });
}

void main() {
  fetchNetworkData()
      .then((value) => print(value))
      .catchError((err) => print('Ada error -> $err'));
  print('Tampilkan UI');

  // output
  // Tampilkan UI
  // Ada error -> Exception: network error
}

```

## Async Await
Method pada dart pada dasarnya dibagi menjadi 2 macam, yaitu method synchronous dan method asynchronous. Method synchronous akan mem-blok eksekusi program sampai method tersebut selesai dijalankan, sedangkan method asynchronous tidak akan mem-blok eksekusi program. Ciri-ciri method asynchronous adalah adanya keyword async sebelum function blok.

```dart

void delay3s() async {
  return Future.delayed(Duration(seconds: 3), () => print('delayed 3s'));
}

void main() {
  delay3s();
  print('Finish');

  // output
  // Finish
  // delayed 3s
}

```
Pada method diatas akan menampilkan 'Finish' terlebih dahulu lalu diikuti 'delayed 3s'. Bagaimana jika kita ingin menampilkan prosesnya secara berurutan dari 'delayed 3s' -> 'Finish' ? Kita dapat menggunakan keyword await untuk menunggu eksekusi delay3s sampai selesai

```dart

// 1. Ubah void menjadi Future<void>
// karena await hanya bisa digunakan pada Future
Future<void> delay3s() async {
  return Future.delayed(Duration(seconds: 3), () => print('delayed 3s'));
}

// 2. Ubah method main menjadi async
// karena await hanya bisa digunakan di blok method async
void main() async {
  
  // 3. Tambahkan keyword await
  await delay3s();
  print('Finish');

  // output
  // Finish
  // delayed 3s
}
```

Lho kalo begitu jadi seperti synchronous lagi dong? Nah trik yang biasanya digunakan adalah menambahkan satu method lagi untuk mengeksekusi method asynchronous tadi. Misal seperti contoh dibawah

```dart
// 1. Ubah void menjadi Future<void>
// karena await hanya bisa digunakan pada Future
Future<void> delay3s() async {
  return Future.delayed(Duration(seconds: 3), () => print('delayed 3s'));
}

// 2. Buat method async baru
// dan panggil delay3s
void runAsync() async {
  await delay3s();
  print('Finish');
}

// 3. Panggil method runAsync dari method main
void main() {
  runAsync();
  print('Render UI');

  // output :
  // Render UI
  // delayed 3s
  // Finish
}

```

## Error Handling Menggunakan Try Catch pada Future
Setelah kita tahu bahwa kita dapat menunggu eksekusi sebuah method asynchronous menggunakan keyword await, lalu bagaimana jika method asynchronous yang telah dipanggil ternyata menghasilkan error? Bagaimana untuk menghandle error tersebut? Nah cara yang biasanya digunakan adalah menggunakan try catch block.
```dart
Future<void> delay3s() async {
  return Future.delayed(
      Duration(seconds: 3), () => throw Exception('Test Error'));
}

void main() async {
  try {
    await delay3s();
  } catch (e) {
    print(e);
  }

  // output :
  // Exception: Test Error
}

```

dengan menggunakan cara tersebut maka kita juga bisa memperlakukan kode asynchronous seperti synchronous, misal untuk mendapatkan data json dari network sebelum diparse menjadi object dart
```dart
import 'dart:math';


// Delay 3 detik, setelah itu akan secara acak mengembalikan
// antara Map<String, dynamic> atau Exception
Future<Map<String, dynamic>> fetchNetwork() async {
  return Future.delayed(
    Duration(seconds: 3),
    () {
      final isSuccess = Random().nextBool();
      if (isSuccess) {
        return {'city': 'bdg', 'temp': 23};
      } else {
        throw Exception('Network Error');
      }
    },
  );
}


void processData() async {
  try {
    Map<String, dynamic> data = await fetchNetwork();
    print(data);
  } catch (e) {
    print(e);
  }
}

void main() {
  processData();
  print('Render UI');

  // output
  // Render UI
  // {city: bdg, temp: 23} || Exception Network Error
}

```