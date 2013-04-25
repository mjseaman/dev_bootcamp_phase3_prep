# THIS IS A WORK IN PROGRESS. MORE EXERCISES TO COME SOON

Exercises
===============

If you haven't done so yet, read the [overview page](https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview). Doing the exercises before reading the overview surely leads to <a href="http://omgface.com/evil/evil%20baby7.jpg" target="_blank">death</a>...

<h2 id="introduction">Introduction</h2>
We, the prior boots, have done our best to create exercises for you, current boot, to complete in hopes you don't feel completely lost when you meet Rails in Week 1 of Phase 3. These exercises are a work in progress and your feedback is greatly appreciated and needed for us to continue improving. If you find an exercise needing improvement please fork the repo and update accordingly, submitting a pull request to notify us. We will add your improvements to the prep as soon as possible.

Also note there may not be exercises for all topics. Again, please help by creating an exercise for us if you can. :) 

<h2 id="rails-setup">Rails setup</h2>

Before we get started let's get setup with Rails. Most of you should already of Rails setup, but for those who don't follow <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book#sec-1_2" target="_blank">this</a> guide. Once completed create a new app by typing:
```sh
$ rails new practice_app -T
``` 
This will create a new Rails app within whatever directory you are currently in. (I recommend doing it from the Desktop directory). The "-T" is short for "--skip-test-unit", which bypasses the creation of the Rails default test unit. We will be writing own tests in rspec, so we don't need it. 

Moving on!

<h2 id="rspec--testing">Rspec & Testing</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#rspec--testing" target="_blank">Rspec & Testing overview</a>

OK, our first tests... I know what you're thinking, "Shit! Uggghhh! Fudge!! Tests... grrrr". Yes, indeed. But tests are our friends. So instead of cursing tests we will welcome them by getting our test environment set up like a <a href="http://ionenewsone.files.wordpress.com/2011/09/al-capone.jpg" target="_blank">G</a>.

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

Start by creating a "models" folder within our newly created "spec" folder. Then create a "user_spec.rb" file. Open this file and add the following code: 

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
If we run our tests again we find they are still failing. So how do we fix this? Well one problem we are having is with mass assignment. We cannot mass assign attributes to a model without declaring them in our attr_accessible statement. So let's declare our attributes in the model. To do so navigate to ```app/models/user.rb``` and open the file. From here let's add our attribute accessible's like so:
```ruby
class User < ActiveRecord::Base
  attr_accessible :username, :email, :password
end
```

Now run our tests and.... The shit works. F* YEAH!!!!!!!! Passing tests and a user model! Done and done. 

So what did we just do? Here's the simple list:
- We generated a model and migration file with ```rails g model User```
- We then added our attributes to the migration file just as we did in Sinatra
- We added our attributes to the attr_accessible line in our User model so we can write to our user model

Really not that difficult, was it? Maybe so, maybe not. Either way we did successfully create a migration and model and got our tests from section 1 working. Heck yeah! Now lets get a controller set up. 

<h2 id="controllers">Controllers</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#controllers" target="_blank">Controllers overview</a>
<h2 id="views">Views</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#views" target="_blank">Views overview</a>
<h2 id="helpers">Helpers</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#helpers" target="_blank">Helpers overview</a>
<h2 id="partials">Partials</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#partials" target="_blank">Partials overview</a>
<h2 id="forms">Forms</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#forms" target="_blank">Forms overview</a>
<h2 id="links">Links</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#links" target="_blank">Links overview</a>
<h2 id="ajax">AJAX</h2>
For an overview checkout the <a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/overview#ajax" target="_blank">AJAX overview</a>
