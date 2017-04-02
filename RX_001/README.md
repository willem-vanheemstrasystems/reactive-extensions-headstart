### README.md

# RX_001

Based on 'Functional Programming in Javascript' at http://reactivex.io/learnrx/

 Functional programming provides developers with the tools to abstract common collection operations into reusable, composable building blocks. You'll be surprised to learn that most of the operations you perform on collections can be accomplished with five simple functions (some native to JavaScript and some included in the RxJS library):

1. map
2. filter
3. concatAll
4. reduce
5. zip

Here's my promise to you: if you learn these 5 functions your code will become shorter, more self-descriptive, and more durable. Also, for reasons that might not be obvious right now, you'll learn that these five functions hold the key to simplifying asynchronous programming. Once you've finished this tutorial you'll also have all the tools you need to easily avoid race conditions, propagate and handle asynchronous errors, and sequence events and AJAX requests. 

In short, ***these 5 functions will probably be the most powerful, flexible, and useful functions you'll ever learn***.

## Working with Arrays

The Array is Javascript's only collection type. Arrays are everywhere. We're going to add the five functions to the Array type, and in the process make it much more powerful and useful. As a matter of fact, Array already has the map, filter, and reduce functions! However we're going to reimplement these functions as a learning exercise.

This section will follow a pattern. First we'll solve problems the way you probably learned in school, or on your own by reading other people's code. In other words, we'll transform collections into new collections using loops and statements. Then we'll implement one of the five functions, and then use it to solve the same problem again without the loop. Once we've learned the five functions, you'll learn how to combine them to solve complex problems with very little code. The first two exercises have been completed in advance, but please look them over carefully!

### Traversing an Array

Exercise 1:  Use ***for*** to print all the names in an array

```javascript
function(console) {
  var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"],
  counter;

  for(counter = 0; counter < names.length; counter++) {
    console.log(names[counter]);
  }
}
```

Exercise 2: Use ***forEach*** to print all the names in an array

```javascript
function(console) {
  var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"];

  names.forEach(function(name) {
    console.log(name);
  });
}
```
***NOTE***: Notice that forEach lets us specify what we want to happen to each item in the array, but hides how the array is traversed.

### Projecting Arrays

Applying a function to a value and creating a new value is called a ***projection***. To project one array into another, we apply a projection function to each item in the array and collect the results in a new array.

Exercise 3: Project an array of videos into an array of {id,title} pairs using forEach()

For each video, add a projected {id, title} pair to the videoAndTitlePairs array.

```javascript
function() {
	var newReleases = [
		{
			"id": 70111470,
			"title": "Die Hard",
			"boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
			"uri": "http://api.netflix.com/catalog/titles/movies/70111470",
			"rating": [4.0],
			"bookmark": []
		},
		{
			"id": 654356453,
			"title": "Bad Boys",
			"boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
			"uri": "http://api.netflix.com/catalog/titles/movies/70111470",
			"rating": [5.0],
			"bookmark": [{ id: 432534, time: 65876586 }]
		},
		{
			"id": 65432445,
			"title": "The Chamber",
			"boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
			"uri": "http://api.netflix.com/catalog/titles/movies/70111470",
			"rating": [4.0],
			"bookmark": []
		},
		{
			"id": 675465,
			"title": "Fracture",
			"boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
			"uri": "http://api.netflix.com/catalog/titles/movies/70111470",
			"rating": [5.0],
			"bookmark": [{ id: 432534, time: 65876586 }]
		}
	],
	videoAndTitlePairs = [];

	newReleases.forEach(function(newRelease) {
	  videoAndTitlePairs.push({"id": newRelease.id, "title": newRelease.title});
	});

	return videoAndTitlePairs;
}
```

All array projections share two operations in common:

1. Traverse the source array
2. Add each item's projected value to a new array

Why not abstract away how these operations are carried out?

Exercise 4: Implement map()

To make projections easier, let's add a ***map()*** function to the Array type. Map accepts the projection function to be applied to each item in the source array, and returns the projected array.

```javascript
Array.prototype.map = function(projectionFunction) {
  var results = [];
  this.forEach(function(itemInArray) {
    results.push(itemInArray + 1);
  });
  return results;
};

// JSON.stringify([1,2,3].map(function(x) { return x + 1; })) // map function returns [2,3,4]
```

