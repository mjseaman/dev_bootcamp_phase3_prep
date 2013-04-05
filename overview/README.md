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
This guide covers a wide spectrum of IMPORTANT topics in Rails. We do not cover any one topic too deeply. On the contrary, our goal is to introduce you to Rails conventions, not make you an expert in them. 

As you go through you may find yourself confused. This is ok. Rails is confusing at first. You may also find yourself angry (as I did), wondering why the hell we learned Sinatra just to switch to rails. Trust in knowing there is a good reason and your hatred for Rails will soon subside (NOTE: everything you learned in Sinatra is used in Rails, the wording is just a little different. DON'T FORGET THIS). Also trust in knowing this tutorial was created by boots, for boots and is not perfect. It is however pretty bad ass and is infinitely more than we (the Sea Lions and Banana Slugs) had as prep for our final chapter at DBC. 

So please be kind with us and please give back by forking this repo and helping us to improve the experience for future boots.

<h2 id="#things-you-should-know-to-succeed-in-phase-3">Things you should know to succeed in phase 3</h2>
- Phase 3 is unlike any other phase
- It is less structured
- You should expect to struggle, A lot
- Rails generate is not to be used for anything but your models 
- Rails generate is not to be used for anything but your models (yes, you need to hear this twice)
- <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book" target="_blank">Hartl</a> is a useful guide, but please God do not take it for bible
- Hartl is a useful guide, but please God do not take it for bible (yes, you ALSO need to hear this twice)
- Go slow
- Learn your tools (Gems) and learn them well
- Struggle with TDD even though you don't want to write it
- TDD is your friend, do your best to love it and learn it's tools (Spork, Guard, TestRuby, FactoryGirl, Capybara, Rspec)
- Things in Rails are not that different than what you learned in Sinatra
- Make sure you truly believe the above bullet point, if you don't, ask someone to explain it to you
- This is just the beginning, not the end
- Learn to enjoy the struggle because your life as a programmer is one BIG effing struggle
- And finally, Rails is your friend, if you're not having fun you're doing it wrong! :)
(If you are not having fun and you are actually doing it right, ask Jeffrey for some slap therapy)

<h2 id="how_to-use-this-guide">How to use this guide</h2>
The prep works like this: 
- We give you a topic and an example of how the topic works in rails
- If we are lucky we can show you how it worked in Sinatra
- If you are lucky you will understand the difference
- If you don't understand the difference we do our best to offer an exercise that helps you understand
- If you don't understand the exercise, fear not, you still have more prep than we did :P
- No really, if you don't understand it, don't freak out, at least you have been introduced to it - this is step 1 in the learning process and referred to as <a href="http://socrates.devbootcamp.com/labs/curriculum/dbc-s-principles/designing-with-empathy#toc_0" target="_blank">recognition</a>...  (click that link)... (seriously, click it). 

Enough mumbo jumbo, let's get to learning!

<h2 id="rspec--testing">Rspec & Testing</h2>
###Your tool bag
<a href="https://github.com/thoughtbot/factory_girl_rails" target="_blank">Factory Girl</a> - *insert description*

<a href="https://github.com/jnicklas/capybara" target="_blank">Capybara</a> - *insert description*

<a href="https://github.com/bmabey/database_cleaner" target="_blank">DatabaseCleaner</a> - *insert description*

<a href="https://github.com/johnbintz/guard-rails" target="_blank">Guard</a> - *insert description*

<a href="https://github.com/sporkrb/spork" target="_blank">Spork</a> - *insert description*

<a href="https://github.com/maltize/sublime-text-2-ruby-tests" target="_blank">RubyTest</a> - *insert description*

<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#rspec--testing" target="_blank">Rspec & Testing exercise</a> 
<h2 id="models--migrations">Models & Migrations</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#models--migrations" target="_blank">Models & Migrations exercise</a>
<h2 id="controllers">Controllers</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#controllers" target="_blank">Controllers exercise</a>
<h2 id="views">Views</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#views" target="_blank">Views exercise</a>
<h2 id="helpers">Helpers</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#helpers" target="_blank">Helpers exercise</a>
<h2 id="partials">Partials</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#partials" target="_blank">Partials exercise</a>
<h2 id="forms">Forms</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#forms" target="_blank">Forms exercise</a>
<h2 id="links">Links</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#links" target="_blank">Links exercise</a>
<h2 id="ajax">AJAX</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#ajax" target="_blank">AJAX exercise</a>
<h2 id="authentication">Authentication</h2>
<a href="https://github.com/rguerrettaz/dev_bootcamp_phase3_prep/tree/master/exercises#authentication" target="_blank">Authentication exercise</a>
<h2 id="environments">Environments</h2>
- Environments (Development, Test, Production)
- Default environment in Rails is Development. 
- Opening development console: ```$ rails console``` Test console: ```$ rails console test```
- Running tests: *insert description*
