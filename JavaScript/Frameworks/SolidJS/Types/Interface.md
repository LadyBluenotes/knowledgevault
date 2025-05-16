## Resource

```ts
interface Unresolved {
  state: "unresolved";
  loading: false;
  error: undefined;
  latest: undefined;
  (): undefined;
}
interface Pending {
  state: "pending";
  loading: true;
  error: undefined;
  latest: undefined;
  (): undefined;
}
interface Ready<T> {
  state: "ready";
  loading: false;
  error: undefined;
  latest: T;
  (): T;
}
interface Refreshing<T> {
  state: "refreshing";
  loading: true;
  error: undefined;
  latest: T;
  (): T;
}
interface Errored {
  state: "errored";
  loading: false;
  error: any;
  latest: never;
  (): never;
}
```

## Signal

```
interface SignalOptions
```