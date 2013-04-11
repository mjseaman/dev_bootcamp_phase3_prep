Overview
==============

Onboarding for Rails. The below topics will help you make a smooth transition from Sinatra to Rails. Skim through them to familiarize yourself. If you have time check out some of the exercises, but don't kill yourself. 

Table of Contents:
-----------

* <a href="#introduction">Introduction (READ ME first)</a>
* <a href="#things-you-should-know-to-succeed-in-phase-3">Things you should know to succeed in phase 3</a>
* <a href="#how-to-use-this-guide">How to use</a>
* <a href="#rspec--testing">Rspec & Testing</a>
* <a href="#models--migrations">Models & Migrations</a>
* <a href="#controllers--routes">Controllers & Routes</a>
* <a href="#views">Views</a>
* <a href="#partials">Partials</a>
* <a href="#forms">Forms</a>
* <a href="#links">Links</a>
* <a href="#ajax">Ajax</a>
* <a href="#environments">Environments</a>

<h2 id="introduction">Introduction</h2>
This guide covers a wide spectrum of IMPORTANT topics in Rails. It does not cover any one topic too deeply. On the contrary, the goal is to introduce you to Rails conventions, not make you an expert in them. 

As you go through you may find yourself confused. This is ok. Rails is confusing at first. You may also find yourself angry (as I did), wondering why the hell we learned Sinatra just to switch to rails. Trust in knowing there is a good reason and your hatred for Rails will soon subside (NOTE: everything you learned in Sinatra is used in Rails, the wording is just a little different. Don't forget this.). Also trust in knowing this tutorial was created by a fellow boot with only 7 weeks of programming under his belt. It's not perfect... It is however pretty bad ass and is infinitely more than the Sea Lions and my cohort, the Banana Slugs, had as prep for our final chapter at DBC. (NOTE: we were not given any prep for phase 3 \#fail)

If you are so inclined to give back and help improve this project, please do so. Forking this repo and adding your own thoughts or edits to improve the experience for future boots is greatly appreciated and I will do my best to add everyone's edits in.

<h2 id="#things-you-should-know-to-succeed-in-phase-3">Things you should know to succeed in phase 3</h2>
- Phase 3 is unlike any other phase
- It is less structured
- You should expect to struggle
- Rails generate is not to be used for anything but your models 
- Rails generate is not to be used for anything but your models (yes, you need to hear this twice)
- <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book" target="_blank">Hartl</a> is a useful guide, but do not take it as gospel
- Hartl is a useful guide, but do not take it as gospel (yes, you ALSO need to hear this twice)
- Go slow
- Learn your tools (aka Gems) and learn them well
- Struggle with TDD even though you don't want to write it
- Things in Rails are not that different than what you learned in Sinatra
- Make sure you truly believe the above bullet point, if you don't, ask someone to explain it
- Learn to enjoy the struggle because your life as a programmer is one BIG effing struggle
- Rails is your friend, if you're not having fun you're doing it wrong! :)
(If you're not having fun and you're actually doing it right, ask Jeffrey for some "slap therapy")
- And finally... this is just the beginning, not the end..

<h2 id="how_to-use-this-guide">How to use this guide</h2>
The prep works like this: 
- I give you a topic in rails
- I try to show you how it worked in Sinatra
- If you are lucky you'll understand the difference
- If you don't understand I do my best to offer an exercise to help you understand
- If you still don't understand, fear not, you still have more prep than my cohort did :P

No really, if you don't understand, don't freak out, at least you've been introduced to it. This is step 1 in the learning process and referred to as <a href="http://socrates.devbootcamp.com/labs/curriculum/dbc-s-principles/designing-with-empathy#toc_0" target="_blank">recognition</a>...  (click that link)... (seriously, click it). 

Enough mumbo jumbo, let's get to learning!

<h2 id="rspec--testing">Rspec & Testing</h2>
Don't stress too much on Rspec and Testing right now. There are (or were) 3 great challenges in week 1 that get you up to speed. Also realize tests can be a major road block to your learning in Rails. I would recommend you get comfortable with rails before you worry about TDD.

That said, here's a list of gems I used to run my testing in rails. We'll call it the TDD toolbelt
###TDD toolbelt
<a href="https://github.com/thoughtbot/factory_girl_rails" target="_blank">Factory Girl</a> - allows you to create objects for your tests, hence the name "Factory" girl. 

<a href="https://github.com/jnicklas/capybara" target="_blank">Capybara</a> - allows you to click links, sign in, fill out forms, etc. 

<a href="https://github.com/thoughtbot/shoulda-matchers">Shoulda-Matchers**</a> - allows you to run tests on your models quite easily. Created by ThoughtBot

<a href="https://github.com/bmabey/database_cleaner" target="_blank">DatabaseCleaner</a> - allows you to run tests in the development and test environments. Watch this <a href="http://railscasts.com/episodes/257-request-specs-and-capybara">Railscast</a>

<a href="https://github.com/johnbintz/guard-rails" target="_blank">Guard</a> - auto runs your tests on save of a file. Follow this <a href="http://ruby.railstutorial.org/chapters/static-pages?version=3.2#sec-3_6_2" target="_blank">tutorial</a> to get setup with guard and the gem below, spork.

<a href="https://github.com/sporkrb/spork" target="_blank">Spork</a> - loads your rails environment *once* for you so it doesn't have to be loaded each time you run tests. Here's another good <a href="http://blog.carbonfive.com/2010/12/10/speedy-test-iterations-for-rails-3-with-spork-and-guard/">tutorial</a> on getting Spork and Guard up and running.  

<a href="https://github.com/maltize/sublime-text-2-ruby-tests" target="_blank">RubyTest</a> - this is actually a Sublime package. It allows you to run your tests straight from Sublime console, super useful. 

These tools make for a speedy and pleasant TDD experience. I highly recommend getting to know them when the time comes. You will surely learn to love them. And if you didn't watch the <a href="http://railscasts.com/episodes/257-request-specs-and-capybara">Railscast</a> I linked to above, I highly recommend you take the 10 minutes to watch it now, it's an excellent overview of TDD and the "toolbelt".

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#rspec--testing" target="_blank">Rspec & Testing exercise</a> 


<h2 id="models--migrations">Models & Migrations</h2>
Models and Migrations in Rails are very similar to Sinatra. The major difference is how to create a migration and model in rails, using ```$ rails generate```

Creating a model in our sinatra skeleton went like this:
```
$ rake generate:model NAME=MyModel
```
This was actually code Jesse wrote for us. In Sinatra this rake task does not exist. In rails however there does exist ```$ rake generate``` and it goes like this:
```
$ rails generate model MyModel
```
This will create a model in assets/models named "my_model.rb" and a migration named "create_my_models.rb". Very useful. 

Probably the most exiting thing about ```$ rails generate``` is the ability to pass table attributes from command line. Here's an example:
```
rails generate model MyModel name:string email:string password:string
```
Again this command will generate a model and migration file, but the migration file will now be created with our columns already in it. Like so:
```ruby
class CreateMyModels < ActiveRecord::Migration
  def change
    create_table :my_models do |t|
      t.string :name
      t.string :email
      t.string :password

      t.timestamps
    end
  end
end
```
That deserves a \#Railsmagic! 

That's about the most I think you should know about models and migrations in Rails. Everything we did in Sinatra still applies with associations and validations. These are part of ActiveRecord and don't change from one "framework" to the other. 

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#models--migrations" target="_blank">Models & Migrations exercise</a>

<h2 id="controllers">Controllers & Routes</h2>
Controllers in rails are a bit different than in Sinatra. The main difference is the syntax of the routes. In rails we have a ```routes.rb``` file. This file is incredibly powerful and important. It's main purpose in life is to serve as an index for rails to know where to find each "route" or url that a user may visit.  Think of it as an old school <a href="http://en.wikipedia.org/wiki/Switchboard_operator">switchboard (phone) operator</a>. Calls come in and the operator connects the call to the proper "jack" or line. ```routes.rb``` does the same thing except with urls. When a url is called it asks the router to connect it to the proper route. The router knows which route goes where because you state the routes in the ```routes.rb``` file. 

An example ```routes.rb``` file:
```ruby
QuestionMonkey::Application.routes.draw do
  root to: 'static_pages#home'
  resources :users
  resources :surveys, :only => [:new, :create, :show, :index]
  resources :questions, :only => [:new, :create, :destroy]
  match "users/profile", to: "users#profile"
end
```

OR this from <a href="https://github.com/shivamd" target="_blank">Shivam D</a>, <a href="https://github.com/jam-tmrw" target="_blank">James (Jimbo) Hamilton</a>, and myself's group project <a href="https://github.com/rguerrettaz/mockrates" target="_blank">Mockrates</a> from week 1 of phase 3:
```ruby
Mockrates::Application.routes.draw do

  root :to => 'users#show'
  resources :github_sessions, only: [:new]
  resources :users
  resources :challenges
  resources :sessions
  resources :attempts
  resources :weeks

  match '/login', to: 'sessions#new'
  match 'auth/:provider/callback', to: 'github_sessions#create'
  match '/test', to: 'challenges#test'
  match '/test2', to: 'challenges#test2'
  match '/challenges/:id/interactive', to: 'challenges#interactive'
  match '/locale/en.xml', to: 'locale#en'
  
end
```

Now that you are thoroughly confused about ```routes.rb``` I will send you off to learn how it truly works. <a href="https://github.com/keithtom">Keith Tom</a> does a great job of explaining routes <a href="https://gist.github.com/keithtom/3f311c392326bc659b54#readme">here</a>. Go through and read his section on routing. This is important. Please make sure to read his post as it sets up many other topics below.  

Now that you've read Keith's post my job here is done... I will however offer a quick exampe of the difference in controllers between Sinatra to Rails.

In Sinatra our controller looks like this:
```ruby
get '/' do
  @user = User.new
  erb :index
end

get '/users/:id' do
  @user = User.find(params[:id])
  erb :profile
end
```
In rails our controller looks like this:
```ruby
class UsersController < ActiveRecord::Base

  def index
    @user = User.new
  end

  def show
    @user = User.find(params[:id])
  end
end
```
What in the world!! Right? Maybe not, but it's a little confusing when you don't know how rails routing works so, for the third time, go read <a href="https://gist.github.com/keithtom/3f311c392326bc659b54#readme">Keith's post</a>. And if you still don't get it, check out the exercise below.
   
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#controllers" target="_blank">Controllers exercise</a>
<h2 id="views">Views</h2>
Views in rails are similar to those in Sinatra. There are a few main differences:
- They end in ```html.erb``` instead of ```html```
- They are organized nicely by model name. I.e. Your users views are in ```app/views/users```
- They are named after the route they represent. That's to say if you have a ```users/new``` route, the view file for this route would be ```apps/views/users/new.html.erb```. If you are still confused about routes because you didn't read Keith's post, please read it... If you read Keith's post and are still confused then rest assured you will understand soon. :)

