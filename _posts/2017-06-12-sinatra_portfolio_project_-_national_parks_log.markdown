---
layout: post
title:  "Sinatra Portfolio Project"
date:   2017-06-12 18:11:21 -0400
---


Finished my sinatra portfolio project! I decided to build a web app for logging National Park visits -- park name, location, dates visited, sites/trails visited, notes for next visit. I found setting up the app itself fairly simple having just completed Fwitter, so the bulk of the time was spent learning about using Bootstrap and Heroku. The Bootstrap sections on [CSS](https://getbootstrap.com/css/) and [Components](https://getbootstrap.com/components/) were extremely helpful, as well as [Getting Started on Heroku with Ruby](https://devcenter.heroku.com/articles/getting-started-with-ruby#introduction) and [Get Started with Sinatra on Heroku](http://www.sitepoint.com/get-started-with-sinatra-on-heroku/) when it came time to deploy to Heroku. 

These are some things I learned that I had to do a bit more digging for:
* I needed a `config/database.yml` file in addition to `config/environment.rb` that defines an adapter, database, host, pool and timeout for development and then all of those things plus a url for production
* I needed to move the sqlite3 gem into a development group once I wanted to deploy to Heroku, since I was getting an error that said they're incompatible. I did that by removing my existing Gemfile.lock, adding `group :development do
  gem "sqlite3"
end` to the Gemfile and re-running `bundle install`
* I added the gem 'pg', which is the Ruby interface to the {PostgreSQL RDBMS}[http://www.postgresql.org/]
* You can run [Rake tasks](https://devcenter.heroku.com/articles/rake) on Heroku, e.g. `heroku run rake db:migrate` 
* I kept getting the following error running `heroku ps`:
`=== web (Free): bundle exec rackup config.ru -p $PORT (1)
web.1: crashed 2017/06/12 11:37:20 -0400 (~ 8m ago)` 
and eventually fixed it by scaling the dynos to 0 using `heroku ps:scale web=0` and then back up to 1 with `heroku ps:scale web=1`

I found a lot of those solutions through Stack Overflow and various blogs, so I hope that information is useful to someone else working on their project! You can view my app [here](https://sinatra-park-portfolio.herokuapp.com/). I'm satisfied with it, but in learning about the options for CSS customization that Bootstrap allows I realized how much more I could add to what's currently a very simple web app. For now I think it's enough that I know those tools exist and feel confident I could implement them if time weren't a factor in finishing this project, since I did use a few of them in building my Sinatra app. 
