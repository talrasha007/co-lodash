#codash
 Extend lodash to support harmony.

## API
 - _.isGenerator(obj)
 - _.coEach(collection, fn) // fn params (item, index, collection)
 - _.coMap(collection, fn)  // fn params (item, index, collection)
 - _.coReduce(collection, fn, memo) //fn params (memo, item, index, collection)

## Example

```js
var _ = require('codash'); // yes, it can do exactly the same as lodash, because it is lodash with some extendsions.

function sleep(mill) { return function (cb) { setTimeout(cb, mill); }; }

co(function *() {
    yield* _.coEach([1,2,3,4,5], function* (v) {
        console.log('each:', v);
        yield sleep(1000);
    });

    console.log(yield* _.coMap([1,2,3,4,5], function *(v) {
        console.log('map:', v);
        yield sleep(1000);
        return v * 2;
    }));

    console.log(yield* _.coReduce([1,2,3,4,5], function*(m, v) {
        console.log('reduce:', v);
        yield sleep(1000);
        return m + v;
    }, 0));
})();
```
