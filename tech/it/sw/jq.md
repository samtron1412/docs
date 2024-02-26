# Overview

- https://stedolan.github.io/jq/
- `jq` is like `sed` for JSON data - you can use it to slice and filter
  and map and transform structured data with the same ease that `sed`,
  `awk`, `grep` and friends let you play with text.
- Manual
    + https://stedolan.github.io/jq/manual

# Common usages

+ Use `cat file.json | jq '. | tostring'` to convert a JSON to a string.

## Escaped JSON string to JSON

- Use `fromjson` builtin to transform escaped JSON string to JSON:
    * https://stedolan.github.io/jq/manual/v1.5/#Convertto/fromJSON
    * https://stackoverflow.com/questions/35154684/how-to-parse-a-json-string-with-jq-or-other-alternatives
    * `pbpaste | jq 'fromjson'`
    * Alternative: `-r` option: `pbpaste | jq -r`
    * In VIM
        - The escaped JSON has to be a string. WRAP IT INSIDE a double
          quotes: `"<escaped JSON>"`
        - `:%!jq 'fromjson'`

```
echo "{\"bar\": \"bam\"}" | jq 'fromjson'
```

## JSON to escaped JSON string

- Escaped JSON (output an escaped JSON string):
    * `jq -R -s '.' < datafile`
    * `jq @json <<< '{"Hello": "World"}'`
    * https://unix.stackexchange.com/questions/548892/how-to-json-escape-input
