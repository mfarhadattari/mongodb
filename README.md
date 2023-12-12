# MongoDB

### MongoDB is a NoSQL database storing data in JSON-link documents called BSON.

- NoSQL database break from traditional models, ideal for managing vast data.
  MongoDB stands out for its scalability, flexibility and performance trusted by giants like Google, Facebook and eBay

- A record in MongoDB is a document, which is a data structure composed of key value pairs similar to the structure of JSON objects.

```
### Database => Collection => Document => Field
```

## Advantage of MongoDB:

- Scalability high-performance & Open source.
- Document-oriented Database JSON format called BSON.
- Cost-effective solution.
- Rich Ecosystem of tools, Documentation and Community.
- Indexing, Aggregation and Security Features.
- Free Atlas Database and GUI.

## Deference Between MongoDB and Traditional Database:

- Data Model: Data store JSON formal Document <==> Data store in tabular format
- Scheme: Flexible Schema <==> Rigid Schema
- Scalability: Horizontally and Vertically Scalable <==> Vertically Scalable
- Performance: Optimized for unstructured or semi-structured data - Optimized for structured data
- Database : Collection => Document => Field <==> Tables => Rows => Columns

## Uses:

- E-commerce Application
- Social Media Application
- Gaming Application
- Real time application
- Charting Application
- Blogging Application

## Basic Commands of shell

- show dbs: To show all database name

```shell
show dbs
```

- use dbName : to create a database

```shell
use testdb
```

- db.createCollection("collectionName"): to create a collection in database

```shell
db.createCollection("user")
```

- db.dropDatabase() : Delete Database

```shell
db.dropDatabase()
```

- db.collectionName.drop() : Delete a Collection of Database

```shell
db.user.drop()
```

## MongoDB Operation:

### Insert Operation:

- insetOne()

```shell
db.user.insertOne(data)
```

- insertMany()

```shell
db.user.insertMany(arrayOfData)
```

### Find Operation:

- find()

```shell
db.user.find()
```

```shell
db.user.find({gender: "male"})
```

- findOne()

```shell
db.user.findOne({ _id: ObjectId("654dbfa0ac03b4ef85f2a90a") })
```

### Sorting Operation

- sort()

```shell
db.user.find({gender: "male"}).sort({ age:1 })
```

### Projection Operation

```shell
db.user.find({ gender: "male" }, {_id:0, name: 1, gender: 1})
```

```shell
db.user.findOne({ _id: ObjectId("654dbfa0ac03b4ef85f2a90a") }, {_id:0, name: 1, gender: 1})
```

- project()

```shell
db.user.find({ gender: "male" }).project({_id:0, name: 1, gender: 1 })
```

### Limiting Operation

- limit()

```shell
db.user.find({gender: "male"}).limit(100)
```

### Update Operation:

- updateOne()

```shell
db.user.updateOne({ _id: ObjectId("654dbfa0ac03b4ef85f2a90a") }, { $set: { isActive: true } })
```

- updateMany()

```shell
db.user.updateMany({ company: "MICRONAUT" }, { $set: { company: "MICROHUT" } });
```

### Delete Operation:

- deleteOne()

```shell
db.user.deleteOne({ _id: ObjectId("654dbfa0ac03b4ef85f2a90a") })
```

- deleteMany()

```shell
db.user.deleteMany({ gender: "male" })
```

## MongoDB Query Operator

### Comparison Operator

- $eq => equal

```shell
db.user.find({ isActive: { $eq: true } }).project({ name: 1, isActive: 1 })
```

- $ne => not equal

```shell
db.user.find({ eyeColor: { $ne: "blue" } }).project({ name: 1, eyeColor: 1 })
```

- $gt => grater then

