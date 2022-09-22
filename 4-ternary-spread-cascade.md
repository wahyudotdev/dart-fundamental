# Ternary, Cascade, and Spread Operator

## Ternary (?)
Bentuk simple dari if else. Jika kondisi true maka nilai disebelah kiri yang akan dikembalikan, begitu pula sebaliknya.
```dart

bool isForecastRain = true;

print(isForecastRain ? 'Bring an umbrella' : 'Just go'); // Bring an umbrella

```

## Cascade Operator (..)
Di bahasa pemrograman lain mungkin kita biasanya mengembalikan 'this' untuk membuat chain method. Namun hal itu tidak diperlukan di dart karena dart memiliki fitur yang bernama cascade operator.
```dart

class Animal {
  
  String? _name;
  int? _lifeSpan;

  set setName(String n) => _name = n;  
  set setLifeSpan(int lifeSpan) => _lifeSpan = lifeSpan;
  
  String? get name => _name;
  int? get lifeSpan => _lifeSpan;

}

// Dari ini
/*
void main() {
  var cat = Animal()
  cat.setName = 'Kucing Ori'
  cat.setLifeSpan = 12;
  print(cat.name); // Kucing Ori
  print(cat.lifeSpan); // 12
}
*/

// Mnejadi seperti dibawah
void main() {
  var cat = Animal()
                ..setName = 'Kucing Ori'
                ..setLifeSpan = 12;
  print(cat.name); // Kucing Ori
  print(cat.lifeSpan); // 12
}

```

### Spread Operator
Berfungsi untuk 'menyebarkan' atau menyalin nilai sebuah array didalam array lainnya

```dart
void main() {
    var even = [2,4,6];
    
    var numbers = [1,2,3,...even];

    print(numbers); // [1,2,3,2,4,6]
}

```