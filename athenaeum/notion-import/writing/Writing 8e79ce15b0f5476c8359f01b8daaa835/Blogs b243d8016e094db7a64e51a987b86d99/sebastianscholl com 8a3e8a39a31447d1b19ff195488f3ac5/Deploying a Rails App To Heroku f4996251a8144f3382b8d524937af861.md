# Deploying a Rails App To Heroku

Created: August 25, 2021 12:15 PM
Location: New York City, United State of America
Original Publish Date: March 25, 2016
Tags: Tech & Code

- [This link is to the Index Card Language Learning App I designed and built last week, which guided this article.](https://stark-inlet-84675.herokuapp.com/)

Heroku is easy to use. So easy that it feels like magic. It's as though all you must do is put the round peg in the round hole. As long as you have the round peg everything goes smoothly.

For about six hours last Wednesday, I thought I had the round peg. Turns out that I didn't! And because of that misunderstanding, I was led down a rabbit hole of hinkering-and-tinkering with my app so that it could deploy. As with so many debugging adventures, the *right* answer (a working solution) ended up being simple edits to only two lines of code and several commands run in the terminal. Here's some of what I learned in the process.

# **Variables on Heroku - ENV["YOUR_KEYS"]:**

When we create a new Rails app, *secret_key_base*'s are created for the development, test, and production environments. These keys can be found in the *secrets.yml* file that's located in the *config/* directory. The keys are unique, and used to verify the integrity of signed cookies. Looking at the example below, you can see that the keys are explicit in development and testing environments. However, the production key gets accessed as an environment variable.

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-24-at-10-03-02-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-24-at-10-03-02-pm.png)

In the process of following this [wonderfully detailed deploying Rails on Heroku guide](https://devcenter.heroku.com/articles/getting-started-with-rails4), I pushed the app to Heroku and was immediately given the error:

> Missing 'secret_key_base' and 'secret_token' for 'development' environment, set these values in config/secrets.yml
> 

The reason I got this error was simple. I hadn't allowed my *secrets.yml* file to be pushed up as to protect the API keys it stored. The keys generated for *test* and *development* aren't sensitive. And as seen above, the *production* key is referenced as an environment variable. So, as long as I could store my API keys somewhere else, there was no harm in pushing up the secrets file. I did just that, and a new error popped up.

> Missing 'secret_key_base' and 'secret_token' for 'production' environment, set these values in config/secrets.yml
> 

Heroku provides a simple dashboard in *Settings* that lets you manage keys. These keys are called Config Variables but treated as environment variables. They can be accessed by your application when it's running on Heroku as an environment variable, and they are protected. This is also the safe environment in which to store API keys.

**DO NOT copy the SECRET_KEY_BASE that Heroku generates for you and paste it into your secrets.yml file.** That is **not** where Heroku will look for the production *secret_key_base -* which makes sense because a) there would be no point for Heroku to look in a file for information that it has stored in Config Variables, and b) even a relative path in *secrets.yml* would just point back to Heroku's own environment.

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-24-41-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-24-41-pm.png)

Instead, Heroku must access necessary keys during configuration. When and where should that happen? In *config/environments/production.rb*.

When the production environment is configured, *production.rb* holds a list of settings that get defined - cache behaviors, database setting, ect... It is also where you can give the relative paths to environment variables. In my case, I only had keys for a Google Translate API and the *secret_key_base*. The picture below shows how I ended up configuring them.

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-39-58-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-39-58-pm.png)

This way, upon configuration, the server is told to look within its own environment for the variables it has stored. These variables get set in *Settings -> Config Variables* either manually (as I put in the Google Translate API key) or automatically by Heroku.

# **Sqlite3 to Postgres**

Heroku doesn't support sqlite3. So if you develop using sqlite3, you must convert your database to Postgres before deploying. This process may require that you refactor certain methods, being that some of the ActiveRecord query methods - .group(), for example - are not compatible with Postgres. Luckily, I had no syntactic conflicts. However, take a read through this [Wiki article for some extra information on converting databases to Postgres.](https://wiki.postgresql.org/wiki/Converting_from_other_Databases_to_PostgreSQL)

Let's imagine that you're in my shoes. After having successfully complied and pushed an app to Heroku, you're being returned an error page when opening the site (the actual error message was contextless). The page is just telling you that something went wrong. If you've yet converted your database to Postgres, that is probably what's wrong! Here are steps to take.

Firstly, take the sqlite3 gem out of your *Gemfile* and include the postgres gem in its place. Run *bundle install* in your terminal, and double check that Postgress was included. Bundle will take care of the versioning (if necessary).

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-52-14-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-52-14-pm.png)

We are able to run commands on Heroku by prefacing them with *heroku run*. Even though we've transition our database over to Postgres, we've yet to migrate it - meaning that all of our tables and seed data is missing. Thus, we need to run the following commands:

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-56-51-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-56-51-pm.png)

![https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-57-08-pm.png](https://mynamessebastian.files.wordpress.com/2016/03/screen-shot-2016-03-25-at-12-57-08-pm.png)

Only run the seed command if you have seed data. Once this is done though, your data will have been configured up on Heroku! And, hopefully, your site is up and running...

[If you're curious as to what the project I built was, here's some info. It's called *Indy - A Language Learning Tool for Slow Learners*. It offers easy text translation and generates index cards for you to practice languages with. Feel free to make and account - and apologies for any bugginess!](https://stark-inlet-84675.herokuapp.com/)

![https://mynamessebastian.files.wordpress.com/2016/03/indy_the_sloth-a6c6e0fe354699fbfe887acbbb699e21d617b6a2704934f717af5009ccef49cb.png](https://mynamessebastian.files.wordpress.com/2016/03/indy_the_sloth-a6c6e0fe354699fbfe887acbbb699e21d617b6a2704934f717af5009ccef49cb.png)