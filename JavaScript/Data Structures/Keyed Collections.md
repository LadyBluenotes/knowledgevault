- Data collections that are ordered by key and not index
- associative in nature
- Map and set objects are keyed collections and are iterable in the **order of insertion**

Include:

- [Map](map.md)
- [Weak Map](Weak%20Map.md)
- [Set](Set.md)
- [Weak Set](Weak%20Set.md)

## Map vs Set

| Feature                          | Map                                                              | Set                                                    |
| -------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------ |
| **Type**                         | Collection of keyed values                                       | Collection of unique values                            |
| **Initialization**               | `new Map([iterable])` – accepts iterable of `[key, value]` pairs | `new Set([iterable])` – accepts iterable of values     |
| **Add Entry**                    | `map.set(key, value)` – adds or updates a key-value pair         | `set.add(value)` – adds a value if not already present |
| **Check Existence**              | `map.has(key)`                                                   | `set.has(value)`                                       |
| **Retrieve Value**               | `map.get(key)`                                                   | Not applicable                                         |
| **Delete Entry**                 | `map.delete(key)`                                                | `set.delete(value)`                                    |
| **Clear All**                    | `map.clear()`                                                    | `set.clear()`                                          |
| **Size**                         | `map.size`                                                       | `set.size`                                             |
| **Key/Value Constraints**        | Keys can be any type (including objects)                         | Values must be unique                                  |
| **Iteration Order**              | Insertion order preserved                                        | Insertion order preserved                              |
| **Indexed Access**               | Not directly accessible by index                                 | Not directly accessible by index                       |
| **Primary Use Case**             | Store/retrieve values by key                                     | Maintain a collection of unique values                 |
| **Advantages Over Object/Array** | More flexible key types, built-in utilities                      | Prevents duplicates, built-in utilities                |

## Weak Map vs Weak Set
