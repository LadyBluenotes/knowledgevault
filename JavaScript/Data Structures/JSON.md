- **JSON**: JavaScript Object Notation — a **text-based format** for representing **structured data**.
- Based on **JavaScript object syntax**, but language-independent.
- Used for **data transmission** in web applications (e.g., client ↔ server communication).
- Stored as a **string** and parsed into objects in code.
- **MIME type**: `application/json`.
- **File extension**: `.json`.

## Syntax rules

- All **object property names** must be in **double quotes**.
- No trailing commas in arrays or objects.
- JSON must be **strictly valid**, even minor syntax issues (like an extra comma) cause errors.
- Use JSON validators like **JSONLint** to verify correctness.

## Key concepts

- **Serialization**: Converting a JavaScript object into a JSON string using `JSON.stringify
- **Deserialization**: Converting a JSON string back into an object using `JSON.parse()`.

## JSON structure

- Looks like JavaScript object literals with **stricter syntax**.
- Can represent:
  - **Objects**
  - **Arrays**
  - **Primitives**: numbers, strings, booleans, and null

```js
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    }
  ]
}
```

## Accessing the data

- JSON must be **parsed** into an object first (if loaded as a string).
- Once parsed:
  - Use **dot notation** or **bracket notation**.

```js
superHeroes.homeTown; // "Metro City"
superHeroes.members[1].powers[2]; // "Superhuman reflexes"
```

## JSON arrays

- JSON can also start as an **array**, not just an object.

```js
[
  {
    name: "Molecule Man",
    age: 29,
    secretIdentity: "Dan Jukes",
  },
  {
    name: "Madame Uppercut",
    age: 39,
    secretIdentity: "Jane Wilson",
  },
];
```

- Can be accessed like:

```js
superHeroes[0].powers[0];
```

## Valid JSON types

| Allowed | Not Allowed                          |
| ------- | ------------------------------------ |
| Strings | undefined                            |
| Numbers | NaN                                  |
| Boolean | Infinity                             |
| null    | Functions                            |
| Objects | Date, Set, Map or other custom types |
| Arrays  | Trailing commas                      |
|         | Comments                             |

## Web API usage

- Use `fetch()` and `.json()` to retrieve JSON from APIs:

```js
fetch("data.json")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

## Converting between objects and JSON strings

Converting is needed for:

- **Receiving data**: Sometimes you get raw JSON **as a string** and must convert it to a JavaScript object.
- **Sending data**: To send a JavaScript object over the network, you must convert it to a JSON **string**.

## Built-in methods

### `JSON.parse()`

- Converts a **JSON string** to **JavaScript object**.
- Used to **read** JSON strings

```js
let obj = JSON.parse('{"name": "Chris", "age": 38}');
```

Example with `fetch()` and `JSON.parse()`

```js
async function populate() {
  const requestURL =
    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json";
  const response = await fetch(requestURL);
  const superHeroesText = await response.text(); // get raw JSON string
  const superHeroes = JSON.parse(superHeroesText); // convert to JS object
  populateHeader(superHeroes);
  populateHeroes(superHeroes);
}
```

### `JSON.stringify()`

- Converts JS object into JSON string
- Used to **send/store** JS objects as JSON strings

```js
let str = JSON.stringify({ name: "Chris", age: 38 });
```
