## `.assign(target, source1 ... sourceN)`

> Unsuitable for merging new properties into a prototype if the merge sources contain getters
> 
> Does not throw `null` or `undefined` sources
> 
> For deep cloning, use alternatives because `Object.assign()` copies property values

- Copies all enumerable own properties from one or more *source objects* to a *target object*
- Uses `[[Get]]` and `[[Set]]` on target, so it will invoke getters and setters
- Assigns properties, versus copying and defining new properties
- Both [[Strings]] and [[Symbol]] are copied

```js
Object.assign(target)
Object.assign(target, source1)
Object.assign(target, source1, source2)
Object.assign(target, source1, source2, /* …, */ sourceN)
```

`target` - target object to apply sources’ properties to
- Is returned after it is modified
- if a primitive value is provided, it will be *converted* to an object

`source1`, … `sourceN` - The source object(s) containing the properties you want to apply

**Returns** modified target object
- In case of an error, `TypeError` is raised and `target` object is changed if any properties are added before error is raised

## `.create(proto, propertiesObject)`

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object