That's really it for views.

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#views" target="_blank">Views exercise</a>
<h2 id="partials">Partials</h2>
Partials in Rails are a bit different than in Sinatra. They are still stored in a file the same way but the way they are called varies slightly. 

Let's start with where and how to store partials. In Sinatra we stored our partials in the ```/views``` folder. Or maybe some of us more advnaced monkeys created a separate ```/views/partials``` file. Either way they were prefixed with an underscore like so ```_my_amazing_partial.html```.  

In Rails we still prefix the partial with an underscore (yay!). And we still store them in the views folder (double yay!). But the <a href="http://stackoverflow.com/questions/2384631/where-to-put-partials-shared-by-the-whole-application-in-rails#answer-2385178">rails convention for storing partials</a> is to store them in a ```/views/shared``` folder. Now you definitely don't have to do this. It will work just fine to store your partials in their respective views folders, but I personally enjoy following convention. 

So imagining we are storing our partials in the ```/views/shared``` folder, how do we call them from inside our view? It's not too difficult. We use ```render```, like so:

```erb
<%= render '/shared/my_amazing_partial' %>
```

This varies from the Sinatra way:
```erb
<%= erb :'/partials/_my_amazing_partial' %> 
```
OR
```erb
<%= erb :_my_amazing_partial %>
```
Notice in Rails we do not include the underscore when we call the partial from the view. This may seem a bit strange, but its no big deal really. 

