Exercises
===============

If you haven't done so yet, read the [overview page](https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview). Doing the exercises before reading the overview surely leads to <a href="http://omgface.com/evil/evil%20baby7.jpg" target="_blank">death</a>...

<h2 id="introduction">Introduction</h2>
Below are exercises to familiarize you with the major topics in Rails. Many of the exercises build on the previous one's so it's recommended to go in order. If you would like to contribute, please do so by forking and running a pull request. 

**Estimated time to complete is 2 hours**

OK cool. Let's get started!

<h2 id="rails-setup">Rails setup</h2>

Before we get started let's get setup with Rails. Most of you should already have Rails installed on your computer. If you don't then follow <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book#sec-1_2" target="_blank">this</a> guide. 

Now, let's create a new app by typing:
```sh
$ rails new practice_app -T
``` 
This will create a new Rails app within whatever directory you are currently in. (I recommend doing it from the Desktop directory). The "-T" is short for "--skip-test-unit", which bypasses the creation of the Rails default test unit. We will be writing own tests in rspec, so we don't need it. 

That was easy. Now let's write our first test!

<h2 id="rspec--testing">Rspec & Testing</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#rspec--testing" target="_blank">Rspec & Testing overview</a>

OK, our first tests... I know what you're thinking, "Shit! Uggghhh! Fudge!! Tests... grrrr". Yes, indeed. But tests are our friends. So instead of cursing tests we will welcome them by getting our test environment set up like a <a href="http://ratchetreview.files.wordpress.com/2013/02/481.jpg?w=490" target="_blank">G</a>.

First things first, add this to your Gemfile (if you have yet to create a new rails project follow the directions in <a href="#rails-setup">setup</a> above).
```ruby
.
.
group :test, :development do
  gem 'rspec-rails'
end
```
Then run:
```sh
$ bundle
```
Then initialize RSpec with:
```sh
$ rails generate rspec:install
```

OK, cool. We now have Rspec installed. Let's write a unit test for Users. "But we haven't created users yet! How will we test them?". Right, that's the point of TDD - to write tests first. So let's write the failing tests for a Users model that doesn't exist. Then we'll get the tests to pass in the next section.

Start by creating a "models" folder within our newly created "spec" folder. Then create a "user_spec.rb" file. Like so: ``` /spec/models/user_spec.rb``` Open this file and add the following code: 

```ruby
require 'spec_helper'

describe User do

  subject { User.new(username: "Me", password: "iheartrails", email: "email@email.com") }

  it { should be_instance_of User }
  its (:username) { should == "Me" }
  its (:password) { should == "iheartrails" }
  its (:email) { should == "email@email.com" }

end
```
OK, great! Our first test is complete. You are officially a testing masta'! We're done here, you can go home now. Seriously though, what the hell is really going on? Well, we first create a subject which is a new user. We then test that this subject has certain attributes. In this case we want our user to have a "username", "email", and "password". So we check the presence and value of each of these. If these tests pass it means we built our user correctly and the fan blades are clean... (think about it). 

To run this test we go to the console and type:
```sh
$ bundle exec rspec
```

The tests should all fail... "Uhhh, no they don't. Nothing works. You fool!!". Aha, yes, of course. You are getting this error:
```sh
$ .../user_spec.rb:3:in `<top (required)>': uninitialized constant User (NameError)
```
This is because we have yet to create our users model. So let's create the model now. Run this command and type 'n' if(when) you get a conflict (this conflict is caused because rails is auto-generating an rspec file for our model):
```sh
$ rails g model User
```
Now run ```$ bundle exec rspec```. Tests failing? Of course they are. And if they aren't then you f*ed up. Your bad, not mine! Just kidding. If that didn't work I would start from scratch and try it all again. If it still doesn't work then <a href="http://lmgtfy.com/?q=My+rspec+thingy+don%27t+work" target="_blank">Google</a> the errors you're receiving. 

OK!! We got our first tests written! This Rspec stuff is easy! Actually it really isn't that bad. It reads like English and makes a lot of sense.

So let's get the tests passing by creating our Models and Migration in the next section.

<h2 id="models--migrations">Models & Migrations</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#models--migrations" target="_blank">Models & Migrations overview</a>

OK, so I'm assuming you did the above exercise. If you didn't then run this command from you rails app:
```sh
$ rails g model User
```
This will create a "user" model in ```/app/models/``` and a migration file in ```db/migrate```. Let's first start with the migration file. 

Open the migration file and add the following attributes: "username", "email", "password". The migration file should look like:
```ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.string :password
      
      t.timestamps
    end
  end
