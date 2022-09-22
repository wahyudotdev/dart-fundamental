# Fundamental

## Data Type

- Number (num, int, double)
- Boolean
- String


```dart
int counter = 0; // number

String name = 'crocodic'; // String

bool isActive = false; // Boolean
```

## Type inference

- var (re-assignable value)
- final (assign once at runtime)
- const (assign once at compile time)

```dart
int a = 1000;
var b = 1000;
final c = 1000;
const d = 1000;

print(a.runtimeType); // int
print(b.runtimeType); // int
print(c.runtimeType); // int
print(d.runtimeType); // int
```

## Collection

- Lists : array of data
- Sets : array of data, but can't have same value
- Map : key value pair

```dart

List<String> names = ['crocodic','studio'];

Set<int> evenNum = {2,4,6,8};

Map<String, double> cityTemperature = {'smg':33, 'bdg':29};

print(cityTemperature['smg']); // 33
```


## Aritmetic Operators

| Operator    | Description   |
| ----------- | ----------- |
| +           | Add |
| -           | Substract |
| *           | Multiply   |
| /           | Division   |
| ~/          | Division(int)   |
| %           | Modulo      |


## Comparation Operators

| Operator    | Description   |
| ----------- | ----------- |
| ==           | Is Equal |
| !=           | Is Not Equal |
| >           | Greater than   |
| <           | Less than   |
| >=          | Greater or equal than  |
| <=           | Less or equal than      |


## Logical Operators

| Operator    | Description   |
| ----------- | ----------- |
| \|\|           | OR         |
| &&           | AND |
| !          | NOT   |


## Function

```dart

// Without param & return value
void helloMom(){
    print('Hello mom');
}

// With param, without return value
void sebutNamakuTuan(String name) {
    print('hello $name');
}

// Without param, with return value
int whatYearIsIt() {
    final year = DateTime.now().year;
    return year;
}

// With param, with return value
String sebutNamaDoiDalamDoa(String doi){
    return 'jika $doi jodohku maka dekatkanlah';
}

// named param
double hasilKali({required double a, required double b}){
    return a * b;
}

// one liner
double multiply({required double a, required double b}) => a * b;

void main(){
    helloMom(); // Hello mom
    sebutNamakuTuan('crocodic'); // hello crocodic
    whatYearIsIt(); // 2022
    final doa = sebutNamaDoiDalamDoa('maudy ayunda');
    print(doa); // jika maudy ayunda jodohku maka dekatkanlah

    final ab = hasilKali(a: 10, b: 100);
    print(ab); // 1000

    final ab2 = multiply(a: 100, b: 100);
    print(ab2); // 10000
}
```