```shell
db.user.find({ age: { $gt: 35 } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- $gte => grater than or equal

```shell
db.user.find({ age: { $gte: 35 } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- $lt => less than

```shell
db.user.find({ age: { $lt: 35 } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- $lte => less than or equal

```shell
db.user.find({ age: { $lt: 34 } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- $in => Matches any of the values specified in an array.

```shell
db.user.find({ age: { $in: [20, 25, 30] } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- $nin => Matches none of the values specified in an array.

```shell
db.user.find({ age: { $nin: [20, 25, 30] } }).project({ name: 1, age: 1 }).sort({ age: 1 })
```

- use multiple relational operators: implicit and

```shell
db.user.find({ age: { $gte: 20, $lte: 30 }, gender: { $eq: 'male' } })
```

### Logical Operator

- $and => Returns documents where both queries match

```shell
db.user.find({
    $and: [
        { age: { $lte: 30 } },
        { age: { $gte: 20 } },
        { gender: { $eq: 'female' } },
        { eyeColor: { $nin: ["blue", 'green'] } }
    ]
})
```

- $or => Returns documents where either query matches

```shell
db.user.find({
    $or: [
        { gender: { $eq: 'male' }, age: { $gte: 20, $lte: 30 } },
        { gender: { $eq: 'female' }, age: { $gte: 18, $lte: 23 } }

    ]
})
```

- $nor => Returns documents where both queries fail to match

```shell
db.user.find({
    $nor: [
        { age: { $lte: 35 } },
        { gender: { $eq: 'male' } },
        { eyeColor: { $in: ['blue', 'green'] } }
    ]
})
```

- $not => Returns documents where the query does not match

```shell
db.user.find({
    age: {
        $not: {
            $gte: 25
        }
    }
})
```

### Element Query Operator

- $exists => Matches documents that have the specified field.

```shell
db.user.find({ salary: { $exists: true } })
```

- $type => Selects documents if a field is of the specified type.

```shell
db.user.find({ age: { $type: "int" } })
```

```shell
db.user.find({ age: { $type: ["string", "int"] } })
```

### Array Query Operator

- $all => Selects the documents where the value of a field is an array that contains all the specified elements.

```shell
db.user.find({
    tags: {
        $all: ["Lorem", "commodo", "laborum"]
    }
})
```

- $elemMatch => Matches documents that contain an array field with at least one element that matches all the specified query criteria.

```shell
db.user.find({
    skills: {
        $elemMatch: {
            name: "JAVASCRIPT",
            level: "Intermidiate"
        }
    }
})
```

- $size => matches any array with the specified number of elements.

```shell
db.user.find({
    friends: {
        $size: 4
    }
})
```

## MongoDB Update Operator

### Field

- $set => Replace the value of a field

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $set: {
        age: 20,
        salary: 400
    }
})
```

- $unset => Removes the field from the document

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $unset: { interests: "" }
})
```

- $inc
- $max
- $min
- $rename

### Array

- $addToSet => Adds distinct elements to an array

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $addToSet: {
        languages: "English"
    }
})
```

- $push => Adds an element to an array

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $push: {
        interests: "Reading Story"
    }
})
```

- $each

```shell
# <=============== With $addToSet===================>
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $addToSet: {
        interests: {
            $each: ["Coding", "Travaling"]
        }
    }
})
```

```shell
# <=============== With $push===================>
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $push: {
        interests: {
    $each: ["Coding", "Travaling"]
}
    }
})
```

- $pop => Removes the first or last element of an array

```shell
# <================Remove Last Element ===================>
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $pop: {
        friends: 1
    }
})

# <================Remove First Element ===================>
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $pop: {
        friends: -1
    }
})
```

- $pull => Removes all array elements that match a specified query

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $pull: {
        languages: "English"
    }
})
```

- $pullAll => Removes all matching values from an array.

```shell
db.user2.updateOne({ "_id": ObjectId("6406ad63fc13ae5a40000065") }, {
    $pullAll: {
        languages: ["Catalan", "Thai"]
    }
})
```

- $ (positional operator)

```shell
db.user2.updateMany({ "skills.name": "JAVASCRIPT" }, {
    $set: {
        "skills.$.name": "TYPESCRIPT",
        "skills.$.level": "Intermidiate",
    }
})
```

- $slice
- $sort

## MongoDB Aggregation

### Aggregation Operator

- $match
- $group
- $limit
- $project
- $sort
- $addFields
- $out
- $merge
- $unwind
- $facet
- $lookup

## MongoDB Indexing

- createIndex()

```shell
db.user.createIndex({email: 1})
```

- dropIndex()

```shell
db.user.dropIndex({email: 1})
```
