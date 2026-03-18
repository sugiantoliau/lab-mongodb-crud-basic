# lab-mongodb-crud-basic

### **🛠 Project Overview**

Title: lab mongodb crud basic

Description: 
This repository provides a basic, hands-on introduction to the fundamentals of MongoDB using the MongoDB Shell (mongosh). It guides users through the essential CRUD (Create, Read, Update, and Delete) workflow, covering tasks such as inserting JSON-like documents and performing simple data queries.


<br>

### **🛠 Prerequisites**


Before you begin, ensure you have the following installed:
1. A MongoDB Atlas account (or a local MongoDB instance)
2. MongoDB Shell (mongosh)

<br>

### **🛠 Environment Setup**
To keep your database safe, never hardcode your password in your scripts. Use environment variables instead.

1. Clone the repository
   ```bash
   git clone https://github.com/sugiantoliau/lab-mongodb-crud-operations.git
   cd lab-mongodb-crud-operations

2. Set your Connection String
Store your Atlas URI in an environment variable to keep your credentials out of your terminal history:

   For Windows:
   ```powershell
   $env:MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/dbname
   ```
   
   For Mac/Linux:
   ```Bash
   export MONGO_URI="mongodb+srv://<username>:<password>@cluster.mongodb.net/dbname"
   ```

<br>

### 🛠 **How to Practice**

### Metadata & Database Management

Displays the current MongoDB server version:
```MongoDB Shell
db.version()
```

Lists all existing databases on the server along with their storage sizes:

```MongoDB Shell
show dbs
```
```
show databases
```

Switches the context to the training database, creating it automatically if it doesn't exist:
```MongoDB Shell
use training
```


Explicitly creates a new collection named languages within the active database.
```MongoDB Shell
db.createCollection("languages")
```

Lists all collections (the NoSQL equivalent of tables) available in the current database.
```MongoDB Shell
show collections
```
```
show tables
```

<br>

### CRUD: Create & Read Operations


Adds new JSON documents into the languages collection to store programming language data.

```MongoDB Shell
db.languages.insert({"name":"java","type":"object oriented"})
db.languages.insert({"name":"python","type":"general purpose"})
db.languages.insert({"name":"scala","type":"functional"})
db.languages.insert({"name":"c","type":"procedural"})
db.languages.insert({"name":"c++","type":"object oriented"})
```


Returns the total number of documents currently stored within the specified collection.
```MongoDB Shell
db.languages.countDocuments()
```

Queries and displays all documents stored within a collection.
```MongoDB Shell
db.languages.find()
```

Retrieves the first document that matches the query (or the first one found) to inspect data structure.
```MongoDB Shell
db.languages.findOne()
```


Restricts the query output to only the first 3 documents retrieved.
```MongoDB Shell
db.languages.find().limit(3)
```

Filters the collection to find specific documents where the "name" field equals "python".
```MongoDB Shell
db.languages.find({"name":"python"})
```

Uses projection to include only the "name" field (and the default _id) in the results.
```MongoDB Shell
db.languages.find({},{"name":1})


Uses projection to exclude the "name" field while displaying all other data.
```MongoDB Shell
db.languages.find({},{"name":0})
```

Filters the collection to retrieve all documents where the "type" field exactly matches the value "object oriented"
```MongoDB Shell
db.languages.find({"type":"object oriented"})
```

Filters the collection to retrieve all documents where the "type" field exactly matches the value "object oriented"
```MongoDB Shell
db.languages.find({"type":"object oriented"},{"name":1})
```

<br>

The general syntax for updating multiple documents; the first object defines which documents to match, and the $set operator defines the specific fields to modify or add.

db.collection.updateMany({what documents to find},{$set:{what fields to set}})

Updates every document in the collection (since the filter {} is empty) to include a new field called "description" with the value "programming language".
```MongoDB Shell
db.languages.updateMany({},{$set:{"description":"programming language"}})
```

Targets only the document where the name is "python" and adds or updates the "creator" field to "Guido van Rossum".
```MongoDB Shell
db.languages.updateMany({"name":"python"},{$set:{"creator":"Guido van Rossum"}})
```

Finds all languages categorized as "object oriented" and adds a boolean field compiled set to true.
```MongoDB Shell
db.languages.updateMany({"type":"object oriented"},{$set:{"compiled":true}})
```

<br>


Deletes all documents from the languages collection where the name is "scala".
```MongoDB Shell
db.languages.remove({"name":"scala"})
```

Deletes all documents categorized under the "object oriented" type.
```MongoDB Shell
db.languages.remove({"type":"object oriented"})
```


Deletes all documents within the collection but keeps the collection structure and indexes intact (similar to TRUNCATE in SQL).
```MongoDB Shell
db.languages.remove({})
```