end
```
Now run your test with ```$ bundle exec rspec```. The tests are all still failing. So we have more work to do. 

First let's migrate the db with:
```sh
$ rake db:migrate
```
Next we must prepare our test database with:
```sh
$ rake db:test:prepare
```

Now run our tests and.... The shit works. F* YEAH!!!!!!!! Passing tests and a user model! Done and done. 

So what did we just do? Here's the simple list:
- We generated a model and migration file with ```rails g model User```
- We then added our attributes to the migration file just as we did in Sinatra
- We added our attributes to the attr_accessible line in our User model so we can write to our user model

Really not that difficult, was it? Maybe so, maybe not. Either way we did successfully create a migration and model and got our tests from section 1 working. Heck yeah! Now lets get a controller set up. 

<h2 id="controllers">Controllers</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#controllers" target="_blank">Controllers overview</a>

So we now have a users model. Next let's create a way to make new users from the web. First we'll need to create a users controller, but before we do this let's check out what routes are available to us. Run ```$ rake routes``` to see what routes are available. At this point there shouldn't be any. Why? Because we haven't created any quite yet. 

Let's run another test. Start the rails server with ```$ rails s```. Now navigate to ```localhost:3000```. We've got this default home page. Cool. Now navigate to ```localhost:3000/users/new```. This is rails default url for creating new users given we have "users" model. 

What's the error message you get when you hit this url? It should look like this:
```
No route matches [GET] "/users/new"
```

Why's that? Because we haven't created the route for this url yet. So let's now create routes for our users model. To do this open the ```config/routes.rb``` file. In this file let's add the below:

```ruby
PracticeApp::Application.routes.draw do
  resources :users # This is the line to add
  
end
```

Now run ```$ rake routes``` again. This time our routes should look like this:

```
    users GET    /users(.:format)          users#index
          POST   /users(.:format)          users#create
 new_user GET    /users/new(.:format)      users#new
edit_user GET    /users/:id/edit(.:format) users#edit
     user GET    /users/:id(.:format)      users#show
          PUT    /users/:id(.:format)      users#update
          DELETE /users/:id(.:format)      users#destroy
```

Now navigate back to our users/new page. ``` localhost:3000/users/new```. This time we should be receiving a different error:
```
uninitialized constant UsersController
```

OK, cool. So we have our routes setup but our controller has no action 'new'. It's time we setup our controller. To do so we'll navigate to our ```app/controllers``` folder and create a new file called "users_controller.rb". Add the below to the file:

```ruby
class UsersController < ApplicationController 

end
```

We now have a users controller shell setup, but still no 'new' action. To get this action we add the following:

```ruby
class UsersController < ApplicationController 
 
  def new
  end
  
