- Only stores **objects** (no primitives like strings or numbers).
- Objects are held **weakly**:
  - If no other references to the object exist, it becomes **eligible for garbage collection**.
- A `WeakSet` can only contain each object **once** (no duplicates).

## Limitations

- Only stores **objects** (no primitives like strings or numbers).
- Objects are held **weakly**:
  - If no other references to the object exist, it becomes **eligible for garbage collection**.
- A `WeakSet` can only contain each object **once** (no duplicates).

## Use cases

1. **Tracking Object Presence**

- Efficient way to check if an object has been "seen" or "processed."
- No risk of memory leaks, as objects are removed when no longer referenced elsewhere.

2. **Marking Objects Privately**

- Can act like a lightweight tag system for objects without modifying them.
- For example, mark DOM nodes as processed without altering the DOM or risking memory issues.

3.  **Object Lifecycle-Aware Collections**

- Use in systems where objects may appear and disappear dynamically (e.g., DOM elements, user sessions).
- No need to manually clean up `WeakSet`; JavaScript engine handles it.
