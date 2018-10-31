Adonis Framework 4 Cheat Sheet (Lucid ORM and Query Builder tips)

Made with ❤️ by Alfredo Paz



**TIP ONE**

_____________________

If you need for example fetch all data but keep certaing column invisible, then you must use **setHidden** method in this way

```javascript
async fetchData(){
    const data = await User.query().setHidden(['created_at']).fetch()
    return data
}
```



**TIP TWO**

______________

If you need for example fetch all data from users and joining with posts table, and then grouping all titles by user, do this

```javascript
async all(){
		const data = await User.query()
		.select(Database.raw("row_number() OVER(ORDER BY namePost) AS NP"))	
		.select("nameUser")
		.select(Database.raw("GROUP_CONCAT(namePost) AS Listado"))
		.join("posts", "users.id", "=", "posts.user_id")
		.groupBy("nameUser")
		.orderBy("NP")
		return data

	}
```



**TIP THREE**

_______________

You need to get all users and then count their posts, do this



```javascript
async all(){
		const data = await User.query()
		      .select(Database.raw("row_number() OVER(ORDER BY nameUser) AS NP"))
			  .select("nameUser")
			  .join("posts", "users.id", "=", "posts.user_id")
			  .count('*')
			  .groupBy('nameUser')
		return data

	}
```



**TIP FOUR**

_______

Even you can use a *callback* to add multiple **where** calusules in this way

```javascript
async all(){
		const data = await User.query()
		      .where(function(){
		      	this.where('nameUser', 'alfa')
		      		.orWhere('statusUser', '<>', 0)
		      }).fetch()
		return data

	}
```

