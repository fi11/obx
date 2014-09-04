Simple inheritance helper with named constructor.

## Installation

```
$ npm install obx
```

## Example

```js
var Obj = require('obx');

// copy of object class
var Base = Obj.create();

// with named constructor "function Model() { Base.apply(this, arguments) }"
var BaseModel = Base.create('Model', {
    foo: 'bar',
    baz: 'foo'
}, {
    fn: function() { return 1 }
});

var Model = BaseModel.create(function Model() {
    BaseModel.apply(this, arguments); // super call
    // or this.__parent.apply(this, arguments);

    this.bar = 'baz';

    // self constructor
    console.log(this.__constructor.name) // >>> 'Model'
}, {
    foo: BaseModel.prototype.foo + '!',
    fn: function() {
        return this.__parent.prototype.fn() + 1;
    }

);

var model = new Model;

model.foo; // >>> 'foo!'
model.bar; // >>> 'baz'
model.baz; // >>> 'foo'
model.fn(); // >>> 2

```

## Running tests

```
$ make test
```

## Authors

  - [Pavel Silin](https://github.com/fi11)

# License

  MIT