end
```

Now navigate to ```localhost:3000/users/new``` one more time. The new error we now get is:
```
Missing template users/new, application/new....
```

OK, cool! We have a controller setup, now we need a template (or view) for our ```users/new``` page. Let's get it done in the next section.

<h2 id="views">Views</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#views" target="_blank">Views overview</a>

Picking up where we left off in the controllers exercise we are going to create a signup page for the url ```localhost:3000/users/new```. To do this we first need to add a ```users``` folder to ```app/views```. The path for this folder should look like ```app/views/users```. 

Great. Now let's create a view for the signup page. To do so add a file called ```new.html.erb``` to ```app/views/users```. NOTE: For those making the shift from Sinatra to Rails you will note here that our html files are suffixed with ```.html.erb```. As you remember, in Sinatra files were simply suffixed with ```.erb```. This is a convention in rails. Both render the same outcome.

Before we test this page in the browser let's add a little text. Something like this should work fine:

```html
<h1>This is a the user signup page!</h1>
<p>Ahhhhh!!!!</p>
```

Now navigate to ```localhost:3000/users/new```. Did it work? Of course it did!! Woohoo! Party time! We now have "Models and Controllers and Views, OH MY!!!"

You are officially a Rails rockstar. You can now retire....

OK, now that you've retired, let's do some more work. :P  First things first, we can't actually sign any users up. So let's jump to the next section where we'll add a signup form using the Rail's helper ```form_for```.

<!-- create a static pages index page, a signup page, and a show page -->

<h2 id="forms">Forms</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#forms" target="_blank">Forms overview</a>

Alrighty then. Continuing on. We left off with this very stylish and sleek ```users/new``` page which lacked a form for actually signing up. Our next task is to use ```form_for``` to create the form. To do so let's add the following to ```new.html.erb```:

```erb
<h1>Sign up</h1>
<%= form_for @user do |f| %>
  <%= f.label :username %>
  <%= f.text_field :username %>
  <%= f.label :email %>
  <%= f.email_field :email %>
  <%= f.label :password %>
  <%= f.password_field :password %>
  <%= f.submit "Signup!!" %>
<% end %>
```

Now navigate to ```localhost:3000/users/new```. You should receive this error:
```
undefined method `model_name' for NilClass:Class
```

Why's this? Well, we didn't actually pass in a user to the form_for. So let's go to our controller and add the following:
```ruby
def new
  @user = User.new
end
```

Now refresh the page. Violá! Form magic!

So we now have a form for signing up. Let's test this bugger out and make sure it works (spoiler alert - it doesn't work). 

You got an error, right? And it looks like:
```
The action 'create' could not be found for UsersController
```

We've seen a similar error, remember? It was in the controller's exercise. Right after we created our routes we ran into the same problem with the ```new``` action. To get this to work we will do what we did then, add a ```create``` action to ```users_controller.rb```:
```ruby
def new
  @user = User.new
end

def create
end
```

Refresh the page where we had the error. A new error should occur:
```
Missing template users/create...
```

So we have no template ```users/create```. That's actually correct. We don't need a template as create is a post. So what we'll do here is actually create the user in our ```create``` method and then redirect to a profile page (```users/:id```) after the user has been saved.

To do this we add the following to ```users_controller.rb```:

```ruby
def create
  @user = User.new(params[:user])
  redirect_to @user if @user.save
end

def show
  @user = User.find(params[:id])
end
```

NOTE: we are not handling errors in this tutorial. To do so you'd add an else statement in the create method. 

If you receive an error like this: 

```
ActiveModel::ForbiddenAttributesError
```
Rails 4 requires that necessary parameters be marked as required.  you can add this to your model to require the ```:user``` parameter and permit its keys. Also, update the ```create``` method to accept user_params instead of the parameters themselves.

```ruby
class UsersController < ApplicationController

  def new
    @user = User.new
  end

  def create
    @user = User.new(user_params)
    redirect_to @user if @user.save
  end

  def show
    @user = User.find(params[:id])
  end

  private

  def user_params
    params.require(:user).permit(:username, :email, :password)
  end

end
```



Now try to sign up. You'll get an error about our show page not existing:
```
Missing template users/show....
```

This is easy to remedy. We just need to create a show view. You should already know how to do this, if not then just add a new file to ```views/users``` called ```show.html.erb```. In this file add something like:

```erb
<h1>Welcome <%= @user.username %> </h1>
```

Now refresh the browser (or signup again). Everything should work! 

