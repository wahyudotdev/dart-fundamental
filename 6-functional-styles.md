# Functional Styles

## Anonymous Function
### Introduction
dart support fungsi tanpa nama, misal
```dart

void main() {
    (){
        print('hello mom');
    }();

    // output: hello mom
}
```
### Disimpan dalam variabel
fungsi tersebut dapat pula disimpan didalam sebuah variabel
```dart
void main() {
    var helloMom = () {
        print('hello mom');
    };

    helloMom(); // hello mom
}
```
### Tipe data function
atau secara eksplisit dengan menggunakan tipe data 'Function'
```dart

void main() {
    Function helloMom = () {
        print('hello mom');
    };

    helloMom(); // hello mom
}

```
### Passing variabel
atau dapat juga kita pass variable didalamnya
```dart
void main() {
    Function(String name) greet = (name) {
        print('hello $name');
    };

    greet('crocodic'); // hello crocodic
}
```

### Return value
return value juga bisa
```dart
Function(String name) greet = (name) {
    return 'hello $name';
};

print(greet('crocodic')); // hello crocodic
```

## Menggunakan Fungsi Sebagai Parameter (Higher Order Function)

```dart


void greet(Function fn) => fn();

void callback(Function(String) fn) => fn('Callback nih');

void main() {
  greet(() => print('Hello')); // Hello

  callback((data) => print(data)); // Callback nih
}


```