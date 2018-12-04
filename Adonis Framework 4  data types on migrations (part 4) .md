# Adonis Framework 4 Cheat sheet

Adonis Framework 4 Cheat Sheet  **Part 4**

Made with ❤️ by Alfredo Paz



### DECIMAL

______________________

If you need to store decimal numbers; you need first to do:

- declare a name to the column, in this example: `price`
- max length identified by the number 5
- reserved decimal space identified by the number 2

```javascript
table.decimal('price', 5, 2).notNullable()
```



### ENUM

_______________

If you need to declare a default list values, maybe you need to do this

- write a name for the column 
- declare an array with default values

```javascript
table.enum('jobs', ['CEO', 'CTO', 'COO', 'Programmer']).notNullable()
```



### JSON

______________

If you need to store a **json** inside your database, *this data type is available in mariaDB for example*, do this

```javascript
table.json('features').notNullable()
```



### TINYINT

_______________

What about a boolean value?, do this

```javascript
table.boolean('status')
```



### LONGTEXT

_________________

You need to store a lot of text?, maybe you want to use a `longText` data type; in adonisJs is in this way

```javascript
table.longText('biography').notNullable()
```



### BIG INTEGER

_____________

You need to sore a `bigInteger` format number? no problem do it in this way

```javascript
table.bigInteger('identifier')
```



### VARCHAR

________________

To store a `varchar` data type, you need to use the `string` method in this way

Optionally you can pass a second argument to indicate the `max-length` of this column

```javascript
table.string('name', 60).notNullable()
```



### DATETIME

______________

To store `datetime` data type, you can use two different methods

*The first one* Using the `dateTime()` method

```javascript
table.dateTime('created_at').notNullable()
```



*The second one* Or with the `timestamps` method in this way

> The main difference with this method, is that AdonisJs called automatically both columns: `created_at` y `updated_at` 

```javascript
table.timestamps()
```



### PRIMARY KEY AUTO_INCREMENT

___________________

The final one, *How to declare an primary key an auto_increment column?*



For example in pure SQL you declare a `PRIMARY KEY` in this way

```mariadb
id INT PRIMARY KEY AUTO_INCREMENT
```



Now in Adonis, you only need to do it in this way

```javascript
table.increments()
```

and.... thats it