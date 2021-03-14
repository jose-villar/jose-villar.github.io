# JavaScript

## Operators

### Equality Operators

#### Strict Equality Operator

- This type of operator considers type and value.

        let x = 1;
        console.log(x === 1);
        console.log(x !== 1);

### Loose Equality Operator

- This type of operator converts the operands if they are not the same type,
  and then checks for strict equality.

        let x = 1;
        console.log(x == 1);
        console.log(x != 1),

## Falsy And Truthy

### Falsy Values
- `undefined`
- `null`
- `0`
- `false`
- `''`
- `NaN`: returned when the evaluation of a mathematical expression is not
  a number.

### Truthy Values
- Anything that is nor falsy, is truthy.

## Strings

        const message = 'hello world';
        console.log(message.length);
        console.log(message.includes('my'));
        console.log(message.startsWith('hi'));
        console.log(message.endsWith('hi'));
        console.log(message.indexOf('world'));
        const newMessage = message.replace('world', 'jose');
        const newMessage = message.trim();
        const arr = message.split(' ');

## Dates

        const now = new Date();
        now.ISOString(); // this is the standard format commonly used in the
        //communication between client and server

## Objects

### Dot Notation

        person.name = Mary;

### Bracket Notation

        let selection = 'name';
        person[selection] = 'Mary';

### Factory Function

        function createAddress(street, number) {
          return {
            street,
            number
          };
        }
        const address = createAddress('myStreet', 1234);

### Constructor Function

        function Address(street, number) {
          this.street = street;
          this.number = number;
        }
        const address = new Address('myStreet', 1234);

### In

        if('radius' in circle)
          console.log("Circle has a radius")

## Loops

### For in

        const person = {
          name: "Jose",
          age: 24
        }

        for (let key in person)
          console.log(key)

### For of

        const colors = [ "red", "blue", "yellow" ]
        for (color of colors)
          console.log(color)


## Arrays

### Adding/Removing Elements

        const arr = [3, 4];
        // append
        arr.push(5, 6);
        // prepend
        arr.unshift(1,2)
        // add in the second index, deleting 0 elements
        arr.splice(2,0,'a', "bc")

        arr.pop(); // remove last element of the array
        arr.shift(); // remove first element of the array
        arr.splice(1,2) // remove 2 elements starting at index 1

        // clear an array
        arr.length = 0

### Combining/Extracting Arrays

        const first = [1, 2, 3];
        const second = [4, 5, 6];
        const combined = first.concat(second);
        const combined2 = [...first, ...second];

        // get a copy (shallow copy)
        const slice = combined.slice()
        const copy = [...combined];

        // get elements starting at index 2
        const slice2 = combined.slice()

        // get the elements in a range, including index 2, excluding 4
        const slice = combined.slice(2, 4);

### Looping Through an Array

        arr.forEach( number => console.log(number) );
        arr.forEach( ( number, index ) => console.log(index, number) );

### Sorting

        const arr = [{name:'b'}, {name:'a'}]
        arr.sort( (a, b) => {
          if(a.name.toUpperCase() > b.name.toUpperCase()) return 1
          if(a.name.toUpperCase() < b.name.toUpperCase()) return -1
          return 0
        } );

### Some and Every

        const arr = [1, 2];

        const allArePositive = arr.every( value => value >= 0 );
        const atLeastOneNegative = arr.some( value => value <= 0 );

### Miscellaneous

        const joinedAsString = arr.join(",");

        const parts = 'message'.split('-');

### Finding

        numbers.indexOf();
        numbers.lastIndexOf();
        numbers.includes();

        courses.find( (course) => {
          return course.name === 'a';
        } );

        courses.findIndex( (course) => {
          return course.name === 'a';
        } );

        courses.findIndex( course => course.name === 'a' );

### Filtering

        const filtered = numbers.filter( n => n >= 0 );

### Mapping

        // Note that you have to surround the curly braces with parenthesis in
        // this case because otherwise they are interpreted as a code block
        // instead of an object
        const mapped = numbers.map( n => ( {value:n} ) );

        // equivalent implementation
        const mapped = numbers.map( n => {
          return { value:n } 
        } );

### Reduce

