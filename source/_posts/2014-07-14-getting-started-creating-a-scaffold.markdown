---
layout: post
title: "Getting Started, creating a scaffold"
date: 2014-07-14 19:56:32 +0100
comments: true
categories: FeedToShare
published: true
---
This is a continuation of the the [first post][FirstPost] on the building of a [FeedToShare](https://github.com/heedfull/FeedToShare). In that post we created the app and installed some gems that we are going to need for testing it.

In this post we are going to create or first entity and all the accompaning files including our tests.

What we need to decide on first is our data model. Whilst I have a very specific problem in mind I'm trying to develop this web app so that it is generic enough that it could be used for other feeds, or even multiple feeds. The best starting place is that we will need a feed object.

We now need to decide what properties this object will need. Here's my initial crack at it. These can of course be added to and changed.

* Feed Name
* Feed Url

To do this we are going to uses the ```generate scaffold``` command. We'll need to put in the name of the object and it's attributes as well as the data types we want them to have.
	rails generate scaffold feed name:string url:string 

Rails will go off an create lots of things for us. Here is the full list 
	invoke  active_record
	create    db/migrate/20140726171324_create_feeds.rb
	create    app/models/feed.rb
	invoke    rspec
	create      spec/models/feed_spec.rb
	invoke  resource_route
	route    resources :feeds
	invoke  scaffold_controller
	create    app/controllers/feeds_controller.rb
	invoke    erb
	create      app/views/feeds
	create      app/views/feeds/index.html.erb
	create      app/views/feeds/edit.html.erb
	create      app/views/feeds/show.html.erb
	create      app/views/feeds/new.html.erb
	create      app/views/feeds/_form.html.erb
	invoke    rspec
	create      spec/controllers/feeds_controller_spec.rb
	create      spec/views/feeds/edit.html.erb_spec.rb
	create      spec/views/feeds/index.html.erb_spec.rb
	create      spec/views/feeds/new.html.erb_spec.rb
	create      spec/views/feeds/show.html.erb_spec.rb
	create      spec/routing/feeds_routing_spec.rb
	invoke      rspec
	create        spec/requests/feeds_spec.rb
	invoke    helper
	create      app/helpers/feeds_helper.rb
	invoke      rspec
	create        spec/helpers/feeds_helper_spec.rb
	invoke    jbuilder
	create      app/views/feeds/index.json.jbuilder
	create      app/views/feeds/show.json.jbuilder
	invoke  assets
	invoke    coffee
	create      app/assets/javascripts/feeds.js.coffee
	invoke    scss
	create      app/assets/stylesheets/feeds.css.scss
	invoke  scss
	create    app/assets/stylesheets/scaffolds.css.scss

It's created a migration, a script that will tell the database what to do. In this case it's going to create a table for our feeds. Rails also creates a model and a spec for that model for our feeds object. It created a route. This tells rails what to do with requests, where to direct them. It created a controller, this will hold what is sometimes called business logic. This is where we will define the functionality for our feeds objects. It then created some views in erb (Embeded Ruby). These are templates that are used for display our data and interacting with it. It also created test for all these. Finally it created some helpers, coffee script for interactivity and scss for styling.

Next we need to run in those database migrations.
	rake db:migrate

This has created our feeds table in our development environment. We also need to do this for our test environemt. This is the database that our tests will run against
	rake db:migrate RAILS_ENV=test

Let's add and commit those changes so that if we need to, we can go back to this point.
	git add .
	git commit -m "Scaffold for feeds object"

Let's see what has been created for us. Ruby on Rails has a built in server. To fire it up just run
	rails server

Now when you browse to http://localhost:3000 you will see the standard Welcome to Rails message. If you go to http://localhost:3000/feeds you can see what has been created for us. 

{% img center /images/FeedsScaffold.png %}

Lets change our app so that this index page is the default page that is loaded. We do this by adding root command to our config.rb file

{% highlight ruby %}
{% github_sample /heedfull/FeedToShare/22acab2805a203c7b995b780f06882c5ba8eee5c/config/routes.rb 2 2 %}
{% endhighlight %}

And commit those changes
	git add config/routes.rb
	git commit -m "Changing default page"

There you have it. Our first object in our Rails app. Next time we'll create our first test and add some form validation.

[FirstPost]: [{% post_url 2014-07-05-introducing-feedtoshare %}]