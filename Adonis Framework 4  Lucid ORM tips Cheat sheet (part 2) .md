Adonis Framework 4 Cheat Sheet (Lucid ORM and Query Builder tips) **Part 2**

Made with ❤️ by Alfredo Paz



Obviously in Adonis Framework you can use the **eagger loading concept** in this way



#### Example one

Under the concept one user has many posts, you need to write the following method on your **User** Model

```javascript
posts()
{
    return this.hasMany('App/Models/Post')
}
```



After that on your **UserController** you can get all users and their posts in this way

```javascript
const User = use('App/Models/User')

class UserController
{
    async fetchAll()
    {
        let data = await User.query().with('posts').fetch()
        return data
    }
}
```



#### Example two 

Now if you need to pass this data from **UserController** to a **users.edge** view in this way

```javascript
const User = use('App/Model/User')

class UserController 
{
    async fetchAll({ view })
    {
        let data = await User.query().with('posts').fetch()
        return view.render('users', { data: data.JSON() })
    }
}
```



Now inside the **users.edge** view print all data in this way



```javascript
@unless(data)
	<h2>No hay registros disponibles</h2>
@else
	<h1>Si existen registros</h1>
	<table>
		<tr>
			<th>Nombre del Usuario</th>
			<th>Nombre del Post</th>
			<th>Creado el: </th>
		</tr>
			@each(registro in data)
			<tr>
				<th>{{ registro.nameUser }}</th>
				@each(post in registro.posts)
						<th>{{ post.namePost }}</th>
						<th>{{ post.created_at }}</th>
				@endeach
			</tr>
			@endeach
	</table>
@endunless

```

