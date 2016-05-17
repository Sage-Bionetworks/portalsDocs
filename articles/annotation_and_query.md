---
title: Annotations and Queries
layout: article
---

## Query API
The Query API is loosely modeled after Facebook's [Query Language](https://developers.facebook.com/docs/reference/fql/).

### Examples

##### **'Select *' Query**

These queries are generally of the form:

````
SELECT * FROM <data type> [LIMIT <#>] [OFFSET <#>]
````

Currently supported data types:

{:.markdown-table}
| \<data type\> | 
| --------- | 
| project   | 
| folder    |
| file      |
| entity    |

##### **'Order By' Query**

These queries are generally of the form:

````
SELECT * FROM <data type> ORDER BY <field name> [ASC|DESC] [LIMIT <#>] [OFFSET #]
````

##### **Single clause 'Where' Query**

These queries are generally of the form:

````
SELECT * FROM <data type> WHERE <expression> (AND <expression>)* [LIMIT <#>] [OFFSET #]
 
<expresssion> := <field name> <operator> <value>
````

\<value\> should be in quotes for strings, but not numbers (i.e. name == "Smith" AND size > 10)
Currently supported <operators> with their required URL escape codes:

{:.markdown-table}
| Operator               |     Value    |  URL Escape Code |
| :--------------------- | :----------- | :--------------- |
| Equal                  |     ==       |     %3D%3D       |
| Does Not Equal         |     !=       |     !%3D         |
| Greater Than           |      >       |     %3E          |
| Less Than              |      <       |     %3C          |
| Greater Than or Equals |     >=       |     %3E%3D       |
| Less Than or Equals    |     <=       |     %3C%3D       |


##### **Multiple clause 'Where' Query**

These queries are generally of the form:

````
SELECT * FROM <data type> WHERE <expression> (AND <expression>)* [LIMIT <#>] [OFFSET #]
 
<expresssion> := <field name> <operator> <value>
````

\<value\> should be in quotes for strings, but not numbers (i.e. name == "Smith" AND size > 10)
Currently supported <operators> with their required URL escape codes:

{:.markdown-table}
| Operator               |     Value    |  URL Escape Code |
| :--------------------- | :----------- | :--------------- |
| Equal                  |     ==       |     %3D%3D       |
| Does Not Equal         |     !=       |     !%3D         |
| Greater Than           |      >       |     %3E          |
| Less Than              |      <       |     %3C          |
| Greater Than or Equals |     >=       |     %3E%3D       |
| Less Than or Equals    |     <=       |     %3C%3D       |


##### **'Select *' Query for the Layers of a Dataset**

These queries are generally of the form:

````
SELECT * FROM layer WHERE parentId == <parentId> [LIMIT <#>] [OFFSET <#>]
````


##### **'Order By' Query for the Layers of a Dataset**

These queries are generally of the form:

````
SELECT * FROM layer WHERE parentId == <parentId> ORDER BY <field name> [ASC|DESC] [LIMIT <#>] [OFFSET <#>]
````


##### **'Select *' Query for the all the people who have agreed to the terms in the End User License Agreement for a Dataset**

These queries are generally of the form:

````
SELECT * FROM <data type> WHERE <expression> (AND <expression>)* [LIMIT <#>] [OFFSET #]
 
<expresssion> := <field name> <operator> <value>
````

\<value\> should be in quotes for strings, but not numbers (i.e. name == "Smith" AND size > 10)
Currently supported <operators> with their required URL escape codes:

{:.markdown-table}
| Operator               |     Value    |  URL Escape Code |
| :--------------------- | :----------- | :--------------- |
| Equal                  |     ==       |     %3D%3D       |
| Does Not Equal         |     !=       |     !%3D         |
| Greater Than           |      >       |     %3E          |
| Less Than              |      <       |     %3C          |
| Greater Than or Equals |     >=       |     %3E%3D       |
| Less Than or Equals    |     <=       |     %3C%3D       |


### Schema

#### **Query Response Schema** 
The [JsonSchema]("http://json-schema.org/") is an emerging standard similar to DTDs for XML.


