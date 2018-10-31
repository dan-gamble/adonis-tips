Adonis Framework 4 Cheat Sheet (Lucid ORM and Query Builder tips)

Made with ❤️ by Alfredo Paz



**TIP ONE**

_____________________

If you need for example fetch all data but keep certaing column invisible, then you must use **setHidden** method in this way

```javascript
async fetchData(){
    const data = await User.query()
    					   .setHidden(['created_at'])
     					   .fetch()
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

