# to-promise-event

[![NPM version](https://img.shields.io/npm/v/to-promise-event)](https://www.npmjs.com/package/to-promise-event) [![Package size](https://img.shields.io/bundlephobia/minzip/to-promise-event)](https://bundlephobia.com/package/to-promise-event) [![Follow Hemi on X](https://img.shields.io/twitter/url?url=https%3A%2F%2Fx.com%2Fhemi_xyz&style=flat&logo=x&label=%40hemi_xyz&labelColor=%23ff6c15&color=%230a0a0a)](https://x.com/intent/follow?screen_name=hemi_xyz)

A utility package that creates PromiEvent-like objects, combining promises and event emitters for asynchronous operations.

## Installation

Install `to-promise-event` as a dependency:

```sh
npm install to-promise-event
```

## API

This package provides a single function for creating promise-event objects.

### `toPromiseEvent`

Converts a function that accepts an event emitter and returns a promise into a "promise event" object, which exposes the promise and the event emitter, both in a sync fashion.

```ts
toPromiseEvent<T>(callback: (emitter: EventEmitter<T>) => Promise<void>): {
  emitter: EventEmitter<T>;
  promise: Promise<void>;
}
```

- **callback**: `(emitter: EventEmitter<T>) => Promise<void>` — A function that receives an event emitter and returns a promise (required)

**Example:**

```ts
import { toPromiseEvent } from "to-promise-event";

const { emitter, promise } = toPromiseEvent(async (emitter) => {
  // Emit events during async operation
  emitter.emit("progress", 0.5);

  // Do some async work
  await someAsyncOperation();

  emitter.emit("complete", "done");
});

// Listen to events
emitter.on("progress", (progress) => {
  console.log(`Progress: ${progress * 100}%`);
});

emitter.on("complete", (result) => {
  console.log(`Completed: ${result}`);
});

// Await the promise
await promise;
```

## Local Setup

To install the dependencies, run:

```sh
npm install
```

To run the tests, run:

```sh
npm test
```
