# interfascist

Validate JavaScript objects against interfaces.

## What

You declare an interface and then you can test if given objects match it. For
example:

```javascript
var geometryInterfaces = {
  Point: {
    x: 'Number',
    y: 'Number'
  },
  Line: {
    start: 'Point',
    end: 'Point'
  }
};

var validator = new Interfascist( geometryInterfaces );
console.log( validator.validate({ x: 10, y: 5.5 }, 'Point') ); //true

## How



## Why not json-schema?

It's overwrought for simple validation - if your needs are complex it may suit
you better. It didn't suit me.