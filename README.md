# Backbone Tutorial

This is a walkthrough of Rui Molefas's Backbone tutorial:

* [Part 1](http://blog.cloudoki.com/backbone-app-end-to-end-the-basics/)
* [Part 2](http://blog.cloudoki.com/backbone-app-end-to-end-basic-design-pattern/)
* [Part 3](http://blog.cloudoki.com/backbone-app-end-to-end-connecting-to-an-external-api/)

## Backbone basics

Backbone is a model-view-collection framework. Notice that the C here is *collection*, not *controller*. In Backbone, views actually serve as both the views and controllers of typical MVC (model-view-controller) frameworks.

Let's go through each of these pieces in turn.

### Model

Models hold data. You can think of them as classes. So you might have a Car model, or a Movie model, or a Person model. Each of these models can be used to create actual instances of cars, movies, or people.

```
var Car = Backbone.Model.extend(); // creates a new Backbone model
var Movie = Backbone.Model.extend(); // and another
var Person = Backbone.Model.extend(); // and another

var car1 = new Car();
var movie1 = new Movie();
var person1 = new Person();
var person2 = new Person();
var person3 = new Person();
```

#### Storing data on a model instance

We've made one car, one movie, and three people. But none of these actually store any data, so let's make a new instance with some properties.

```
var car2 = new Car({
  color: 'red',
  brand: 'Volvo',
  horsepower: 200
})
```

Now this new instance of a car actually has some data on it that we can use. Note that you can save any arbitrary properties and values in here - just throw it all into an object.

#### Defining what data your model stores

*This sub-section is a work in progress.*

All of our models above are exactly the same, but cars, movies, and people presumably have different kinds of information we want to store for each of them.

So let's go a little more into the "..." we placed in our model definitions above.

```
var Car = Backbone.Model.extend({
  initialize: function(options) {
    ...
  },
  ...
});
```

### Collection

Collections are also classes. A collection instance is simply a glorified array of model instances. Let's define our collections of cars, movies, and people, and create a few instances.

```
var Movies = Backbone.Collection.extend();
var Cars = Backbone.Collection.extend();
var People = Backbone.Collection.extend();

var myMovieLibrary = new Movies();
var karensMovieLibrary = new Movies();
var carsInParkingLotB = new Cars();
var peopleInCanada = new People();
````

These are all fairly boring collections, since they're all empty. Let's create a new collection instance that actually has a few model instances in it.

```
var movie1 = new Movie({
  name: 'Wreck-It Ralph',
  year: 2012
});

var movie2 = new Movie({
  name: 'Frozen',
  year: 2013
});

var myFavoriteDisneyMovies = new Movies([movie1, movie2]);
```

**Side note**: The collection instance will be initialized with the first argument passed. The first argument can be an *array of model instances* (as shown here), *an array of objects* that contain data to encapsulate into model instances, or *one object* that contains data to encapsulate into a model instance. Backbone is smart enough to handle all of these.

### Views

Views are also classes. A view instance will render data from a model or collection instance. Views do everything required to turn your raw data, sitting inertly in your model and collection instances, into actual HTML. They also allow DOM events (such as a user click) to update your data. In other words, they do all the handling of work both from your models to your DOM elements, and vice versa.

```
var MovieView = Backbone.View.extend();
var movieView1 = new MovieView();
```