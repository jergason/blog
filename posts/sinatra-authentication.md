---

title: Sinatra Authentication Roundup Part 1
date: '2011-01-23'
tags: [sinatra, ruby, authentication]
categories: coding
permalink: /post/2888090008/sinatra-authentication-roundup-part-1

---

I am working on a small Sinatra application for a client that needs to
authenticate users. I found several different authentication solutions for
Sinatra, and this should be the first in a series that looks at them. (*edit:* NOPE, only one)

The first one I looked at was
[sinatra-authentication](https://github.com/maxjustus/sinatra-authentication "sinatra-authentication").
Get with `gem install sinatra-authentication`{.ruby} or by including it
in your Gemfile and running `bundle install`{.ruby}. This gem provides
you with a User object that supports DataMapper, MongoMapper, Mongoid,
Sequel, and Rufus-Tokyo as your ORM. It handles authentication and
supports simple permissions, which is nice.

It uses Rack::Session::Cookies to store authenticated users in the
session object, and wins the prize for having the best default secret
key or password:

    use Rack::Session::Cookie, :secret => 'A1 sauce 1s so good you should use 1t on a11 yr st34ksssss'

The
[README](https://github.com/maxjustus/sinatra-authentication/blob/master/readme.markdown "README")
on GitHub is very complete. Following it I was able to install the gem,
require it, run `DataMapper.auto_migrate!` to change my database schema,
and it was up and running. Kudos for easy setup.

sinatra-authentication is fairly opinionated in how you should handle
authentication. It adds several routes with corresponding views to your
application, which makes it extremely simple to start using if you just
want to go with the defaults. There is support for overriding the
default views, but none so far for changing the added routes. It adds
the following routes:

-   get '/login'
-   get '/logout'
-   get '/signup'
-   get/post '/users'
-   get '/users/:id'
-   get/post '/users/:id/edit'
-   get '/users/:id/delete'

The User object includes a `permission\_level` attribute
that you can use to implement permissions. By default it is set to 1
when new users are created. Admin users are -1. There are some nice
helper methods to check if users are administrators or not, and to see
if a user is logged in. It was plenty to add the simple permissions I
needed for my app.

Overall, I was pleased with sinatra-authentication. The User model and
the helper methods are great. My one hangup is how opinionated it is
about the routes and actions it provides. It was overkill for my
project, so I had to fork the gem and remove some un-needed routes and
tweak some of the remaining ones. It was still a great base to build off
of. I also contacted the author of the gem, Max Spransy, with a few
questions. He responded quickly and thoroughly, and seems like a great
guy.
