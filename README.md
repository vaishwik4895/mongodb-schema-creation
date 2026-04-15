# mongodb-schema-creation
<img width="1920" height="1200" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/3bb50a8e-a078-43cb-8cf1-401f4fae03e4" />
<img width="1920" height="1200" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/e2a7f35a-a521-467d-aabb-ce5d3bf71e93" />
# MongoDB Schema Validation — Users Collection

This project demonstrates how to define and enforce a schema in MongoDB using **JSON Schema validation**. The goal is to ensure that documents inserted into the collection follow a structured format.

---

## Objective

To create a MongoDB collection (`users`) with validation rules for the following fields:

* `name` → String
* `email` → String (must follow email format)
* `age` → Integer (must be ≥ 0)

---

## Implementation Steps

### 1. Create Database

```js
use myDatabase
```

---

### 2. Create Collection with Schema Validation

```js
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email", "age"],
      properties: {
        name: {
          bsonType: "string"
        },
        email: {
          bsonType: "string",
          pattern: "^.+@.+$"
        },
        age: {
          bsonType: "int",
          minimum: 0
        }
      }
    }
  }
})
```

---

### 3. Insert Valid Document

```js
db.users.insertOne({
  name: "Alice",
  email: "alice@example.com",
  age: 22
})
```

Successfully inserted because it matches schema rules.

---

### 4. Retrieve Data

```js
db.users.find()
```

---

### 5. Insert Invalid Document (Example)

```js
db.users.insertOne({
  name: "Alice1",
  email: "aliceexample.com",
  age: twenty
})
```

This fails because:

* `email` does not match required format
* `age` is not an integer

---

## Important Notes

* MongoDB is schema-less by default, but validation can be enforced using `$jsonSchema`
* Validation ensures data integrity

Example error:

```
ReferenceError: twenty is not defined
```

---

## Concepts Covered

* MongoDB collections and documents
* Schema validation using `$jsonSchema`
* Data types (`string`, `int`)
* Constraints (`required`, `minimum`, `pattern`)
* CRUD operations (`insertOne`, `find`)

---

## Tools Used

* MongoDB Server
* Mongosh (MongoDB Shell)
* Windows Command Line

---

## Conclusion

This project demonstrates how MongoDB can enforce structure in a NoSQL database using schema validation, ensuring only valid and properly formatted data is stored.

---

## Author

Developed as part of a MongoDB assignment.

---


