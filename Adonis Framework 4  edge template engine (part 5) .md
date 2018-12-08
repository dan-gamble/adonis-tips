# Adonis Framework 4 Cheat sheet

Adonis Framework 4 Cheat Sheet **Part 5**

Made with ❤️ by Alfredo Paz



Working with *edge* template engine it's a piece of cake; here we're going to make a review about some of nice features on it

List:

1. `@each` loop
2. `@if` conditional
3. `@elseif` conditional 
4. `@unless` method



### Background

_______

Imagine you got some data, into one controller, for this example called *DemoController* in this way

```javascript
const data = [{"name": "alfredo"}, {"name": "jorge"}, {"name": "virk"}, {"name": "joshua"}]
```



So we make a nice index method to send this data from it to a view; in this way

```javascript
async index({ view }) {

const data = [{"name": "alfredo"}, {"name": "jorge"}, {"name": "virk"}, {"name": "joshua"}]
	return view.render("listado", {data: data})
    
}
```



So at this point, we need no print data in an organized way; this to consider

- data comes from in a json form
- data is composed of some objects inside of it
- we need to iterate all of this data



### Making use of *loops* to iterate data

______

We have for example `@each()` loop to iterate data in a view, this makes sense since you don't need to make dirty your view with programming logic 



Inside for example in *resources/views/listado.edge* we can make the following

```javascript
@each(user in data)
	{{ user.name }}
@endeach
```



As final result will get some like this

```html
Adonis members

alfredo 
jorge
virk
joshua
```



### Conditionals

_______

Imagine you need to print certain data under certain conditions, for this scenario; first we check if the username *Virk* exists in the data then print it, otherwise don't print anything.



To achieve this, we're going to use `@if() @endif` conditional

```html
<h1>Adonis members</h1>

@each(user in data)
	@if(user.name == "Virk")
		<h1>Hello Boss: {{ user.name }}</h1>
	@endif
@endeach
```



Now if we need to check about a single value?, well please read the following example

```javascript
async index({ view }) {
		const data = [{"name": "Virk", "job": "Making the coolest Nodejs Framework"}]

		return view.render("listado", {data: data})
	}
```



Well, if the data corresponds to a certain user on your system and you want to print an specific message only if the user is the same you´re comparing; please make some like this.

```javascript
@each(user in data)
	@if(user.name == "Virk")
		<h1>Hello Boss: {{ user.name }}</h1>
		<p>{{ user.job }}</p>
		@else
		<p>Welcome dudes</p>
	@endif
@endeach
```



What  about make a logical comparison like this:

```javascript
if(condition){
    some actions
}else if(condition){
    some actions
}else{
    default actions
}
```



Now with `enge engine` you achieve it in this way

```javascript
@each(user in data)
	@if(user.name == "Virk")
	<h1>Welcome Boss</h1>
	@elseif(user.name == "Alfred")
	<h2>Welcome writter</h2>
	@else
	<h3>Welcome community</h3>
	@endif
@endeach
```



 

AdonisJs offers another way to make a logical comparison, with the `@unless @endunless` method which works in the opossite way to an `if else` conditional; same last scenario but now using it

  ```javascript
@each(user in data)
	@unless(user)
	<h1>Welcome dudes</h1>
	@else
	<h2>Welcome {{ user.name }}</h2>
	<p>{{ user.job }}</p>
	@endunless
@endeach
  ```

As you can see in this case `@unless` is working checking first the negative result of a comparison and after resolves if the response is positive