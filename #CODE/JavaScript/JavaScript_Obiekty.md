# JavaScript - Obiekty

**Obiekt** - typ złożony w JavaScript służący do przechowywania danych oraz metod.

## Tworzenie obiektów

```javascript
// Notacja literałowa (literal notation)
const myObj = {
  name: "Pies",
  speed: 1000,
  print: function() {
    console.log("Lubię walczyć ze złem");
  }
};
```

```javascript
const pet = "Pies";
const speed = 1000;

// Starszy zapis
const myObj = {
    pet : pet,
    speed : speed,
    print: function() { ... }
}

// Nowy zapis
const myObj = {
    pet,
    speed,
    print() { ... }
}
```

```javascript
// Tworzenie obiektu za pomocą konstruktora
const txt = new String("Ala ma kota");
const car = new Car("BMW", "czarny");
const person = new Object({
  age: 100,
  name: Jan
});
```

```javascript
// Tworzenie obiektu za pomocą metody Object.create()
const car = {
  drive() {
    console.log("Jadę");
  },
  refuel() {
    console.log("Tankuję");
  },
  stop() {
    console.log("Zatrzymuję się");
  }
};

const c1 = Object.create(car);
c1.name = "Samochód 1";

const c2 = Object.create(car);
c2.name = "Samochód 2";
```

## Metody

**Metoda** - funkcja znajdująca się w obiekcie

```javascript
const wes = {
  name: "Westopher Bos",

  // Metoda
  sayHi: function() {
    console.log(`Hey ${this.name}`);
    return "Hey Anna";
  },

  // Skrótowy zapis metody
  yellHi() {
    console.log("HEY ANNA");
  },

  // Metoda w postaci funkcji strzałkowej
  wisperHi: () => {
    console.log("hii Anna im a mouse");
  }
};
```

## Odwoływanie się do właściwości i metod

```javascript
const ob = {
    name : "Marcin",
    pet : "pies",
    pisz : function() { ... }
}

// Notacja kropki
ob.name
ob.pet
ob.pisz()

// Nawiasy kwadratowe
ob["name"]
ob["pet"]
ob["pisz"]()
```

## Dodawanie właściwości

```javascript
const car = {
  brand: "Mercedes",
  color: "czerwony",
  speed: 150,
  print: function() {
    console.log(car.brand + " koloru " + car.color);
  }
};

car.doors = 4;
car.wheels = 4;
car.drive = function() {
  console.log("Jadę sobie żwawo!");
};

car.print();
car.drive();
```

## Usuwanie właściwości i metod

```javascript
const car = {
    brand : "Mercedes",
    color : "czerwony"
    speed : 150,
    print : function() {
        console.log(this.brand + ' koloru ' + this.color );
    }
}

console.log(car.color); // czerwony
delete car.color;
console.log(car.color); // undefined
```

## this

**this** - słowo kluczowe wskazujące na obiekt, który w danym momencie wywołał określoną metodę. Domyślnie używanym obiektem w przeglądarce jest `Window`. W JavaScript słowo kluczowe `this` Jest definiowane w miejscu gdzie funkcja (metoda) została wywołana a nie w miejscu jej definiowania

```javascript
const person = {
  name: "Wes Bos",
  sayHi() {
    console.log(this);
    console.log(`hey ${this.name}`);
    return `hey ${this.name}`;
  }
};

const sayHi = person.sayHi;
person.sayHi(); // Zwróci "hey Wes Bos"
sayHi(); // Zwróci samo "hey " bo w miejscu wywołania this wskazuje na obiekt Window
```

### that i self

Ze względu na to, że w różnych kontekstach słowo kluczowe `this` może wskazywać na różne elementy np. na przycisk, obiekt lub obiekt globalny `Window` dobrą praktyką jest stworzenie dodatkowej zmiennej, która będzie wskazywała na element do którego chcemy mieć stałe odwołanie - zazwyczaj obiekt.

```javascript
const ob = {
  name: "Marcin",
  printDelay: function() {
    const self = this; // Odwołanie wersja self
    const that = this; // Odwołanie wersja that

    setTimeout(function() {
      console.log(this); //window
      console.log(self.name); //Marcin
    }, 2000);
  }
};

ob.printDelay();
```

## Metody zmieniające kontekst `this`

### `bind()`

Instrukcja `bind(newThis, *params)` pozwala przekazać nowy kontekst dla `this`. Funkcja zwraca nam nową funkcję ze zmienionym wiązaniem `this`.

```javascript
const myFn = function() {
  console.log(this); // To nie jest metoda żadnego obiektu więc this === window
};

const myNewFn = myFn.bind({ x: 10 });
myFn(); // window
myNewFn(); // {x : 10}
```

