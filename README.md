# ramda-playground
A place to play with all kinds of ramda tricks

```
const event = {
  "id": 86850,
  "name": "Test event",
  "sellingTickets": true,
  "client": {
    "id": 3145,
    "encryptedId": "yaxIInm",
    "__typename": "Client"
  },
  "artists": {
    "items": [
      {
        "id": 838,
        "name": "2manydjs",
        "__typename": "Artist"
      },
      {
        "id": 24,
        "name": "Bob Evans",
        "__typename": "Artist"
      },
      {
        "id": 6369,
        "name": "The Elton Jack show",
        "__typename": "Artist"
      },
      {
        "id": 2744,
        "name": "Ampere Quartet",
        "__typename": "Artist"
      }
    ],
    "__typename": "ArtistConnection"
  },
  "__typename": "Event"
}
```

```
let removeAttribute = (object, nameOfAttribute) => {
  const newObject = { ...object }
  delete newObject[nameOfAttribute];
  return newObject;
}
```

```
removeAttribute(event, '__typename')
```

```
removeAttribute = (nameOfAttribute) => (object) => {
  const newObject = { ...object }
  delete newObject[nameOfAttribute];
  return newObject;
}
```

```
removeAttribute('__typename')(event)
```

```
let addAttribute = (nameOfAttribute, value) => (object) => {
  const newObject = { ...object, [nameOfAttribute]:value }
  return newObject;
}
```

```
addAttribute('mynewatt', 1234)(event)
```

```
const doEverything = R.pipe(
  addAttribute('mynewatt', 1234),
)()
```

```
undefined
let doErrrthing = R.pipe(
  addAttribute('mynewatt', 1235675674),
  addAttribute('myneweratt', 1234534),
  addAttribute('mynewereratt', 12234534),
  addAttribute('mynewestatt', 2345),
  removeAttribute('__typename'),
)(event);
```

```
let doErrrthing = R.pipe(
  addAttribute('mynewatt', 1235675674),
  addAttribute('myneweratt', 1234534),
  addAttribute('mynewereratt', 12234534),
  addAttribute('mynewestatt', 2345),
  removeAttribute('__typename'),
)
```

```
doErrrthing = R.pipe(
  addAttribute('mynewatt', 1235675674),
  addAttribute('myneweratt', 1234534),
  addAttribute('mynewereratt', 12234534),
  addAttribute('mynewestatt', 2345),
  removeAttribute('__typename'),
)
```

```
doErrrthing(event)
```

```
R.assoc('newAtt', 'newValue')(event)
```

```
R.pipe(
  R.assoc('mynewatt', 1235675674),
  R.assoc('myneweratt', 1234534),
  R.assoc('mynewereratt', 12234534),
  R.assoc('mynewestatt', 2345),
  R.dissoc('__typename'),
)(event)
```

```
R.pipe(
  R.prop('ticketTypes')
)(event)
```

```
R.pipe(
  R.prop('artists')
)(event)
```

```
R.pipe(
  R.prop('artists'),
  R.prop('items'),
)(event)
```

```
R.pipe(
  R.path(['ticketTypes', 'items']),
)(event)
```

```
R.pipe(
  R.path(['artists', 'items']),
)(event)
```

```
R.pipe(
  R.path(['artists', 'items', 0]),
)(event)
```

```
R.pipe(
  R.path(['artists', 'items']),
)(event)
```

```
R.pipe(
  R.path(['artists', 'items']),
  R.map(R.prop('id'))
)(event)
```

```
const mapToIds = R.map(R.prop('id'))
```

```
R.pipe(
  R.path(['artists', 'items']),
  mapToIds,
)(event)
```

```
R.pipe(
  R.assoc('mynewatt', 1235675674),
  R.assoc('myneweratt', 1234534),
  R.over(R.lensPath(['artists', 'items']), () => 1234),
  R.assoc('mynewereratt', 12234534),
  R.assoc('mynewestatt', 2345),
  R.dissoc('__typename'),
)(event)
```

```
R.pipe(
  R.assoc('mynewatt', 1235675674),
  R.assoc('myneweratt', 1234534),
  R.over(R.lensPath(['artists', 'items']), R.pipe(
    R.map(R.prop('id'))
  )),
  R.assoc('mynewereratt', 12234534),
  R.assoc('mynewestatt', 2345),
  R.dissoc('__typename'),
)(event)
```

```
R.pipe(
  R.assoc('mynewatt', 1235675674),
  R.assoc('myneweratt', 1234534),
  R.over(R.lensPath(['artists', 'items']), R.pipe(
    R.sort(R.ascend(R.prop('id')))
    R.map(R.prop('id')),
  )),
  R.assoc('mynewereratt', 12234534),
  R.assoc('mynewestatt', 2345),
  R.dissoc('__typename'),
)(event)
```

```
R.pipe(
  R.assoc('mynewatt', 1235675674),
  R.assoc('myneweratt', 1234534),
  R.over(R.lensPath(['artists', 'items']), R.pipe(
    R.sort(R.ascend(R.prop('id'))),
    R.map(R.prop('id')),
  )),
  R.assoc('mynewereratt', 12234534),
  R.assoc('mynewestatt', 2345),
  R.dissoc('__typename'),
)(event)
```

```
const log = item => console.log(item) || item;
```

```
R.pipe(
  log,
  R.assoc('mynewatt', 1235675674),
  log,
  R.assoc('myneweratt', 1234534),
  log,
  R.over(R.lensPath(['artists', 'items']), R.pipe(
    R.sort(R.ascend(R.prop('id'))),
    R.map(R.prop('id')),
  )),
  log,
  R.assoc('mynewereratt', 12234534),
  log,
  R.assoc('mynewestatt', 2345),
  log,
  R.dissoc('__typename'),
)(event)
```
