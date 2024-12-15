# Dart Notes

## Introduktion til Dart
Dart er et moderne, objektorienteret programmeringssprog udviklet af Google. Det bruges ofte til at udvikle mobil-, desktop-, backend- og webapplikationer. Det er også sproget bag Flutter, en populær framework til mobil-appudvikling.

### Hvorfor vælge Dart?
- **Hurtig udvikling:** Hot reload og kompileringsmuligheder.
- **Multi-platform:** Kode én gang og deploy på flere platforme.
- **Let at lære:** Simpelt og intuitivt sprog.

---

## Kom godt i gang
### Installation
1. Download og installer [Dart SDK](https://dart.dev/get-dart).
2. Valgfrit: Installer en editor som VS Code eller Android Studio.

### Kørsel af Dart-kode
- Brug `dart run` til at køre en Dart-fil.
- Brug `dart create` til at oprette et nyt projekt.

---

## Grundlæggende syntaks
### Hello World
```dart
void main() {
  print('Hello, World!');
}
```

### Variabler
Dart er et **statisk typet sprog**, men kan også bruge **type inference**:
```dart
void main() {
  var name = 'John'; // Type inference (String)
  int age = 30; // Statiske typer
  double height = 5.9;
  bool isDeveloper = true;

  print('Name: $name, Age: $age, Height: $height, Developer: $isDeveloper');
}
```

### Funktioner
```dart
int add(int a, int b) {
  return a + b;
}

void main() {
  print(add(2, 3));
}
```

### Control Flow (Hvis-Sætninger og Løkker)
#### If/Else
```dart
void main() {
  int score = 85;

  if (score >= 90) {
    print('A');
  } else if (score >= 75) {
    print('B');
  } else {
    print('C');
  }
}
```

#### For-løkke
```dart
void main() {
  for (int i = 0; i < 5; i++) {
    print('Tallet er $i');
  }
}
```

---

## Klasser og Objekter
### En simpel klasse
```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  void sayHello() {
    print('Hello, my name is $name, and I am $age years old.');
  }
}

void main() {
  var person = Person('Alice', 25);
  person.sayHello();
}
```

### Arv
```dart
class Animal {
  void eat() {
    print('This animal eats food.');
  }
}

class Dog extends Animal {
  void bark() {
    print('Woof! Woof!');
  }
}

void main() {
  var dog = Dog();
  dog.eat();
  dog.bark();
}
```

---

## Asynkron Programmering
Dart understøtter **async** og **await** til håndtering af asynkrone operationer:

```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return 'Data hentet';
}

void main() async {
  print('Henter data...');
  String data = await fetchData();
  print(data);
}
```

---

## Fejlhåndtering
Brug **try-catch** til at håndtere fejl:
```dart
void main() {
  try {
    int result = 10 ~/ 0; // Dividering med nul
    print(result);
  } catch (e) {
    print('En fejl opstod: $e');
  } finally {
    print('Udfører cleanup her.');
  }
}
```

---

## Ressourcer til videre læring
- [Dart's officielle dokumentation](https://dart.dev)
- [DartPad - Online editor](https://dartpad.dev)
- [Flutter udvikling](https://flutter.dev)
