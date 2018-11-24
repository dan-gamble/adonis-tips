Adonis Framework 4 Cheat Sheet (Create new columns) **Part 3**

Made with ❤️ by Alfredo Paz

ADD A NEW COLUMN TO AN EXISTING TABLE.

In this example we need to add a column named **features** after **email** on an existing table which contains data; drop all migrations **is not an option**



### Step One.

_______

Run the following command to create a new migration file

```bash
adonis make:migration add_features_users
```



Now the command cli will ask to you if you need create or select a table; please use the **select table** option 

```bash
> Choose an action Select table
√ create  database\migrations\1543069307679_add_features_to_users_schema.js
```



### Step Two.

_______

After that open your adonis project and go to **nameProject/database/migration** and open the new migration file; add the following code:

```javascript
'use strict'

const Schema = use('Schema')

class AddFeaturesToUsersSchema extends Schema {
  up () {
    this.table('add_features_to_users', (table) => {
      table.json('features')
      	.after('email')
      	.notNullable()
    })
  }

  down () {
    this.table('add_features_to_users', (table) => {
      // reverse alternations
    })
  }
}

module.exports = AddFeaturesToUsersSchema

```



As you can see the name of the table is not correct, so we need to change this line:

```javascript
this.table('add_features_to_users', (table) => {
```



By this:

```javascript
this.table('users', (table) => {
```



Why?

> Because the correct table's name is **users**



### Step three

_______

After that please run this command

```bash
adonis migration:run
```



And you will receive a message similiar to this one

```bash
migrate: 1543069307679_add_features_to_users_schema.js
Database migrated successfully in 1.63 s
```



### Step four

______

Now if you make a `describe tableName` on your sql console, you will read the new column created

```mariadb
[test]> describe users;
+------------+------------------+------+-----+---------+----------------+
| Field      | Type             | Null | Key | Default | Extra          |
+------------+------------------+------+-----+---------+----------------+
| id         | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| username   | varchar(80)      | NO   | UNI | NULL    |                |
| email      | varchar(254)     | NO   | UNI | NULL    |                |
| features   | longtext         | NO   |     | NULL    |                |
| password   | varchar(60)      | NO   |     | NULL    |                |
| created_at | datetime         | YES  |     | NULL    |                |
| updated_at | datetime         | YES  |     | NULL    |                |
+------------+------------------+------+-----+---------+----------------+
```

