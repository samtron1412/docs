# Overview

- https://stedolan.github.io/jq/
- `jq` is like `sed` for JSON data - you can use it to slice and filter
  and map and transform structured data with the same ease that `sed`,
  `awk`, `grep` and friends let you play with text.
- Manual
    + https://stedolan.github.io/jq/manual
    + Use `cat file.json | jq '. | tostring'` to convert a JSON to a
      string.
