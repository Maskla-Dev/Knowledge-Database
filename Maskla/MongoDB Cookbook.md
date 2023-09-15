General purpose document database
data in documents like json documents
attributes are columns
documents are rows, is the basic type of related data
collections are tables, group documents
database contains collections
# document model
documents output is in json format, store format is in bson. Bson adds features to support data types.
document pairs data in key-value format, key and field are interchangeable.
objectid are identifier, automatic id is attached to the document if it is not provided, `_id` field stores the objectid
documents have flexible schema, it means, field structure grows as required without update the data (polymorphic behavior). if a hard structure is required, optional schema validation can be used to constrain document structure.
Documents are delimited by the `{}` characters.
# Data Modeling
Documents lack of data schema, it is a great advantage in the modeling process, because is not necessary follow the harden rules from the Entity-Relationship workflows. However, document model will be highly benefited if relationship analysis is part of the modeling process.

Questions to guide the modeling process:
- *What the application do?* this question is answered during the requirement gathering.
- *What data will store?* this question is answered in the system sketch
- *How will users use this data?* Use-Case models and User Stories can help to know the answer
- *What data will be most valuable to me?* the answer for this question will help to know data domains and data that users won't consume.
Patterns at access and modeling levels can be found when solving the previous answers. Complex relationships ends in document embedding (document inside in another document), whit this, queries and data management comes more efficient. Document referencing is allowed, only object id is needed for this purpose, references becomes handy when related data can easily exceed the 16MB size.
## Modeling Patterns
The modeling patterns becomes from the relationship types: *one-one*, *one-many* and *many-many*.

>***Data that is accessed together should be store together*** First Pattern from model to implementation

![[embedvsreferencing mongo.png]]
### One to One 
If some instance of the entity has a relationship with a unique instance of another entity, the relationships type is one to one.
![[one-to-one example.png]]
For the Backyard object:
```json
{
	"_id_": ObjectId("352335abc"),
	"size": 15,
	"owner": "Smith"
}
```
For the Pool object:
```json
{
	"_id_": ObjectId("124969ade"),
	"size": 2,
}
```
The previous examples are joined in a single document:
```json
{
	"_id_": ObjectId("352335abc"),
	"size": 15,
	"owner": "Smith"
	"pool" : {
		"size": 2
	}
}
```
Also (using linking reference, not recommended):  
```json
{
	"_id_": ObjectId("352335abc"),
	"size": 15,
	"owner": "Smith"
	"pool" : ObjectId("124969ade")
}
```
or (if is a simple attribute): 
```json
{
	"_id_": ObjectId("352335abc"),
	"size": 15,
	"owner": "Smith"
	"pool-size" : 2
}
```
### One to Many
If some instance of the entity has a relationship with many instances of another entity, the relationships type is one to many. Document embedding is the best modeling approach.
![[one-to-many example.png]]
Taking the same structure for pool and backyard, we will notice that the joint logic uses the array storage:
```json
{
	"_id_": ObjectId("352335abc"),
	"size": 15,
	"owner": "Smith"
	"pools" : [
		{ "size": 2 },
		{ "size": 3 },
		{ "size": 6 }
	]
}
```
### Many to Many
If many instances of the entity has a relationship with many instances of another entity, the relationships type is many to many. Document embedding is the best modeling approach.
## Antipatterns
Massive arrays
Massive number of collections
Bloated documents
Unnecessary indexes 
Query without indexes
Queries without indexes
Data that is accessed together, but stored in different collections 