Sweet! That was fun. We now have an app where a user can come and signup... Well, kinda. A user can't actually come to the home page and signup. So that's what we'll do next. We'll create a landing page with a link to signup. 

But before we do that you should take a break if you haven't yet. I recommend possibly drinking some water (yes water... not coffee) or maybe even stretching a little... Surely sitting in that chair can't be good for your posture. What's this? You're at a standing desk? In that case have yourself a seat and relax like the rest of us! 

Enough sillyness. On to the next exercise!

<h2 id="links">Links</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#links" target="_blank">Links overview</a>

In this exercise we'll be creating navigation that will show on each page. This will give us a chance to use the Rail's ```link_to``` helper for all our links. Before we get started I want to forewarn you, this navigation is going to be pretty wild. It's going to have a signup link and a home link. I know, I know. I'm pretty extreme. :P

Before we get to building our amazing navbar we'll need to setup our landing page. If you remember correctly our current landing page is the default Rails landing page. This file is located in the public folder under ```index.html```. Let's delete this file as we'll not be needing it any longer. 

Now that we've deleted the default landing page, let's create our own. First we'll update ```routes.rb``` with:

```ruby
PracticeApp::Application.routes.draw do

  root to: "static_pages#index" # this is the line we are addding
  resources :users
  
end
```

Next let's create a ```static_pages``` folder in ```views```. Once we've created this folder we'll add the ```index.html.erb``` page we see referenced in the routes file above. Next add the following code to the ```index.html.erb``` file:

```erb
<h1>Welcome to the Sample app!</h1>
<p>This is being used to help teach Dev Bootcamp students</p>
```

Before our new landing page will work we'll have to create a controller for it. Let's create a new controller called ```static_pages_controller.rb``` in the ```controllers``` folder and add the following code:

```
class StaticPagesController < ApplicationController

  def index
  end

end
```

OK cool, now navigate to ```localhost:3000```. You should see our brand new landing page. Next let's create that amazing navbar I was talking about earlier. To do so we'll add the following to ```app/views/layouts/application.html.erb```:

```erb
<body>
  <div class="navbar">
    <%= link_to "Home", :root %>
    <%= link_to "Sign Up!", :new_user %>
  </div>
  
<%= yield %>

</body>
```

Note the use of the Rail's ```link_to``` to create our home and signup links. To test our work out refresh the page at ```localhost:3000```. Links for home and signup should be found at the top of the page. Let's click them a few times to ensure they function as expected. 

All good? Sweet! That's all there is to the ```link_to``` tag. Much nicer than writing out anchor tags all day, you agree?
OK, let's move on to the next exercise where we'll learn about partials. We'll do this by refactoring our navbar out of the main layout file and into a partial. Ready?

<h2 id="partials">Partials</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#partials" target="_blank">Partials overview</a>

OK, last exercise here. Let's create a partial. First we'll create a new file called ```_navbar.html.erb``` in  ```app/views/layouts```. 

Next we'll cut out our navbar html from the ```application.html.erb``` and add it into our new partial. The code for ```_navbar.html.erb``` should look like so:

```erb
<div class="navbar">
  <%= link_to "Home", :root %>
  <%= link_to "Sign Up!", :new_user %>
</div>
```

OK, so far so good. Last thing is to call the partial from the main layout file. We'll do this with render like so:

```erb
<body>
  <%= render "layouts/navbar" %>

<%= yield %>
.
.
.
```

Note here you do not include the underscore in the render statement. Now refresh the browser and you should still see our links working as before. 

Works? Sweet!

<h2>That's all folks!!! </h2>

Holy hell we're finally done! I hope you enjoyed doing these exercises as much as I enjoyed making them for you. If you're interested in learning more you can always <a href="http://adventuresincoding.tumblr.com" target="_blank">check out my blog</a> where you'll find more tutorials and tips. And if you'd like to connect feel free to <a href="http://facebook.com/rguerrettaz" target="_blank">add me as a friend</a> on Facebook. That's it. :)

GOOD LUCK!

