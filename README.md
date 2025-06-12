 

##   Завдання 1 - Скорочена ініціалізація класу
**Задача:** Використати parameter properties для скорочення оголошення властивостей класу.

**Рішення:**
```ts
class Student {
  constructor(
    public name: string,
    public age: number,
    public grade: string
  ) {}
}
```

##   Завдання 2 - Модифікатори доступу та наслідування
**Задача:** Створити класи Employee та Manager з правильними модифікаторами доступу.

**Рішення:**
```ts
class Employee {
  constructor(
    public name: string,
    private department: string,
    protected salary: number
  ) {}

  getEmployeeDetails() {
    return `Name: ${this.name}, Department: ${this.department}, Salary: ${this.salary}`;
  }
}

class Manager extends Employee {
  constructor(
    name: string,
    department: string,
    salary: number
  ) {
    super(name, department, salary);
    this.salary += 10000;
  }
}
```

##   Завдання 3 - Інтерфейси
**Задача:** Створити інтерфейси ICharacter та ISpellCaster для класу Wizard.

**Рішення:**
```ts
interface ICharacter {
  name: string;
  level: number;
  introduce(phrase: string): void;
  levelUp(): void;
}

interface ISpellCaster {
  castSpell(): void;
}

class Wizard implements ICharacter, ISpellCaster {
  constructor(public name: string, public level: number) {
    if (this.level < 1) {
      throw new Error('Level too low');
    }
  }

  introduce(phrase: string): void {
    console.log(phrase + ', ' + this.name);
  }

  castSpell(): void {
    console.log('Casting a spell, behold my power!');
  }

  levelUp(): void {
    this.level++;
    console.log(`Level up! New level is ${this.level}`);
  }
}
```

##  Завдання 4 - Абстрактні класи та композиція
**Задача:** Реалізувати систему взаємодії між Key, Person, House та MyHouse.

**Рішення:**
```ts
class Key {
  private signature: number;

  constructor() {
    this.signature = Math.random();
  }

  getSignature(): number {
    return this.signature;
  }
}

class Person {
  constructor(private key: Key) {}

  getKey(): Key {
    return this.key;
  }
}

abstract class House {
  protected door: boolean = false;
  protected tenants: Person[] = [];

  constructor(protected key: Key) {}

  abstract openDoor(key: Key): void;

  comeIn(person: Person): void {
    if (this.door) {
      this.tenants.push(person);
      console.log('Person came in successfully');
    } else {
      console.log('Door is closed, cannot come in');
    }
  }
}

class MyHouse extends House {
  openDoor(key: Key): void {
    if (key.getSignature() === this.key.getSignature()) {
      this.door = true;
      console.log('Door opened successfully');
    } else {
      console.log('Wrong key, door remains closed');
    }
  }
}

// Використання:
const key = new Key();
const house = new MyHouse(key);
const person = new Person(key);

house.openDoor(person.getKey());
house.comeIn(person);
```

 
