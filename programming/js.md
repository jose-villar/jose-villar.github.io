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


## Objects

### Dot Notation

        person.name = Mary;

### Bracket Notation

        let selection = 'name';
        person[selection] = 'Mary';

## Arrays

- Splice: adds/removes items to/from an array, and returns the removed item(s).
- Find: `const course = courses.find( c => c.id === parseInt(req.params.id))`
- Push: `courses.push(course);`
- Delete:

        const index = courses.indexOf(course);
        courses.splice(index, 1);

- Integer to String: parseInt()


