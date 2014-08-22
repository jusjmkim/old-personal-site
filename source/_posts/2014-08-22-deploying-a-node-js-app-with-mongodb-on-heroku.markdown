---
layout: post
title: "Deploying a Node JS app with MongoDB on Heroku"
date: 2014-08-22 09:21:42 -0400
comments: true
categories: 
---
In this blog post, I am going to talk about how I configured Node JS (and Express) to use the node module, Monk, to access MongoDB with on Heroku. It strikes me, at least, as fairly odd that there is very little literature out there (at the time of this writing), so I just wanted to share my implementation of it. To note, I will only be providing the code relevant to this topic.

First, it is important to define our cloud-based database (in this case MongoLab), and we will store it in the variable mongoUri here, as shown below.
``` javascript
var mongoUri = process.env.MONGOLAB_URI ||
    'mongodb://localhost/databaseName';
```

<!-- more -->

While running locally, MongoLab would not be defined, so it would default to the localhost, and for it to be valid, you must create and run that database locally through the Mongo Console. To define Mongolab on Heroku, you have to run the following on your terminal.

``` bash
heroku addons:add mongolab
```

Then, we have to configure Monk, our API layer, on top of Mongo (this helps us connect to Mongo):

``` javascript
var monk = require('monk')
    , db = monk(mongoUri)
    , collection = db.get('collection');
```

At this point, Mongo should be sufficiently set up. Now, to show you how to access it, I have included two examples.

To insert a new entry:
``` javascript
collection.insert({'key': value});
```

To query the database for all entries:
``` javascript
collection.find().success(function(queryResult) {
  client.emit('event', queryResult);
});
```

And of course, it is important to reference the Mongo documentation: http://docs.mongodb.org/manual/
And Heroku's getting started with Node.js: https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction
And here are free courses on Mongo: https://university.mongodb.com/