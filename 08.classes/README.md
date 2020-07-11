# Classes

## Basics
``` javascript
class Circle {
    constructor(radius) {
        // instance property
        this.radius = radius;
    }

    // prototype methods
    getArea() {
        return Math.PI * (this.radius ** 2);
    }

    getCircumference() {
        return this.circumference;
    }

    //  getters
    get area() {
        return this.getArea();
    }

    get circumference() {
        return 2 * Math.PI * this.radius;
    }

    // static method
    static double(circle) {
        return new Circle(circle.radius * 2);
    }
}
```

``` javascript
// creating a new instance
const circle = new Circle(5);

// accessing a class property
circle.radius;       // 5

// calling a method
circle.getArea();    // 78.53981633974483

// calling a getter
circle.circumference; // 31.41592653589793

// calling a static method
const doubled = Circle.double(circle);
doubled.radius    // 10
```

## Private fields
``` javascript
class Point {
    // private fields must be declared up-front
    #x = 0;
    #y = 0;

    constructor(x, y) {
        this.#x = x;
        this.#y = y;
    }

    // getters
    get x() {
        return this.#x;
    }

    get y() {
        return this.#y;
    }

    // setters
    set x(val) {
        return this.#x = val;
    }

    set y(val) {
        return this.#y = val;
    }
}
```

``` javascript
const point = new Point(2, 3);
point.#x;    // Uncaught SyntaxError: Private field '#x' must be declared in an enclosing class
point.x;     // valid since using the getter
point.x = 5; // valid since using the setter
```

## Inheritance
``` javascript
class Animal {
    constructor(name, sound) {
        this.name = name;
        this.sound = sound;
    }

    makeSound() {
        console.log(`${this.name} goes ${this.sound}.`);
    }
}
```

``` javascript
class Dog extends Animal {
    constructor(name) {
        super(name, 'woof');
    }
}
```

``` javascript
const dog = new Dog('Angel');
dog.makeSound(); // Angel goes woof.
```