I think that's it for partials!

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#partials" target="_blank">Partials exercise</a>
<h2 id="forms">Forms</h2>
Forms in Rails are \#awesome. You may not think so at first, but they are. What makes them so great you wonder? They are powerful little buggers that allow you to write less code and offer more functionality than in Sinatra. Here's what I mean:

In sinatra our forms were built by hand if you will, like so:
```html
<form action="/users" method="post">
<input type="text" name="user[username]" placeholder="Username">
<input type="email" name="user[email]" placeholder="email">
<input type="password" name="user[password]" placeholder="Password">
<input type="submit" value="Sign up!">
```
Seems all good, right? But to be honest I don't want to keep writing that out over and over. In steps the rails <a href="http://guides.rubyonrails.org/form_helpers.html#binding-a-form-to-an-object">form_for</a> helper. What does form_for do? It allows us to pass an object into the form and will create our ```method```, ```action```, and ```inputs``` for us based on that objects attributes and Rails routes... Confusing, indeed. Check out this example. It may make more sense.

Rails form_for in action:
```erb
<%= form_for @user do |f|  %>
<%= f.text_field :username, placeholder: "Username" %>
<%= f.email_field :email, placeholder: "Email" %>
<%= f.password_field :password, placeholder: "Password" %>
<%= f.submit "Sign up!" %>
<% end %>
```
Which translates to:
```html
<form accept-charset="UTF-8" action="/users" class="new_user" id="new_user" method="post" >
  <div style="margin:0;padding:0;display:inline">
    <input name="utf8" type="hidden" value="✓">
    <input name="authenticity_token" type="hidden" value="fGUew7MnGx+48gel2vjxNhqdHVUKp7q7rIMCIk+ehOw=">
  </div>
  <input id="user_username" name="user[username]" placeholder="Username" size="30" type="text" />
  <input id="user_email" name="user[email]" placeholder="Email" size="30" type="email" />
  <input id="user_password" name="user[password]" placeholder="Password" size="30" type="password" />
  <input name="commit" type="submit" value="Sign up!" />
</form>
```

