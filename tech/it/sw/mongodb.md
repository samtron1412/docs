# Overview

# Usage of `mongo` shell

- List all databases: `show dbs`
- Switch to DB or Create new DB: `use DB_NAME`
- List all collections in DB: `show collections`
- Create new collection: `db.COLLECTION_NAME.insert(OBJECT)`
- Get all data in the collection: `db.COLLECTION_NAME.find()`
- Search an object: `db.COLLECTION_NAME.find(OBJECT)`
- Search and only get one result: `db.COLLECTION_NAME.findOne(OBJECT)`
- Store results in a variable: using JavaScript
    + `var result = db.COLLECTION_NAME.find().toArray()`: result is an
      array, we can access the first document by `result[0]`
    + `var result = db.COLLECTION_NAME.findOne({...})`
    + `var result = db.COLLECTION_NAME.find()`: result contains cursor
      to documents, it is not documents itself, so after we evaluate
      result once, we loose the access to documents
    + Add a new field to result: `result.new_field = 'something'`
    + Delete a field: `delete result.field`

# MongoDB database tools

- mongoimport: imports content from an extended JSON, CSV, TSV (export
  created by mongoexport
    + Syntax: `mongoimport <options> <connection-string> <file>`
    + `mongoimport -d tacoshop -c people --jsonArray --drop --file users.json`


# MongoDB GUI clients

- MongoDB compass
- Robo 3T
