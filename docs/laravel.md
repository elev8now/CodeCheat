# Laravel 

## Terminology

**Framework**
-  A foundation of existing code that supports the building and deployment of applications using less code 

**Variable**
- A value that is stored and can change over time

**Function**
- A piece of code that takes an argument, performs an action, and returns an output 

**Object**
- A way of storing various types of information (properties or instance methods) in key/value pairs

**Class**
- A way of encapsulating code as a template/blueprint for instantiating an Object instance, or creating reusable code

**Property**
- A variable within a Class  

**Method**
- A function within a Class

**Instance / Instantiate**
- An Object instance is an instantiated class 

**Class method**
- A method that you can call without instantiating a Class

**Instance method**
- A method that exists within an Object instance

**MVC**
- Model View Controller 
  - A **model** is where you put code that is responsible for putting data into and getting data out of the database 
  - A **view** is ...
  - A **controller** is where you put code that code handles the request and sends the response 

**OOP**
- Object Oriented Programming - a paradigm of organising code 

**API**
- Application Programming Interface (API)
- In basic terms, APIs just allow applications to communicate with one another

**HTTP**
- Hypertext Transfer Protocol (HTTP) is essentially a well defined text format or standard that the browser is able to interpet into a web page. 
- By default, servers liten on port 80 for any request that looks like HTTP. If it receives a valid request, it sends back an HTTP response.

**HTTP Request Methods**

- GET - used to retrieve data
- POST - used to submit data
- PUT - used to edit data
- PATCH - used to edit data
- DELETE - used to delete data 

* * *

## Introduction

