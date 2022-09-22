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
```dart

abstract class Animal {
  void move(){
    print('walking');
  }
}

class Cat extends Animal {}

class Duck extends Animal {

    @override
    void move() {
        print('duck walking');
    }
}


// Jika menggunakan 'implements' maka wajib untuk
// membuat implementasi di child class, meskipun di parent 
// abstract class sudah ada implementasinya
class Bird implements Animal {

    @override
    void move() {
        print('bird flying');
    }

}

void main() {
    var cat = Cat();
    var duck = Duck();

    cat.move(); // walking
    duck.move(); // duck walking
}
```

## Mixin
### Contoh kasus :
Seorang programmer harus memiliki skill laravel untuk menjadi backend engineer, sedangkan untuk menjadi frontend dev harus memiliki skill react. Kita anggap 'mixin' ini adalah skill yang wajib dimiliki programmer agar dapat diterima kerja sebagai backend/frontend engineer
- Parent class : Programmer
- Mixin : laravel, react

```dart

abstract class Programmer {
    void ngoding();
}

mixin Laravel {
    void buildRestApi();
}

mixin React {
    void buildUI();
}

// Dapat diterima kerja jika memiliki skill React
void seleksiFrontend(React dev) {
    dev.buildUI();
}

// Dapat diterima kerja jika memiliki skill Laravel
void seleksiBackend(Laravel dev) {
    dev.buildRestApi();
}

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