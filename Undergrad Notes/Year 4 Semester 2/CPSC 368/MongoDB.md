- MongoDB is a type of document database, which uses id numbers to key documents
- You can do the four basic query operations (CRUD) in MongoDB
- In SQL, we create by running CREATE TABLE and then INSERT
- But in MongoDB, inserting into a collection that doesn't exist will create a collection with that name
- When inserting a document, if it does not already have an `_id` value, one will be randomly assigned
- You can insert multiple rows at once with the `insert_many` command
- We can query our database with the find command
- Doesn't use as much natural language terminology compared to SQL
- Can still do things like use in, and, or statements
- First is the fields to be selected, second is the conditions
- When updating values, we can either update the first document we hit, or every document that fulfills that condition
- In MongoDB, each row is represented by a JSON document, or even a nested set of multiple documents
- Depending on which operator you are using, when you want to do a where operation you add another curly brace after the variable you are filtering containing the operator and the condition
- For example, `"$gt"` does greater than, and `"in$"` is the same as in
##### CRUD Operations
- The find function doesn't actually give you the results directly, it gives you a cursor that you can use to iterate through the results
- Projection is when you want to query some columns based on criteria from another column
- Can be done in MongoDB by adding two sets of curly braces in your query
- The first set is the filtering condition, and the second set determines which variables are returned
- Assign a variable to 1 to show it, and 0 to exclude it, `_id` is always shown unless you set it to 0 which is recommended
- Updating is done either with `update_one` or `update_many` and can be used to find and replace specific variables or add fields
- The variable criteria goes in the first bracket, and the second bracket should contain `$set` and the value to be set in the form `{"variable": value}`
- Delete is done with `delete_one` and `delete_many`, the former will delete the first matching row and the other deletes all matching rows
##### Aggregation
- Likely the most important kind of operations for advanced queries
- Lets you add stages to process data step by step
- Supports grouping, count, sum, and other statistical operations like mean and median

| Stage      | Description                                       |
| ---------- | ------------------------------------------------- |
| `$match`   | Filters documents, similar to WHERE               |
| `$group`   | Groups documents, similar to GROUP BY             |
| `$sort`    | Sorts documents, similar to SORT                  |
| `$project` | Includes and excludes fields from a row           |
| `$limit`   | Limits the number of rows shown                   |
| `$skip`    | Skips a number of rows                            |
| `$count`   | Counts the number of rows                         |
| `$unwind`  | Deconstructs an array variable into multiple rows |
| `$lookup`  | Does a left outer join with another table         |
- These operations are used with `db.aggregate`
- This function accepts a list of curly brackets, each containing the chosen aggregate operation
- For group, choose the `_id` value you want group by which contains the column name in the format `"$variablename"`
- Then you can optionally name a column to represent your chosen aggregation as well as the aggregation operation
- For `$sort`, -1 signifies descending, and 1 is ascending
- For `$lookup`, you need to input an array specifying the table to pull from using `from`, the field to merge on in your current table with `localField`, and the field to merge from the other table with `foreignField`
- Also need to set the name of the new field with `as`, the merged info will be inserted as a sub table under that field
- `$unwind` works by creating different rows for each object in an array
- Only works if you have a field containing an array, which appears like a Python list
- Rows that don't contain the specified field can be preserved with null values by setting `preserveNullAndEmptyArrays: true`
- `$match` can also be used to match strings, similar to LIKE in SQL
- This done by putting a curly bracket inside `$match` specifying the field, and then another bracket containing `$regex`, the string matching expression, and `$options: "i"` to ignore case
- Make sure to do this before grouping