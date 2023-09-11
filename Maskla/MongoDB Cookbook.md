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
