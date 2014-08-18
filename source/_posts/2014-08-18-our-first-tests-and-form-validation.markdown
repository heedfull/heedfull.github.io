---
layout: post
title: "Our first tests and form validation"
date: 2014-08-18 17:43:28 +0100
comments: true
categories: FeedToShare
---
[Last time]({% post_url 2014-07-14-getting-started-creating-a-scaffold %}) we added our feeds object to our Ruby on Rails app. This time we're going to add some form validation to our feeds forms. Since we will be using test driven development style, we should write the tests before writing the code.
<!--More-->
First off lets just run the tests that were created for us.
	rake spec

We are going to create integration tests. They test the end to end process. Let's create folder to hold those test. The -p option on the mkdir means that it will make all folders along the way. In this case the ```features``` folder and the ```feeds``` folder within that.
	mkdir -p spec/features/feeds

Let's create a spec in that folder. If you are using [Subime Text](http://www.sublimetext.com/) then I would highly recommend the [AdvanceNewFile](https://github.com/skuroda/Sublime-AdvancedNewFile) package. Simply press ```cmd``` ```alt``` + ```n```. You can then type in the path with tab auto-complete goodness.

Here is our intial first test.

{% highlight ruby %}
{% github_sample /heedfull/FeedToShare/2accd322214d9fc38418289b597670a267511000/spec/features/feeds/create_spec.rb %}
{% endhighlight %}

Can you see what I mean about our test being done in a specification kind of style.
We are saying that this test is for Creating Feeds and we describe what we want the app to do. In this case, check that what we entered as the name of the feed is succesfully displayed once the feed is created. This test is just testing what was given to use by the scaffold.

Let's check that it works. We do this by running rspec directly and passing in the name of the test that we are interested in.
	rspec spec/features/feeds/create_spec.rb

This should run successfully and you should get something like this in your terminal window

{% img center /images/successful_test.png %}

Let's actually do some test driven development. Lets add another test to this spec. We want the app to display an error when a name isn't entered when trying to create a feed record.

{% github_sample_ref /heedfull/FeedToShare/0da4cfbbba63fe4f262c146deae9fef595b211ce/spec/features/feeds/create_spec.rb %}
{% highlight ruby %}
{% github_sample /heedfull/FeedToShare/0da4cfbbba63fe4f262c146deae9fef595b211ce/spec/features/feeds/create_spec.rb 13 30 %}
{% endhighlight %}

This test is very similiar to our first one. Finally we are using the Feeds collection to check that the feed without a Name is not created.

Lets run our tests again. It should fail, but that's alright it's what we were expecting as we hadn't written any code to stop a feed from being created without a name.

{% img center /images/OurFirstTests_Failure.png %}

Now lets add the code that does the validation. There is a whole [guide to adding validations in Ruby](http://guides.rubyonrails.org/active_record_validations.html) the first example in the guide is of the type that we are going to use. To do this we add it to our model. It's our model that interfaces with the database, so it makes sense to put the validation in this level of the application.

{% github_sample_ref /heedfull/FeedToShare/0da4cfbbba63fe4f262c146deae9fef595b211ce/app/models/feed.rb %}
{% highlight ruby %}
{% github_sample /heedfull/FeedToShare/0da4cfbbba63fe4f262c146deae9fef595b211ce/app/models/feed.rb %}
{% endhighlight %}

This additional line will make our test pass. In the next post I will create another test and discuss the importance of not repeating yourself when it comes to coding.
