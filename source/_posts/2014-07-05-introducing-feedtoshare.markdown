---
layout: post
title: "Introducing FeedToShare"
date: 2014-07-05 23:39:58 +0100
comments: true
categories: FeedToShare
---
This is the first in a series of post detailing the development of [FeedToShare](https://github.com/heedfull/FeedToShare). Feed to Share is a Ruby on Rails web app design to consume and RSS feed of podcasts episodes and make a torrent file for each of those episodes. It then goes onto seed those torrents and produces an RSS feed of the torrent episodes to allow other to automatically download the torrents and the episodes. 
<!-- More -->

##Problem##
[Freedomain Radio](https://freedomainradio.com/) is the &ldquo;number 1 philosophy podcast&rdquo;. They do not have advertising or sponsors because the host of the show, Stefan Molyneux, believes that his listeners' time is too important. He relies solely on donations to keep his work going. He is current getting 900GB of downloads a month, and that sort of bandwidth doesn't come cheap. My goal is to build a system that makes it easy for his users to listen to the podcast whilst reducing the bandwidth that he uses with his web hosting .

##Solution##
Stefan talked about torents but said that they were too difficult for the average user. I want to build a system that downloads a copy of the episode, creates a torrent and starts seeding that episode. FeedToShare is the name that I've given for that system. It would then create an RSS feed of the torrents allowing some to subscribe to automatically download the new episodes. Once this is up and running I would like to create an Android App based on the [libtorrent library](https://github.com/rakshasa/libtorrent/tree/master). This would allow listeners to share the episode amongst themselves and eventually listen to them in the app.

I've decided to build [FeedToShare](https://github.com/heedfull/FeedToShare) as a web app using Ruby on Rails. Ruby on Rails gives me the ability to develop a web front end for managing the torrents easily. Ruby on Rails also has the capability to spin of Ruby processes, these will be used to interact with [Transmission](http://www.transmissionbt.com/) that I am using to do the torrent creating and seeding.

I plan to develop this app in the open. All the code is [shared on github](https://github.com/heedfull/FeedToShare) and I will be blogging about all that I am doing here, in the hope that it might help other who want to build their own apps. So let's get started.

First want to make sure you have your development environment setup. There is a [guide](http://rubyonrails.org/download/) on their website how to do that. If you're on a mac I would recommend using [rbenv](https://github.com/sstephenson/rbenv), so that you can use different versions of Ruby on your machine, really useful if you're working on a few different projects or using hosts with different versions of Ruby.

Now that have rails installed you can create a new rails applicaiton

	rails new FeedToShare

I'm going to be using [git](http://www.git-scm.com/), [github](https://github.com/) and [git flow](https://github.com/nvie/gitflow). If you haven't tried git flow, I would highly recommend it. I know it's going to make managing this project much eaiser. This [video walkthorough](http://vimeo.com/16018419) really help sell it to me.

First go into the directory that has been created
	cd FeedToShare
Initialise a new repo 
	git init
And setup git flow in that repo
	git flow init

I then went and created a new repo on github and added this repo as the origin for our local repo. Then add the files This will make it easy to push and pull and changes and share the code with others.
	git remote add origin https://github.com/heedfull/FeedToShare.git
	git add .
	git commit -m "Initial commit of rails application"
	git push origin develop

With the git flow model you will be doing most of your work on the develop branch or on feature branches. The master branch is reserved for when you actually release the software. It should contain the code that is actually deployed to your production environment. With this in mind I change the default branch in github to be the develop branch.

I'm going to be developing this web app using Test Driven Development. If you haven't heard of the term I thoroughly recommend that you do some research on it. I've started using it on a project that I'm developing at work and can't believe I didn't give it a try sooner. It's great at making you focus on what it is that you are trying to achieve when writing a piece of functionality. It forces you to break down your application into little chunks and develop each chunk one at a time.

I'll be using [rspec](http://rubydoc.info/gems/rspec-rails) and [capybara](http://jnicklas.github.io/capybara/) to write our tests and execute them. Rspec lets you write the tests in a kind of specification way. You tell the application how you want it to behave before you go and code that behaviour. Capybara acts as a mock browser it will test that certain things are on the page. I'll go into more details later when I actually write some tests.

To set these up you need to add them to the Gemfile. Were going to require rspec-rails in our development and test environment and capybara in our test environment.

```ruby
group :development, :test do
	gem 'rspec-rails', '~> 2.0'
end

group :test do
	gem 'capybara', '~> 2.1.0'
end
```

We then run ```bundle``` to go off and actually install those Ruby gems.

Next we then need to initialise rspec in our app. This will create few files needed by rspec and also the specs directory.
```bash
bin/rails generate rspec:install
```

In the spec/spec_helper.rb file we need to tell rpsec to use capybara. We do this by adding the following line:
```ruby
require 'capybara/rspec'
```

The final step in getting this setup is to actually generate the binstubs in our applicaitons bin folder. These are [wrapper files  for the actually binary executables](https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs).
```bash
bundle binstubs rspec-core
```

Because we are using specs rather than tests we can git rid of the directory locally and in git.

```bash
rm -rf test
git rm -rf test
```

<!--
bundle
bin/rails generate rspec:install
st .zsh_history
bundle binstubs rspec-core
git status
git add .
git commit -m "Adding rspec and capybara so can do test driven development"
git push
ls
rm -rf test
git rm -rf test
git status
git commit -m "Removed test directory as no longer needed"
git push
git push develop origin
git push origin develop
ping 192.168.192.1-->