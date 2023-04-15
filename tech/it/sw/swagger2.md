# Overview

- Swagger (aka OpenAPI 2.0) is a tool that can be used to describe APIs.

# Specification

- https://swagger.io/docs/specification/2-0/what-is-swagger/
- `additionalProperties`
    + https://stackoverflow.com/questions/41239913/why-additionalproperties-is-the-way-to-represent-dictionary-map-in-swagger-ope
    + Represent a Map/Dict with
        * key is property names, and
        * the value's schema is represented by `$ref`

```
GroupMappings:
  description: Mappings for group definitions.
  additionalProperties:
    $ref: "Group"

Group:
  type: object
  description: Represents a group definition.
  required:
    - granularityKey
    - mapping
  properties:
    granularityKey:
      type: string
    mapping:
      $ref: "GroupMapping"

GroupMapping:
  description: The group-to-members mapping for a group.
  additionalProperties:
    type: array
    items:
      type: string
```

# API Definition

- `tags`
    + Set the name for the API class
    + Operations with `tags: admin` will be placed into `AdminApi.java`
