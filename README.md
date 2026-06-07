# lsm — LSM-tree storage engine for Zeta

**Namespace:** `@storage/lsm`

Log-structured merge-tree storage engine with Grid block allocation,
sorted B-tree table operations, level-based compaction, and manifest
metadata.

## Architecture

```
Forest
 ├── Tree 0 (accounts)
 │   ├── Level 0 (memtable + flushed tables)
 │   ├── Level 1 (compacted)
 │   ├── Level 2 (compacted)
 │   └── ...
 ├── Tree 1 (transfers)
 └── ...
Grid (fixed-size block storage)
Journal (write-ahead log)
Manifest (checkpoint metadata)
```

## Key operations

- `Tree_put(key, value)` — sorted insert into memtable
- `Tree_get(key)` — search memtable then levels
- `Tree_delete(key)` — tombstone insert
- `Tree_flush()` — persist memtable to Grid
- `binary_search(entries, count, key)` — sorted lookup
- `merge_entries(a, b, out)` — two-way merge with tombstone filtering

## License

MIT — The Zeta Foundation
