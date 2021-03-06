# interfascist

Validate JavaScript objects against interfaces

```
npm install interfascist
```

## What

You declare interfaces and then you can test if given objects match them. 

```javascript
var geometryInterfaces = {
  Point: {
    x: 'Number',
    y: 'Number'
  },
  Size: {
    width: 'Number',
    height: 'Number'
  },
  Rectangle: {
    location: 'Point',
    size: 'Size'
  },
  Color: [ 'red', 'green', 'blue' ],
  Colored: {
    fill: 'Color',
    stroke: 'Color'
  },
  ColoredRectangle: {
    extends: [ 'Rectangle', 'Colored' ]
  },
  RedRectangle: {
    extends: [ 'ColoredRectangle' ],
    values: {
      fill: 'red'
    }
  }
};

var validator = new Interfascist( geometryInterfaces );

var rect1 = {
  location: { x: 1.3, y: 13 },
  size: { width: 25, height: 96.3 },
  fill: 'red',
  stroke: 'blue'
}

var rect2 = {
  location: { x: 41, y: 26 },
  size: { width: 55.3, height: 18 }  
}

var rect3 = {
  location: { x: 1.3, y: 13 },
  size: { width: 25, height: 96.3 },
  fill: 'purple',
  stroke: 'purple'
}

console.log( validator.validate( rect1, 'Point' ) ); //false
console.log( validator.validate( rect1, 'Rectangle' ) ); //true
console.log( validator.validate( rect1, 'ColoredRectangle' ) ); //true
console.log( validator.validate( rect1, 'RedRectangle' ) ); //true
console.log( validator.validate( rect2, 'Rectangle' ) ); //true
console.log( validator.validate( rect2, 'ColoredRectangle' ) ); //false
console.log( validator.validate( rect3, 'Rectangle' ) ); //true
console.log( validator.validate( rect3, 'ColoredRectangle' ) ); //false

```

There's some more functionality, check out test/test.js until I have a chance
to write a better readme.

## Tests

Run with mocha from the root of interfascist

```
npm install -g mocha
mocha
```

## Why not json-schema?

It's overwrought for simple validation - if your needs are complex it may suit
you better. It didn't suit me.

## License

MIT
