# Create Table API Endpoint

*https://{{domain}}/api/v1/realtime/database/create_table*
                

Store and sync data with our cloud database. Data is synced across all clients in realtime, and remains available in all of your apps. The Realtime Database API is a cloud-hosted database. Data is stored and consumed as JSON and synchronized in realtime to every connected client. You can access these tables via X-Dev Console (Xposed Development Console).

To use this API, you need an API key. Please contact me at young.cet@gmail.com to get your own API key.
Create table
                
To create a table you need to make a POST call to the following url :
*https://{{domain}}/api/v1/realtime/database/create_table*
```
#Here is a curl example
curl -X POST https://{{domain}}/api/v1/realtime/database/create_table
   -H 'Content-Type: application/json'
   -H 'APIKEY: {{your-api-key}}'
   -d '{"query":"CREATE TABLE {{test}}(id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,first_name VARCHAR(30) NOT NULL,last_name VARCHAR(30) NOT NULL,email VARCHAR(70) NOT NULL UNIQUE)"}'
   
   
Result example :

{
    "message": "success",
    "request": {
        "query": "CREATE TABLE test(id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,first_name VARCHAR(30) NOT NULL,last_name VARCHAR(30) NOT NULL,email VARCHAR(70) NOT NULL UNIQUE)",
        "name": "test"
    }
}
```                

QUERY PARAMETERS
```
Field 	Type 	Description
query 	String 	The SQL prepare statement to execute

HTTP HEADERS

These are the HTTP Headers to include in your request.
Header 	Value
Content-Type 	application/json
APIKEY 	{{your-api-key}}
```

# Storing Data in a Table

You can store data in the table/s created by a simple call.

Store Data in a Table API Endpoint

*https://{{domain}}/api/v1/realtime/database/modify_table*
                

### Store Data      

To store data you need to make a POST call to the following url :
*https://{{domain}}/api/v1/realtime/database/modify_table*
```
#Here is a curl example
curl -X POST https://{{domain}}/api/v1/realtime/database/modify_table
   -H 'Content-Type: application/json'
   -H 'APIKEY: {{your-api-key}}'
   -d '{"query":"insert into {{test}} (first_name, last_name, email) values (?,?,?)", "values":["test3", "test3", "test5@somedomain.com"], "bind":"sss"}'
   
   
Result example :

{
    "message": "success",
}
```                

QUERY PARAMETERS
```
Field 	Type 	Description
query 	String 	The SQL prepare statement to execute
values 	Array 	The values to pass in SQL statement
bind 	String 	The value binding data types

HTTP HEADERS

These are the HTTP Headers to include in your request.
Header 	Value
Content-Type 	application/json
APIKEY 	{{your-api-key}}
```

# Querying Data in a Table

You can select the data inserted into the tables by making an HTTP request.

Query Data in a Table API Endpoint

*https://{{domain}}/api/v1/realtime/database/select_rows*
                

### Select Rows
                

To select rows from a table you need to make a POST call to the following url :
*https://{{domain}}/api/v1/realtime/database/select_rows*
```
#Here is a curl example
curl -X POST https://{{domain}}/api/v1/realtime/database/select_rows
   -H 'Content-Type: application/json'
   -H 'APIKEY: {{your-api-key}}'
   -d '{"query":"select * from {{test}} where email = ?", "values":["test5@somedomain.com"], "bind":"s"}'
   
   
Result example :

{
    "results": "success",
    "rows": [{
        "id": 1,
        "first_name": "test3",
        "last_name": "test3",
        "email": "test5@somedomain.com"
    }],
    "num_of_rows": 1
}
```             

QUERY PARAMETERS
```
Field 	Type 	Description
query 	String 	The SQL prepare statement to execute
values (optional) 	Array 	The values to pass in SQL statement
bind (optional) 	String 	The value binding data types

HTTP HEADERS

These are the HTTP Headers to include in your request.
Header 	Value
Content-Type 	application/json
APIKEY 	{{your-api-key}}
```

# Listing a Table

You can select a single table or all tables by making an HTTP request.

Listing a Table API Endpoint

*https://{{domain}}/api/v1/realtime/database/show_table/*
                

### Listing a Table
                

To list a single table you need to make a GET call to the following url and append the table name at the end:
*https://{{domain}}/api/v1/realtime/database/show_table/test*

To list all tables you need to make a GET call to the following url:
*https://{{domain}}/api/v1/realtime/database/show_tables*

```
#Here is a curl example for listing a single tabble
curl https://{{domain}}/api/v1/realtime/database/show_table/
   -H 'Content-Type: application/json'
   -H 'APIKEY: {{your-api-key}}'

#Here is a curl example for listing all tables
curl https://{{domain}}/api/v1/realtime/database/show_tables
   -H 'Content-Type: application/json'
   -H 'APIKEY: {{your-api-key}}'
   
   
Result example of listing a single table :

{
    "message": "success",
    "test": {
        "columns": ["id", "first_name", "last_name", "email"],
        "created": "2022-02-24 16:13:32",
        "num_of_rows": 1
    }
}


Result example of listing all tables :

{
    "results": "success",
    "rows": [{
        "table_name": "persons_2306",
        "created": "2022-02-19 17:58:47",
        "columns": ["id", "name", "lname", "email"],
        "num_of_rows": 0
    }, {
        "table_name": "persons_4819",
        "created": "2022-02-19 18:06:28",
        "columns": ["id", "first_name", "last_name", "email"],
        "num_of_rows": 3
    }, {
        "table_name": "test",
        "created": "2022-02-24 23:40:06",
        "columns": ["id", "first_name", "last_name", "email"],
        "num_of_rows": 1
    }],
    "num_of_rows": 3
}
```              
