# Object Oriented

## Class
```dart
class Animal {

    // property
    final String species;
    final String name;
    final int lifeSpan;

    // constructor
    Animal({
        required this.species,
        required this.name,
        required this.lifeSpan,
    });


    // method
    void talking() {
        print('I\'m $name ($species). Please be my side for $lifeSpan years');
    }
}


void main() {
    var cat = Animal(species: 'felis catus', name: 'kucing ori', lifeSpan: 12);
    print(cat); // Instance of 'Animal'
    print(cat.species); // felis catus
    print(cat.name); // kucing ori
    print(cat.age); // 12
    cat.talking(); // I'm kucing ori (felis catus). Please be my side for 12 years
}
```

## Getter dan Setter
```dart
class Animal {
    String _name = '';
    set setName(String name) => _name = name;
    String get name => _name;
}

void main() {
    var animal = Animal();
    animal.setName = 'Kucing';
    print(animal.name); // Kucing
}
```


## Abstract Class
Semua class di dart sebenarnya dapat digunakan sebagai parent class untuk class lainnya. 
```dart
class Animal {
    void move() {
        print('walking');
    }
}

// print('walking')
class Cat extends Animal {}

// print('duck walking')
class Duck implements Animal {
    @override
    void move() {
        print('duck walking');
    }
}
```


Namun terkadang kita hanya membutuhkan blueprintnya saja tanpa menuliskan implementasinya, maka dari itu ada yang dinamakan abstract class untuk secara eksplisit menyebutkan bahwa class tersebut dapat hanya merupakan blueprint, dan child class harus menerapkan implementasi dari class tersebut
```dart

abstract class Animal {
  void move(){
    print('walking');
  }

  // method ini hanya merupakan blueprint
  // tanpa implementasi
  void eat();
}


// method void eat() wajib diimplementasikan karena
// tidak ada implementasi defaultnya di abstract class 'Animal'
class Cat extends Animal {

    @override
    void eat() {
        print('cat eats');
    }

}

// Method move akan di 'override' (ditimpa) oleh
// implementasi baru dari class 'Duck'
class Duck extends Animal {

    @override
    void move() {
        print('duck walking');
    }

    @override
    void eat() {
        print('duck eats');
    }
}


// Jika menggunakan 'implements' maka wajib untuk
// membuat implementasi semua member parent class 
// di child class, meskipun method void move()
// di abstract class 'Animal' sudah ada implementasinya
class Bird implements Animal {

    @override
    void move() {
        print('bird flying');
    }

    @override
    void eat() {
        print('bird eats');
    }
}

void main() {
    var cat = Cat();
    var duck = Duck();

    cat.move(); // walking
    duck.move(); // duck walking
}
```

dapat juga menggunakan extends dan implements secara bersamaan
```dart
abstract class Animal {
    void move();
}

abstract class Bird {
    void fly();
}

class Kenari extends Animal implements Bird {

    @override
    void move() {
        print('kenari move');
    }

    @override
    void fly(){
        print('kenari fly');
    }
}

```
## Mixin
### Untuk Apa?
Untuk menggunakan blueprint method dan property tanpa extends dari parent class, juga berguna untuk penerapan prinsip 'composition over inheritance'. Lho kenapa tidak memakai implements? Keunikannya kita bisa menggunakan lebih dari 1 mixin.
### Contoh kasus :
Seorang programmer harus memiliki skill laravel untuk menjadi backend engineer, sedangkan untuk menjadi frontend dev harus memiliki skill react. Kita anggap 'mixin' ini adalah skill yang wajib dimiliki programmer agar dapat diterima kerja sebagai backend/frontend engineer
- Parent class : Programmer
- Mixin : laravel, react

```dart

abstract class Programmer {
    void ngoding();
}

// keyword 'on' membatasi mixin agar hanya dapat dipakai
// oleh class yang mewarisi kelas 'Programmer'
mixin Laravel on Programmer {
    void buildRestApi();
}

mixin React on Programmer {
    void buildUI();
}

// Instance dapat diberikan sebagai parameter jika memiliki mixin React
void seleksiFrontend(React dev) {
    dev.buildUI();
}

// Instance dapat diberikan sebagai parameter jika memiliki mixin Laravel
void seleksiBackend(Laravel dev) {
    dev.buildRestApi();
}

// Mixin digunakan menggunakan keyword 'with'
class Backend extends Programmer with Laravel {
    
    @override
    void ngoding() {
        print('ngoding');
    }

    @override
    void buildRestApi() {
        print('build rest api');
    }

}

class Frontend extends Programmer with React {
    @override
    void ngoding() {
        print('ngoding');
    }

    @override
    void buildUI() {
        print('Build UI');
    }
}

// Jika menggunakan mixin lebih dari 1 dapat dipisahkan
// dengan tanda koma (,)
class Fullstack extends Programmer with Laravel, React {
    @override
    void ngoding() {
        print('ngoding');
    }

    @override
    void buildRestApi() {
        print('build rest api');
    }

    @override
    void buildUI() {
        print('Build UI');
    }
}

void main() {
    var be = Backend();
    var fe = Frontend();
    var fullstack = Fullstack();

    seleksiFrontend(fe); // ok
    seleksiFrontend(be); // compile error
    seleksiFrontend(fullstack); // ok
    
    seleksiBackend(fe); // compile error
    seleksiBackend(be); // ok
    seleksiBackend(fullstack); // ok
}
```