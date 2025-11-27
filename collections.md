# Collections (Sets & Maps deep dive)

A compact guide to how ordered tree-based collections (TreeSet / TreeMap) and hash-based collections (HashSet / HashMap) work in Java.

## Overview
- `Collection`, `List`, `Set`, `Queue`, `Map` (note: `Map` is not a `Collection`).
- `HashSet`/`HashMap` (hash-based), `LinkedHashSet`/`LinkedHashMap` (insertion-order), `TreeSet`/`TreeMap` (sorted, tree-based).

## Collections hierarchy (schema)

```text
java.lang.Object
└─ java.util
   ├─ Collection<E> (root interface for collections)
   │  ├─ List<E> (ArrayList, LinkedList, Vector)
   │  ├─ Set<E> (HashSet, LinkedHashSet, TreeSet)
   │  └─ Queue<E> (ArrayDeque, LinkedList, PriorityQueue)
   └─ Map<K,V> (HashMap, LinkedHashMap, TreeMap, ConcurrentHashMap)
```

## HashSet / HashMap — conceptual flows

Add new element (HashMap.put)
1. Compute hash (`obj.hashCode()` or 0 for null).
2. Map to bucket index.
3. Inspect bucket — if key exists (hash+equals) replace/ignore; else insert.
4. Resize if threshold exceeded.

Find element (HashMap.get)
1. Compute hash, map to index.
2. Iterate bucket nodes comparing hash and equals.

Notes: average O(1), worst-case O(n) but mitigated by treeification to O(log n).

## TreeSet / TreeMap — conceptual flows

Add new element
1. Use Comparator or Comparable.compareTo.
2. Traverse from root left/right until insertion point.
3. Insert and rebalance (Red-Black tree rules).

Find element
1. Compare at each node and traverse left/right until found or null.

Notes: O(log n), supports range queries and ordered iteration.

## Practical tips
- Use hash-based when order doesn't matter and you need fastest average lookup.
- Use tree-based when ordering, range queries, or predictable worst-case needed.
- Implement `equals()` and `hashCode()` consistently for hash-based collections.
- Avoid mutating keys while they are used in hash-based structures.
- Null-handling: `HashMap` allows one null key; `TreeMap` with natural order does not accept null keys.