```javascript
const ob = {
  name: "Marcin",
  printDelay: function() {
    setTimeout(
      function() {
        console.log(this); // ob
        console.log(this.name); // Marcin
      }.bind(this),
      2000
    ); // Wykorzystanie bind() do zmiany this
  }
};

ob.printDelay();
```

W wersji ES6 wprowadzono tak zwaną funkcję strzałkową, która poza krótszym zapisem, nie zmienia w swoim wnętrzu kontekstu this biorąc je z otaczającego ją środowiska.

### `call()`

Metoda `call(newThis, *params)` - dostępna dla każdej funkcji, służy do jej wywołania.

- Jako pierwszy jej parametr podajemy wartość, która zostanie podstawiona pod `this` wewnątrz wywoływanej funkcji
- Jako kolejne podajemy parametry, których wymaga wywoływana funkcja

Przy pomocy `call()` można "pożyczać" metody innych obiektów, ponieważ jako pierwszy jej parametr podajemy wartość, która zostanie podstawiona pod `this` wewnątrz wywoływanej funkcji.

```javascript
const ob = {
  name: "Marcin",
  print: function() {
    console.log("Mam na imię " + this.name);
  }
};

ob.print(); // Mam na imię Marcin

const ob2 = {
  name: "Roman"
};

ob.print.call(ob2); // Mam na imię Roman
ob.print.call({ name: "Patryk" }); // Mam na imię Patryk
```

### `apply()`

Metoda `apply(newThis, [params])`

- Jako pierwszy jej parametr podajemy wartość, która zostanie podstawiona pod `this` wewnątrz wywoływanej funkcji
- Jako drugi atrybut przyjmuje tablicę, która zawiera w sobie parametry

```javascript
const ob = {
  name: "nikt",

  print: function(pet1, pet2) {
    console.log(
      `Nazywam się ${this.name} i mam 2 zwierzaki: ${pet1} i ${pet2}`
    );
  }
};

const user = {
  name: "Marcin"
};
const tab = ["pies", "kot"];

ob.print.apply(user, tab); // Nazywam się Marcin i mam dwa zwierzaki: pies i kot
```

## Iterowanie po obiekcie

### Pętla for in

Pętla "for in" zwraca klucze danej instancji oraz z prototypu danego obiektu jeżeli dany obiekt został zbudowany na bazie konstruktora.

```javascript
const car = {
  brand: "Mercedes",
  color: "czerwony",
  speed: 150,
  print: function() {
    console.log("Marka: ", this.brand);
    console.log("Kolor: ", this.color);
    console.log("Szybkość: ", this.speed);
  }
};

for (const key in car) {
  console.log(key); // brand, color, speed, print
}
```

### Object.keys(obj)

`Object.keys()` zwraca tylko klucze danej instancji

```javascript
const car = {
  brand: "Mercedes",
  color: "czerwony",
  speed: 150
};

const keys = Object.keys(car);
for (const key of keys) {
  // Pętla po tablicy z użyciem of
  console.log(car[key]);
}
```

## Konstruktor

**Konstruktor** - funkcja, na bazie której tworzone są nowe obiekty. Dobrą praktyką jest pisanie nazw konstruktorów z wielkiej litery.

```javascript
function Car(brand, color) {
  this.age = 0;
  this.brand = brand;
  this.color = color;

  this.print = function() {
    console.log(this.brand + " koloru " + this.color);
  };
}

// Tworzymy 2 obiekty na bazie konstruktora
const car1 = new Car("Fiat", "czerwony");
car1.print(); //Fiat koloru czerwony

const car2 = new Car("BMW", "czarny");
car2.print(); //BMW koloru czarny
```

Do tej pory tworzyliśmy zmienne typu string, number, boolean, array jako literały (literał - skrócony zapis). Każdy taki typ możemy stworzyć też za pomocą odpowiednich konstruktorów:

- string możemy utworzyć poprzez `new String()`
- wartości boolowskie przez `new Boolean()`
- numery przez `new Number()`
- tablice przez `new Array()`

Metody te przydają się w nielicznych sytuacjach, a w codziennej pracy nie są raczej zalecane:

- wydłuża to zapis
- zwiększa obciążenie pamięci

```javascript
const txt = new String("Ala ma kota");
const nr = new Number(23);
const bool = new Boolean(true);
```

### new

**new** - słowo kluczowe, którego wykorzystanie przed funkcją pozwala stworzyć nową instancję obiektu tej funkcji.

```javascript
function Pizza() {
  console.log("Making a pizza");
}

const pepperoniPizza = new Pizza(); // Zwraca obiekt: Pizza {}
```

