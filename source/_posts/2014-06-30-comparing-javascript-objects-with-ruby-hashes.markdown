---
layout: post
title: "Comparing Javascript Objects with Ruby Hashes"
date: 2014-06-30 08:37:44 -0400
comments: true
categories: 
---
Having just finished the Javascript track on Codecademy, I felt compelled to comment on at least one aspect of what I learned in the course. Since the two previous languages I learned were Java and Ruby, I found Javascript particularly interesting because it seemed to be a weird mix of the two languages. In this post, I will be looking at the similarities and differences between objects in Javascript and hashes in Ruby. I apologize in advance for any mistakes in this post as while I googled as much as I could to make the information on this accurate, I am still a novice in Javascript.

A comparison of Javascript objects and Ruby hashes came to mind because their syntaxes are extremely similar. One can define a Javascript object through literal notation, as shown below.
<!-- more -->
``` javascript
var obj = {
  key1: "value1",
  key2: "value2"
}
```
At the same time, one can define a Ruby hash through literal notation as well.

```ruby
hash = {
  key1: "value1",
  key2: "value2"
}
```

Literally, the only difference in syntax would be the var in front of obj in the Javascript version. In terms of functionality, the two data structures are incredibly similar as they both store data with key-value pairs. In fact, the syntax to call value1 in both structures is incredibly similar.

In Javascript, it would be:

```javascript
obj["key1"]
```

and in Ruby, it would be:

```ruby
hash[:key1]
```

This difference in syntax hints at one of the subtle differences between these two data structures. In Javascript, the colons are a necessity and simply link corresponding keys and values. In Ruby, however, this syntax implies that the key is a certain data type called a symbol, and in more explicit syntax, the hash can also be declared with hash rockets as such:

```ruby
hash = {
  :key1 => "value1",
  :key2 => "value2"
}
```

For both languages, the key can be data types other than strings or symbols. It is interesting to note that both languages are object oriented languages, and most things are objects in both languages. Thus, it comes as no surprise that hashes in Ruby are also objects. There is a distinction, though, between the construction behind Javascript objects and Ruby hashes since, as the name would imply, Javascript objects represent the general construction behind all objects in Javascript while hashes are just one type of object in Ruby.

The fact that they are both objects is apparent as they can both be declared through constructors. This shows that they are both instances of their respective classes. In Javascript, it would be:

```javascript
var obj = new Object;
```

while in Ruby, it would be:

```ruby
hash = Hash.new
```

It is interesting to note that values stored in Javascript can be called through the dot notation, as shown below.

```javascript
var obj = {
  key1: value
}

obj.key1 === value;
```

This is exactly the syntax to call an instant variable through a reader method in Ruby (and many other object oriented languages). However, these are not instance variables, so you are not using reader methods. Ultimately, these are two very different data types, but they both store data and have syntaxes so similar that I thought it would be worth mentioning. I'm also not entirely sure if the difference between the two is significant, so upon future research (and my remembering to update this post), I will update this information accordingly.


Additional Resources

http://blog.flatironschool.com/post/67666573907/javascript-vs-ruby

http://stantona.github.io/blog/2012/12/12/a-tale-of-two-object-models-javascript-and-ruby/