- This method is used for reducing an array to a single value.

        const numbers = [1, -1, 2, 3];

        let sum = 0
        for(let n of numbers)
          sum += n;

        // You can accomplish the same result with the reduce method, passing
        // the initial value of the accumulator as the second argument
        numbers.reduce( (accum, current) => {
          return accum + current
        }, 0);

        // Or even simpler, with the accum initialiazing to the first value:
        numbers.reduce((accum, current) => accum + current);

        // Another example to get the max value of an array
        function max(array) {
          if(array.length == 0) return undefined;
          return array.reduce( (accum, current) => (current > accum) ? current : accum );
        }

- Splice: adds/removes items to/from an array, and returns the removed item(s).
- Find: `const course = courses.find( c => c.id === parseInt(req.params.id))`
- Push: `courses.push(course);`
- Delete:

        const index = courses.indexOf(course);
        courses.splice(index, 1);

- Integer to String: parseInt()

## Functions

- The following example shows a function with a variable number of arguments
used inside of it.

        function sum() {
          let total = 0;
          for(let value of arguments)
            total += value
          return total;
        }

        // With the rest operator that transforms the arguments into an arrray
        function sum(...args) {
          return args.reduce( (a, b) => a + b );
        }

- When using default parameters, those should be the last ones in the list.

### Getters and Setters

        const person = {
          firstName: 'Jose',
          lastName: 'Villar',
          get fullname() {
            return \`${firstname} ${lastName}\`;
          },
          set fullname(value) {
            const parts = value.split(' ');
            this.firstName = parts[0];
            this.lastName = parts[1];
          }
        }

        //Using the setter
        person.fullname = 'John Smith';

        //Using the getter
        console.log(person.fullname);

        // before ES6
        const person = {
          firstName: 'Jose',
          Object.defineProperty(this, 'fullName', {
            get: function {
              return this.firstName
            },
            set: function(value) {
              this.firstName = value
            }
          }),
        }

### Property Descriptors

        let person = { name: 'Jose' }
        Object.defineProperty(person, 'name', {
          writable: false,  // can't be modified
          enumerable: true, // shows up in Object.keys()
          configurable: false // prevents deleting this property (delete
          //person.name)
        })

### Prototype vs Instance Members

- If there are many objects of the same type, and they have the same method,
you should implement that method in its prototype so that there's a single
instance of it in the program. This way it saves memory.

        function Circle(radius) {
          this.radius = radius;
        }

        Circle.prototype.draw = function() {
          console.log("Draw")
        }

        Circle.prototype.toString = function() {
          return "Circle of radius" + this.radius
        }

        const c1 = new Circle(1);
        c1.draw();


## Classes

        class Circle {
          constructor(radius) {
            this.radius = radius;
          }

          // Instance method
          draw() {

          }

          // Static method
          static parse(str) {
            const radius = JSON.parse(str).radius;
            return new Circle(radius);
          }
        }

        const circle = Circle.parse('{ "radius": 1 }');
        const circle 2 = new Circle(2);

### Es6 Classes With Private Members, Getters and Setters

        const _items = new WeakMap();
        class Stack {
          constructor() {
            _items.set(this, []);
          }

          push(obj) {
            _items.get(this).push(obj);
          }

          pop() {
            const items = _items.get(this);
            if (items.length === 0)
              throw new Error('Stack is empty.');
            return _items.get(this).pop();
          }

          peek() {
            const items = _items.get(this)

            if (items.length === 0)
              throw new Error('Stack is empty');

            return items[items.length - 1];
          }

          get count() {
            return _items.get(this).length();
          }

        }


## Miscellaneous

- Arrow functions use the `this` value of their containing function. It is not
rebound, but inherited.
- Template strings can be nested
- `Object.keys` Only returns instance members, not prototype members. A `for
in` loop returns bothinstance and prototype members.
- You can use the `Date` object with the `getTime()` method to calculate the
time between the start and end of an operation in milliseconds.
- `this` references the object executing the current function.
- Arrow functions inherit `this` from the containing function. It's not rebound
to a new object.
- Avoid using the `var` keyword because it's function-scoped`
- Exceptions are errors when thrown.
- Use `typeof` to get the type of a variable
- Use the `delete` operator to remove a property from an object:

        const circle = {
          color: "blue"
        }
        delete circle.color;

- Primitives are copied by value, while objects are copied by reference.
- You can check if an object has a given property with:

        if('name' in person)
          console.log("yes")

- **Hoisting:** The process when the js engine moves all the function
- declarations to the top of the files. It allows to declare a function and use
- it before it is declared. Note it doesn't work with function constants.