## Klasy

- Każda z klas ma konstruktor, czyli funkcję, która jest automatycznie odpalana przy tworzeniu nowej instancji za pomocą słowa kluczowego `new`
- Jeżeli chcemy jakąś klasę rozszerzyć, używamy słowa kluczowego `extends`
- Jeżeli chcemy wywołać kod z rozszerzanej klasy, zamiast sięgać po `call/apply` podobnie do języka używamy składni `super()`

```javascript
class Animal {
  constructor() {
    this.name = name;
    console.log("Tworzę zwierzę: " + this.name);
  }

  eat() {
    return this.name + " właśnie je";
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name);
    this.type = "dog";
  }
  eat() {
    const text = super.eat();
    return text + " kości";
  }
  bark() {
    return this.name + " wof! wof!";
  }
}

const dog = new Dog("Pies");
console.log(dog.eat()); //"Pies właśnie je kości";
```

## Prototyp

`__proto__` - właściwość, która wskazuje na prototyp, na którym opiera się dany obiekt. Obiekty odwołują się hierarchicznie w górę poprzez `__proto__` do kolejnych prototypów, kończąc na rodzicu wszystkich obiektów - `Object`.

- Wszystkie obiekty stworzone na bazie danego konstruktora za pomocą właściwości `__proto__` wskazują na ten sam obiekt prototyp
- Jeżeli kiedykolwiek zmienimy w tym obiekcie cokolwiek, zmieni się to dla wszystkich instancji już stworzonych i tworzonych w przyszłości na bazie tego konstruktora.

```javascript
const user = {
    // Stworzone przez programistę właściwości i metody:
    // test: "Aaa",
    // ...

    __proto__ = {...to jest prototyp obiektu...}
}
```

Jeżeli za pomocą słowa kluczowego `new` utworzymy nowy obiekt, JavaScript:

- ustawi takiemu obiektowi prototyp biorąc go z właściwości `prototype` naszego konstruktora (na ten obiekt będą wskazywać `__proto__` nowych obiektów)
- zmieni kontekst słowa `this`, które od tego momentu będzie wskazywać na daną instancję obiektu, a nie na obiekt globalny window

```javascript
function Car(brand, color) {
  this.age = 0;
  this.brand = brand;
  this.color = color;

  this.print = function() {
    console.log(this.brand + " koloru " + this.color);
  };
}

const car1 = new Car("Fiat", "czerwony");
console.log(car1.__proto__ === Car.prototype); // true
```

Dodawanie właściwości i metod do prototypu pozwala oszczędzić zasoby i pamięć ponieważ dane nie są powielane wielokrotnie.

## Dziedziczenie

Dziedziczenie w JavaScript jest oparte o prototypy.

```javascript
function Animal(name) {
  // Kontruktor Animal
  this.name = name;
  console.log("Tworzę zwierzę: " + this.name);
}

Animal.prototype.eat = function() {
  // Dodajemy metodę do prototypu
  return this.name + " właśnie je";
};

function Dog(name) {
  // Kontruktor Dog
  this.name = name;
  this.type = "dog";
}

// Tworzymy nowy obiekt prototypu na bazie innego prototypu
Dog.prototype = Object.create(Animal.prototype);
//lub
Dog.prototype = Object.assign({}, Animal.prototype);
//lub
Dog.prototype = Object.create(...Animal.prototype);

Dog.prototype.constructor = Dog; // Wskazujemy poprawny konstruktor dla Dog

Dog.prototype.bark = function() {
  return this.name + " wof! wof!";
};

const dog = new Dog("Pies");
console.log(dog.bark()); // Pies wof! wof!
console.log(dog.eat()); // Pies właśnie je;

const animal = new Animal("Pingwin");
animal.eat(); // Pingwin właśnie je
animal.bark(); // błąd, bo Animal nie ma metody bark()
```

## Sprawdzanie typu i właściwości

### instanceof

**instanceof** - Sprawdza czy dany obiekt należy do wskazanego typu. Zwraca `true/false`

```javascript
console.log(dog instanceof Dog);
console.log(dog instanceof Animal);
console.log(dog instanceof Object);
console.log(animal instanceof Animal);
console.log(animal instanceof Object);
```

### hasOwnProperty()

**hasOwnProperty()** - sprawdza czy dana instancja obiektu ma konkretną właściwość lub metodę

```javascript
const ob = {
  name: "Marcin",
  print: function() {}
};

console.log(ob.hasOwnProperty("print")); // true
console.log(ob.hasOwnProperty("name")); // true
console.log(ob.hasOwnProperty("surname")); // false
```