- Created by Taylor Otwell: previously a .NET developer
- A modern PHP framework
- Written using modern best practices
- Minimal core: uses Composer packages where possible
- Built on [Symfony](https://symfony.com)
- Great ecosystem

### Laravel Features

- **Homestead** Vagrant configuration
- **Eloquent ORM**
- CLI tool **artisan**
- **Database migrations**
- Scheduling
- Job Queues
- Good documentation
- Active community: [Laracasts](https://laracasts.com)
- [Laravel Forge](https://forge.laravel.com): easily host Laravel apps

* * *

## Creating an API

### Setup

We'll need to install the Laravel installer package:

```shell
composer global require laravel/installer
```

This will allow us to easily create new Laravel projects. You'll only need to run this once (or if you get a new computer).

* * *

### New Project

To create a new Laravel project run:

```shell
laravel new blog-api
```

**Note**: `blog-api` is just the project name, you could choose anything.

We're going to use Vagrant. Laravel has a prebuilt box called **Homestead**.

In the newly created `blog-api` directory, run:

```shell
composer require laravel/homestead --dev
```

Next, we need to setup Homestead:

```shell
vendor/bin/homestead make
```

Next, change the second line of `Homestead.yaml`:

```
memory: 512
```

Finally, we can run:

```shell
vagrant up
```

Once Vagrant has finished loading visit `http://homestead.test` (or `http://localhost:8000` in Windows)

* * *

### Routing

We're already familiar with **routing** from when we did React. The concept is very similar in Laravel: we need to take a URL and use it to determine what we want to do.

First, let's add a route to handle `POST` events sent to `/articles`. This will point to code that handles creating a new article.

Add a `POST` route for `/articles` to `routes/api.php`:

```php
// use the post method
// when the use request /articles - don't need the forward slash
// which will call the store method of the Articles controller
$router->post("articles", "Articles@store");
```

* * *

### Controllers

In Laravel routes point to **controllers**. It is the controller's job to deal with the request and return a response.

Run the following inside your Vagrant box<sup>†</sup> to create an Articles controller:

```shell
artisan make:controller Articles --api
```

Laravel has added a `store` method to `Articles`:

```php
public function store(Request $request)
{
    // handle post request
}
```

<p class="footnote">† <i>All</i> commands should be run inside Vagrant</p>

* * *

### Database Migrations

We'll need to store the articles in a database so that the data is persisted.

Laravel makes it really easy to deal with database structuring using **database migrations**.

Database migrations are bits of code that tell the database how it should be structured. These are run by Laravel when we run the `artisan migrate` command. This means anyone with our codebase can easily get their database to have the right structure for the app.

#### Creating a Model/Migration

On your Vagrant box run:

```shell
artisan make:model Article -m
```

This will create an Article model class (in `app/Article.php`) as well as a database migration (in the `database/migrations` directory).

* * *

### Database Migrations

We'll need to update the migration file to create the structure we'll need to store an article:

```php
public function up()
{
    Schema::create('articles', function (Blueprint $table) {
        $table->increments('id');
        $table->string("title", 100);
        $table->text("article");
        $table->timestamps();
    });
}
```

Finally, we need to run the migrations:

```shell
artisan migrate
```

We should now have an `articles` table in the database.

**Note**: if you make a mistake in your migration file, you can run `artisan migrate:rollback` to undo the last set of migrations that you ran.

* * *

### Models

The `Article` model **extends** the Eloquent ORM model. This allows us to use the model to interact with the data from the database.

For example, to add an article to the database we can use the `Article::create()` method. And to get all the articles out of the database we can use `Article::all()`.

Once we have an `Article` object we can access the data from the database. For example:

```php
$article->title; // would give us the article title
$article->title = "Blah blah blah"; // would set the article title
```

If you change the values of a model object, make sure you run `save()` on it:

```php
$article->save();
```

You can read more above models on the [Eloquent ORM Documentation](http://laravel.com/docs/5.6/eloquent#introduction).

* * *

### Creating

Now we've got somewhere to store the articles, we need to update our controller so that we can create an Article.

First, we need to tell the controller to use the `Article` model that we created using `artisan`:

```php
// make sure you add this near the top, undereath the namespace declaration
use App\Article;
```

Then we need to update our `store` function to create an article using the data from the request:

```php
public function store(Request $request)
{
    // get post request data for title and article
    $data = $request->only(["title", "article"]);

    // create article with data and store in DB
    $article = Article::create($data);

    // return the article along with a 201 status code
    return response($article, 201);
}
```

Now we can try doing a `POST` request with Postman.

* * *

### Mass Assignment Vulnerability

If we're not careful we might accidentally allow users to update fields that they should have access to. Laravel guards against this by default.

We can update the `Article` model to tell it which fields to expect.

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Article extends Model
{
    // Only allow the title and article field to get updated via mass assignment
    protected $fillable = ["title", "article"];
}
```

Now try doing a `POST` request with Postman.

* * *

### Listing

Next let's setup the `GET` request to `/articles`.

First, add the route:

```php
$router->get("articles", "Articles@index");
```

And update the `index` method in the `Articles` controller:

```php
public function index()
{
    // get all the articles
    return Article::all();
}
```

That's all there is to it: Laravel does all the hard work for us once we've setup our model.

* * *

### Reading

Next we want to add a route for `GET` to something like `/articles/1`.

First, add a route:

```php
// we can group all our articles routes together
$router->group(["prefix" => "articles"], function ($router) {
    // ...previous routes...

    // {article} is a url parameter representing the id we want
    $router->get("{article}", "Articles@show");
});
```

And update the `show` method in `Articles`:

```php
// the id gets passed in for us
public function show($id)
{
    return Article::find($id);
}
```

* * *

### Editing

Next we'll add editing. We'll need a `PUT` route for `/articles/{article}`.

Add a route:

```php
$router->group(["prefix" => "articles"], function ($router) {
    // ...previous routes...

    $router->put("{article}", "Articles@update");
});
```

And update the `update` method in `Articles`:

```php
public function update(Request $request, $id)
{
    // find the current article
    $article = Article::find($id);

    // get the request data
    $data = $request->only(["title", "article"]);

    // update the article
    $article->fill($data)->save();

    // return the updated version
    return $article;
}
```

* * *

### Deleting

Finally, let's add a `DELETE` route.

Add a route:

```php
$router->group(["prefix" => "articles"], function ($router) {
    // ...
    $router->delete("{article}", "Articles@destroy");
});
```

And update the `destroy` method in `Articles`:

```php
public function destroy($id)
{
    $article = Article::find($id);
    $article->delete();

    // use a 204 code as there is no content in the response
    return response(null, 204);
}
```

* * *

### Route Model Binding

What if we try to update `/articles/34849`? Currently we'll get a 500 error as there is no article with ID 34849.

However, we can use **Route Model Binding** to automatically fix this for us.

```php
public function show(Article $article)
{
    return $article;
}

public function update(Request $request, Article $article)
{
    $data = $request->only(["title", "article"]);
    $article->fill($data)->save();
    return $article;
}

public function destroy(Article $article)
{
    $article->delete();
    return response(null, 204);
}
```

Less code and more functionality. Laravel is your friend.

* * *

### Resources

It would also be good if we had some control over how our data comes back. For example when we're listing the articles we probably don't want to send the full article text and when we might not want to send the `created_at` and `updated_at` properties.

This is where **Resources** come in. They let us control the format of the JSON output.

First, we create one using `artisan make:resource ArticleResource`.

Then we edit the file to list the properties we need:

```php
public function toArray($request)
{
    // just show the id, title, and article properties
    // $this represents the current article
    return [
        "id" => $this->id,
        "title" => $this->title,
        "article" => $this->article,
    ];
}
```

Next, we need to update the `Articles` controller to use the resource for output:

```php
use App\Http\Resources\ArticleResource;

// ...

public function store(Request $request)
{
    // ... store code

    // return the resource
    // automatically uses the right status code
    return new ArticleResource($article);
}

public function show(Article $article)
{
    // return the resource
    return new ArticleResource($article);
}

public function update(Request $request, Article $article)
{
    // ... update code

    // return the resource
    return new ArticleResource($article);
}
```

* * *

We also want to make the `list` method only show the `id` and `title` properties.

Again, we'll make a resource: `artisan make:resource ArticleListResource`

```php
public function toArray($request)
{
    return [
        "id" => $this->id,
        "title" => $this->title,
    ];
}
```

And update the `Articles` controller:

```php
use App\Http\Resources\ArticleListResource;

// ...

public function index()
{
    // needs to return multiple articles
    // so we use the collection method
    return ArticleListResource::collection(Article::all());
}
```

As we're returning a collection of articles rather than a single article we use the `Resource::collection()` method.

* * *

### CORS

Finally, we need to make sure our API will work with our Redux app.

By default browsers won't allow JS from domain *x* to get data from domain *y* as they have different **origins**, a potential security issue. However, if our API is on a separate domain we need to be able to make cross-origin requests.

Modern browsers use something called **Cross-Origin Resource Sharing** to handle this. This uses HTTP headers to let us define who can and can't use our API.

We don't want to have to write the code for this ourselves as it's fairly complicated. Luckily, [someone else has done it for us](https://github.com/barryvdh/laravel-cors).

```shell
composer require barryvdh/laravel-cors
```

We'll need to update a few files to get it working.

First, run:

```shell
php artisan vendor:publish --provider="Barryvdh\Cors\ServiceProvider"
```

Then, in `config/app.php`:

```php
'providers' => [
    // ...other providers...
    Barryvdh\Cors\ServiceProvider::class,
],
```

In `app/Http/Kernel.php`:

```php
protected $middleware = [
    // ...other middleware...
    \Barryvdh\Cors\HandleCors::class,
];
```

* * *

### Key Terms
- **ORM**: Object Relational Mapper - allows us to access data from a database using standard objects
- **Controller**: a piece of code that is run for a specific route, whose job it is to get/update the relevant data and return a response to the user
- **Resource**: allows us to control the JSON output of our API
- **CORS**: cross-origin resource sharing - a safety feature that permits browsers to make requests to APIs on different domains

* * *

## Appendix

- [Routing](https://laravel.com/docs/5.6/routing)
- [Controllers](http://laravel.com/docs/5.6/controllers)
- [Requests](https://laravel.com/docs/5.6/requests)
- [Responses](https://laravel.com/docs/5.6/responses)
- [Database Migrations](http://laravel.com/docs/5.6/migrations)
- [Eloquent](http://laravel.com/docs/5.6/eloquent)
- [Route Model Binding](https://laravel.com/docs/5.6/routing#route-model-binding)
- [API Resources](https://laravel.com/docs/5.6/eloquent-resources)