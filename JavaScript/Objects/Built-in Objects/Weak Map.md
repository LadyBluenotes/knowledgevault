- Only accepts **objects as keys** (not primitives).
- Keys are held **weakly**, meaning:
  - If no other references to the key exist, both the key and its value can be **garbage collected**.
- Not iterable:
  - No `keys()`, `values()`, `entries()`, or `forEach()`.
  - No `.size` property.

## Limitations

- You **cannot inspect** the contents of a `WeakMap`.
- Designed this way because:
  - Garbage collection is **non-deterministic** (timing is up to the JavaScript engine).
  - There’s no way to know if a key has been collected.
  - Keeping metadata like size would defeat the weak reference behavior.

## Use cases

**1. Storing Additional Metadata**

- Attach data to objects **owned by other code** (e.g. third-party library).
- When the object is collected, the data in `WeakMap` is also cleaned up.
- Prevents memory leaks from manually tracking data lifecycle.

2. **User Tracking Without Leaks**

- Example: tracking visit counts for users.
- With `Map`, data for "gone" users must be manually removed.
- With `WeakMap`, the data disappears automatically when the user object is no longer referenced.

2. **Caching**

- Store computed results associated with objects.
- With `Map`, you must clear the cache manually.
- With `WeakMap`, when the original object is gone, the cached result is automatically removed.
