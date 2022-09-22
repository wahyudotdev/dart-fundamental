# Control Flow

## If Else

```dart
int role = 1;

if(role == 1) {
    print('admin');
} else if (role == 2) {
    print('user');
} else {
    print('unknown');
}

```


## For Loops
```dart
for (int i = 1; i <= 100; i++) {
  print(i);
}
```

## While
```dart
var i = 1;
 
while (i <= 100) {
  print(i);
  i++;
}
```

## Do while
```dart
do {
  print(i);
  i++;
} while (i <= 100);
```


## Break
```dart

for(var i = 0; i <= 5; i++){
    if(i == 4) {
        print('finish');
        break;
    }
    print(i);
}
// 0
// 1
// 2
// 3
// finish
```

## Continue
```dart
for(var i = 0; i <= 5; i++){
    if(i == 4){
        print('finish');
        continue;
    }
    print(i);
}
// 0
// 1
// 2
// 3
// finish
// 5
```

## Switch Case
```dart

int role = 1;

switch(role){
    case 1:
        print('Admin');
        break;
    case 2:
        print('Driver');
        break;
    case 3:
        print('Customer');
        break;
    default:
        print('Unknown role');
        break;
}

// Admin

```