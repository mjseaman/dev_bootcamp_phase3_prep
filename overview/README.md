Overview
==============

Onboarding for Rails. The below topics will help you to make a smooth transition from Sinatra to Rails.

Table of Contents:
-----------

* <a href="#introduction">Introduction (READ ME first)</a>
* <a href="#things-you-should-know-to-succeed-in-phase-3">Things you should know to succeed in phase 3</a>
* <a href="#how-to-use-this-guide">How to use</a>
* <a href="#rspec--testing">Rspec & Testing</a>
* <a href="#models--migrations">Models & Migrations</a>
* <a href="#controllers">Controllers</a>
* <a href="#views">Views</a>
* <a href="#helpers">Helpers</a>
* <a href="#partials">Partials</a>
* <a href="#forms">Forms</a>
* <a href="#links">Links</a>
* <a href="#ajax">Ajax</a>
* <a href="authentication">Authentication</a>
* <a href="environments">Environments</a>

<h2 id="introduction">Introduction</h2>
This guide covers a wide spectrum of IMPORTANT topics in Rails. It does not cover any one topic too deeply. On the contrary, the goal is to introduce you to Rails conventions, not make you an expert in them. 

As you go through you may find yourself confused. This is ok. Rails is confusing at first. You may also find yourself angry (as I did), wondering why the hell we learned Sinatra just to switch to rails. Trust in knowing there is a good reason and your hatred for Rails will soon subside (NOTE: everything you learned in Sinatra is used in Rails, the wording is just a little different. Don't forget this.). Also trust in knowing this tutorial was created by boots, for boots and is not perfect. It is however pretty bad ass and is infinitely more than we (the Sea Lions and Banana Slugs) had as prep for our final chapter at DBC. 

So please be kind with us and please give back by forking this repo and helping us to improve the experience for future boots.

<h2 id="#things-you-should-know-to-succeed-in-phase-3">Things you should know to succeed in phase 3</h2>
- Phase 3 is unlike any other phase
- It is less structured
- You should expect to struggle, A lot
- Rails generate is not to be used for anything but your models 
- Rails generate is not to be used for anything but your models (yes, you need to hear this twice)
- <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book" target="_blank">Hartl</a> is a useful guide, but do not take it as gospel
- Hartl is a useful guide, but do not take it as gospel (yes, you ALSO need to hear this twice)
- Go slow
- Learn your tools (Gems) and learn them well
- Struggle with TDD even though you don't want to write it
- Things in Rails are not that different than what you learned in Sinatra
- Make sure you truly believe the above bullet point, if you don't, ask someone to explain it to you
- This is just the beginning, not the end
- Learn to enjoy the struggle because your life as a programmer is one BIG effing struggle
- And finally, Rails is your friend, if you're not having fun you're doing it wrong! :)
(If you are not having fun and you are actually doing it right, ask Jeffrey for some "slap therapy")

<h2 id="how_to-use-this-guide">How to use this guide</h2>
The prep works like this: 
- We give you a topic in rails
- If we are lucky we can show you how it worked in Sinatra
- If you are lucky you'll understand the difference
- If you don't understand we do our best to offer an exercise to help you understand
- If you still don't understand, fear not, you still have more prep than we did :P

No really, if you don't understand, don't freak out, at least you've been introduced to it. This is step 1 in the learning process and referred to as <a href="http://socrates.devbootcamp.com/labs/curriculum/dbc-s-principles/designing-with-empathy#toc_0" target="_blank">recognition</a>...  (click that link)... (seriously, click it). 

Enough mumbo jumbo, let's get to learning!

<h2 id="rspec--testing">Rspec & Testing</h2>
Don't stress too much on Rspec and Testing right now. There are (or were) 3 great challenges in week 1 that get you up to speed. Also realize tests can be a major road block to your learning in Rails. I would recommend you get comfortable with rails before you worry about TDD.

That said, here is a list of gems I used to run my testing in rails. We'll call it the TDD toolbelt
###TDD toolbelt
<a href="https://github.com/thoughtbot/factory_girl_rails" target="_blank">Factory Girl</a> - allows you to create objects for your tests, hence the name "Factory" girl. 

<a href="https://github.com/jnicklas/capybara" target="_blank">Capybara</a> - allows you to click links, sign in, fill out forms, etc. 

<a href="https://github.com/bmabey/database_cleaner" target="_blank">DatabaseCleaner</a> - allows you to run tests in the development and test environments. Watch this <a href="http://railscasts.com/episodes/257-request-specs-and-capybara">Railscast</a>

<a href="https://github.com/johnbintz/guard-rails" target="_blank">Guard</a> - auto runs your tests on save. 

<a href="https://github.com/sporkrb/spork" target="_blank">Spork</a> - loads your rails environment *once* for you so it doesn't have to be loaded each time you run tests. Here's a great <a href="http://blog.carbonfive.com/2010/12/10/speedy-test-iterations-for-rails-3-with-spork-and-guard/">tutorial</a> on getting Spork and Guard up and running.  

<a href="https://github.com/maltize/sublime-text-2-ruby-tests" target="_blank">RubyTest</a> - this is actually a Sublime package. It allows you to run your tests straight from Sublime console, super useful. 

These tools make for a speedy and pleasant TDD experience. I highly recommend getting to know them when the time comes. You will surely learn to love them. And if you didn't watch the <a href="http://railscasts.com/episodes/257-request-specs-and-capybara">Railscast</a> I linked to above, I highly recommend you take the 10 minutes to watch it now, it's an excellent overview of TDD and the "toolbelt".

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#rspec--testing" target="_blank">Rspec & Testing exercise</a> 


<h2 id="models--migrations">Models & Migrations</h2>
Models and Migrations in Rails are very similar to Sinatra. The major difference is how to create a migration and model in rails, using ```$ rails generate```

Creating a model in our sinatra skeleton went like this:
```
$ rake generate:model NAME=MyModel
```
This was actually code Jesse wrote for us, in Sinatra this rake task does not exist. In rails however there does exist ```$ rake generate``` and it goes like this:
```
$ rails generate model MyModel
```
This will create a model in assets/models named my_model.rb and a migration name create_my_models.rb. Very useful. Probably the most exiting thing about ```$ rails generate``` the ability to pass table attributes from command line. Here's an example:
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
#Railsmagic

If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#models--migrations" target="_blank">Models & Migrations exercise</a>
<h2 id="controllers">Controllers</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#controllers" target="_blank">Controllers exercise</a>
<h2 id="views">Views</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#views" target="_blank">Views exercise</a>
<h2 id="helpers">Helpers</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#helpers" target="_blank">Helpers exercise</a>
<h2 id="partials">Partials</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#partials" target="_blank">Partials exercise</a>
<h2 id="forms">Forms</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#forms" target="_blank">Forms exercise</a>
<h2 id="links">Links</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#links" target="_blank">Links exercise</a>
<h2 id="ajax">AJAX</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#ajax" target="_blank">AJAX exercise</a>
<h2 id="authentication">Authentication</h2>
If you'd like to learn more check out the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#authentication" target="_blank">Authentication exercise</a>
<h2 id="environments">Environments</h2>
There are 3 envirnonment we work with in Rails: Development, Test, & Production. There a few important differences to look out for. Here they are:

- *insert differences or examples*
