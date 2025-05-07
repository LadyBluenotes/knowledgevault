---
title: Promises
date created: Tuesday, April 22nd 2025, 11:12:28 am
date modified: Tuesday, May 6th 2025, 1:56:08 pm
---

# Promises

- Represents the eventual completion (or failure) of an asynchronous operation and its resulting value
- Proxy for a value not necessarily known when the promise is created
- Allows the association of handlers with an asynchronous action's eventual success value or failure reason
  - Return values like synchronous methods: instead of immediately returning the value, the asynchronous method returns a *promise* to supply the value at some point in the future

## States

A promise is in one of these states: - `pending` - initial state, neither fulfilled nor rejected - `fulfilled` - meaning that the operation was completed successfully - `rejected` - meaning that the operation failed

- The eventual state can be either fulfilled (includes a value) or rejected (with a reason / error)
  - When either happen, associated handlers queued up by a promise's `then` method are called
- A promise is settled when _either_ fulfilled or rejected but _not pending_
- _Resolved_ - the promise is settled or "locked in" to match the eventual state of another promise and further resolving or rejecting it has **no effect**