The syntax is a bit different, but the above html has the exact same outcome as the Sinatra form. It may not feel so, but check the Sinatra form again. Compare it to the rails form. The same main parameters are there ```action```, ```method```, ```input```, ```names```, ```types```, ```placeholders```, and a ```submit button```. Yes, the rails form has extra parameters but don't get confused. The truth is, both are going to send params[:user] to the "action" route as a "post"... 

Also, don't get bogged down in the details of the ```<div>```. it's part of rails security and prevents CSRF (Cross Site Request Forgery). If you want to learn more, read <a href="http://stackoverflow.com/questions/941594/understand-rails-authenticity-token#answers-header">this</a>. 

That's it for an intro. Rails forms are super powerful so start using them and keep using them. And if you're interested in learning more check out the exercise or, if you're feeling really frisky, start learning about <a href="http://apidock.com/rails/ActionView/Helpers/FormHelper/fields_for">fields_for and nested forms</a>...

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#forms" target="_blank">Forms exercise</a>
<h2 id="links">Links</h2>
Links in rails are quite different than Sinatra. 
**add more**

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#links" target="_blank">Links exercise</a>
<h2 id="ajax">AJAX</h2>
**needs content**

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#ajax" target="_blank">AJAX exercise</a>
<h2 id="environments">Environments</h2>
Don't worry too much about environments. There are 3 of course: Development, Test, & Production. All you might want to know for now is that in order to run your rspec tests you must type in 
```
$ rake db:test:prepare
```
after you run your 

```
$ rake db:migrate
```

That's all folks. The final advice I will share is that the first week of Rails can (will) be treacherous. When it is, remember back to the first week of Phase 2 when you were introduced to Sinatra, CSS, HTML, AJAX, javascript, JQuery, and erb all in one day. That week was most likely just as overwhelming, but after 3 weeks you are now a wizard. The same will be true with Rails. So stay confident and keep working hard!! 
