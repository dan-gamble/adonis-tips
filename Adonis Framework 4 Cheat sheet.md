# Adonis Framework 4 Cheat sheet

made with ❤️ by: Ing. Alfredo



**Part One.**

_________________



If you want to install a fresh copy from the adonis framework, first download it's CLI 

```bash
npm i -g @adonisjs/cli
```



**Part Two.**

_________



Now, crate a new app in this easy way

```bash
adonis new appname
```



**Part Three.**

______



Great!!! in this step now you can run your app with this command

```bash
adonis serve --dev
```



**Part Four.**

_____



Now if you're gonna working with a database for example a mysql database, then you must to do this

```bash
npm i -S mysql
```



**Part Five.**



So now we need to configure the database access; so open your new app recently created and make this changes

into your *app/.env* file put your mysql credentials

```env
HOST=127.0.0.1
PORT=3333
NODE_ENV=development
APP_URL=http://${HOST}:${PORT}
CACHE_VIEWS=false
APP_KEY=CD2tQfjSjY230r7rNWIHTaD2ytZwoZWf
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3307
DB_USER=root
DB_PASSWORD=password
DB_DATABASE=blog
SESSION_DRIVER=cookie
HASH_DRIVER=bcrypt
```



now into your *app/config/database.js* file, make this changes

```js
module.exports = {
    connection: Env.get('DB_CONNECTION', 'mysql'),
}
```



**Part Six.**

_____



Now we're gonna create our frst controller; in this way (**select the first one option**)

```bash
adonis make:controller UserController
> Select controller type (Use arrow keys)
  For HTTP requests
  For Websocket channel
```



Second we're gonna create our first model, like this

```bash
adonis make:model User
```



**Part Seven.**

_____



Now into our model located at *app/app/Models/User.js* and then make this

```javascript
static get table(){
    return 'users'
}
```



Now into your new Controller located at *app/app/Controllers/UserController* and make this

*declare at the top of your script the following line*

```javascript
const User = use('App/Models/User')
```



Now into your controller class, write a method to generate a query that gets all users registered, like this

```javascript
async getUsers(){
    const response = await User.all()
    return response
}
```



Finally go to *app/start/routes.js* and write the route needed to run you app

```javascript
Route.get('/all', 'UserController.getUsers')
```

 

And you will get something like this on your werb browser

```javascript
[
    {
        "id": 1,
        "nameUser": "car",
        "passwordUser": "password",
        "statusUser": 1,
        "created_at": "2018-10-02 15:30:38"
    },
    {
        "id": 2,
        "nameUser": "motor",
        "passwordUser": "secret",
        "statusUser": 1,
        "created_at": "2018-10-02 15:30:38"
    },
    {
        "id": 3,
        "nameUser": "gama",
        "passwordUser": "secreto",
        "statusUser": 1,
        "created_at": "2018-10-02 15:30:38"
    },
    {
        "id": 4,
        "nameUser": "delta",
        "passwordUser": "nover",
        "statusUser": 1,
        "created_at": "2018-10-02 15:30:38"
    }
]
```



**Part Eight.**

_____



But if you need use SQL fucntions not inclued on Lucid ORM?, well you can write SQL queries using the query builder, like this



First, at the top of your UserController script write this

```javascript
const Database = use('Database')
```



After inside the getUsers method, write this

```javascript
async getUsers(){
    const response = await Database.table('users').count('* as total of Users')
    return response
}
```



You will get something like this

```javascript
[
    {
    	"total of users": 4
    }
]
```



**Part nine**

_______



You wanna see part of the query builder power in action?



See this SQL query

```sql
SELECT row_number() OVER(ORDER BY nameUser) AS NP, users.nameUser, GROUP_CONCAT(namePost) AS List, COUNT(namePost) AS Total
JOIN posts ON users.id = posts.user_id
GROUP BY nameUser
ORDER BY NP;
```



Now the same query, built with query builder

```javascript
const response = await Database
					   .table('users')
					   .select('users.nameUser')
					   .select(Database.raw("row_number() OVER(ORDER BY nameUser) AS NP"))
					   .select(Database.raw("GROUP_CONCAT(namePost) AS List"))
					   .select(Database.raw("COUNT(namePost) AS Total"))
					   .innerJoin('posts', 'users.id', '=', 'posts.user_id')
					   .groupBy('nameUser')
					   .orderBy('NP')
		return response
```



The output will looks like this

```javascript
[
    {
        "nameUser": "xxxxxx",
        "NP": 1,
        "List": "PHP 7,xxxx",
        "Total": 2
    },
    {
        "nameUser": "xxxxx",
        "NP": 2,
        "List": "HTML 5,MySQL 8",
        "Total": 2
    }
]
```

