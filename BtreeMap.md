


# BTreeMap

The `BTreeMap` is a stable map based on a B-tree, implemented in the `ic_stable_structures` crate for the Internet Computer. It follows the algorithm outlined in "Introduction to Algorithms" by Cormen et al.

## Table of Contents

- [Overview](#overview)
- [Struct Definition](#struct-definition)
- [Methods](#methods)
  - [`init`](#init)
  - [`new`](#new)
  - [`load`](#load)
  - [`insert`](#insert)
  - [`get`](#get)
  - [`contains_key`](#contains_key)
  - [`is_empty`](#is_empty)
  - [`len`](#len)
  - [`into_memory`](#into_memory)
  - [`clear`](#clear)
  - [`first_key_value`](#first_key_value)
  - [`last_key_value`](#last_key_value)
  - [`remove`](#remove)
  - [`pop_last`](#pop_last)
  - [`pop_first`](#pop_first)
  - [`iter`](#iter)
  - [`range`](#range)
  - [`iter_upper_bound`](#iter_upper_bound)

## Overview

The `BTreeMap` is a data structure that provides stable mapping functionality based on a B-tree. It is designed for use in the Internet Computer environment and follows the outlined algorithm from a well-known algorithms textbook.

## Struct Definition

```rust
pub struct BTreeMap<K, V, M>
where
    K: Storable + Ord + Clone,
    V: Storable,
    M: Memory,
{
    /* private fields */
}
```

- `K`: Key type that must implement the `Storable`, `Ord`, and `Clone` traits.
- `V`: Value type that must implement the `Storable` trait.
- `M`: Memory type that must implement the `Memory` trait.

## Methods

### `init`

```rust
pub fn init(memory: M) -> Self
```

Initializes a BTreeMap. If the provided memory already contains a BTreeMap, it is loaded. Otherwise, a new instance is created.

### `new`

```rust
pub fn new(memory: M) -> Self
```

Creates a new instance of a BTreeMap. Assumes that the provided memory is exclusively reserved for this data structure.

### `load`

```rust
pub fn load(memory: M) -> Self
```

Loads an existing BTreeMap from memory.

### `insert`

```rust
pub fn insert(&mut self, key: K, value: V) -> Option<V>
```

Inserts a key-value pair into the map. Returns the previous value of the key if present.

**PRECONDITION:**
- Key is bounded in size: `key.to_bytes().len() <= max_size(Key)`
- Value is bounded in size: `value.to_bytes().len() <= max_size(Value)`

### `get`

```rust
pub fn get(&self, key: &K) -> Option<V>
```

Returns the value associated with the given key if it exists.

### `contains_key`

```rust
pub fn contains_key(&self, key: &K) -> bool
```

Returns true if the key exists in the map, false otherwise.

### `is_empty`

```rust
pub fn is_empty(&self) -> bool
```

Returns true if the map contains no elements.

### `len`

```rust
pub fn len(&self) -> u64
```

Returns the number of elements in the map.

### `into_memory`

```rust
pub fn into_memory(self) -> M
```

Returns the underlying memory.

### `clear`

```rust
pub fn clear(self) -> Self
```

Removes all elements from the map.

### `first_key_value`

```rust
pub fn first_key_value(&self) -> Option<(K, V)>
```

Returns the first key-value pair in the map. The key in this pair is the minimum key in the map.

### `last_key_value`

```rust
pub fn last_key_value(&self) -> Option<(K, V)>
```

Returns the last key-value pair in the map. The key in this pair is the maximum key in the map.

### `remove`

```rust
pub fn remove(&mut self, key: &K) -> Option<V>
```

Removes a key from the map, returning the previous value at the key if it exists.

### `pop_last`

```rust
pub fn pop_last(&mut self) -> Option<(K, V)>
```

Removes and returns the last element in the map. The key of this element is the maximum key that was in the map.

### `pop_first`

```rust
pub fn pop_first(&mut self) -> Option<(K, V)>
```

Removes and returns the first element in the map. The key of this element is the minimum key that was in the map.

### `iter`

```rust
pub fn iter(&self) -> Iter<'_, K, V, M>
```

Returns an iterator over the entries of the map, sorted by key.

### `range`

```rust
pub fn range(&self, key_range: impl RangeBounds<K>) -> Iter<'_, K, V, M>
```

Returns an iterator over the entries in the map where keys belong to the specified range.

### `iter_upper_bound`

```rust
pub fn iter_upper_bound(&self, bound: &K) -> Iter<'_, K, V, M>
```

Returns an iterator pointing to the first element below the given bound. Returns an empty iterator if there are no keys below the given bound.

## Auto Trait Implementations

- `RefUnwindSafe`, `Send`, `Sync`, `Unpin`, and `UnwindSafe` traits are implemented for `BTreeMap` with appropriate bounds for its generic types.

## Blanket Implementations

Several blanket implementations for common traits such as `Any`, `Borrow`, `BorrowMut`, `From`, `Into`, `TryFrom`, and `TryInto` are provided.

