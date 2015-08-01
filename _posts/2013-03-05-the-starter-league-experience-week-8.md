---
layout:     post
title:      The Starter League Experience - Week 8
date:       2013-03-05 11:21:29
summary:    Websites pretty much create themselves these days, right?!? Well not really…
categories: The-Starter-League bootcamp
---

This blog post will walk you through how to create a basic Rails form with Nested Attributes. By the end of this post you will be able to create a form that takes receives input and saves it to multiple database tables. The example given uses a One-To-Many relationship.

Requirements: Rails environment on your computer. My machine has Rails 3.2.12 and Ruby 1.9.3 p362. Since we are not using any gems and the only built in rails function that will be used is “.build”, I anticipate the steps covered here will be valid for many versions to come.

In conjunction with this blog post you may want to reference my Github repo [example_of_rails_form_with_nested_attributes](https://github.com/lando2319/example_of_rails_form_with_nested_attributes), I kept my commits nice and clean.

Step One: Create A New Rails Application. From the terminal run:
> $ rails new example_of_rails_form_with_nested_attributes

Step Two: Generate Scaffold For People Table. From the terminal run:

> $ rails g scaffold people first_name last_name family_id:integer

Step Three: Generate Scaffold For Families Table. From the terminal run:

> $ rails g scaffold families family_name

At this point we have a basic Rails Application with two database tables. The likely next step is to create model associations between People and Families. Since a Family has many People and People only have one Family, this is a One-To-Many relationship.

Step Four: Add Model Associations.

In the Family Model add:

> has_many :people

In the People Model add:

> belongs_to :family

In the spirit of [Error Driven Development](http://www.mikepland.com/the-starter-league-experience-week-5-error-driven-development/) let’s now adjust the form to accept nested attribute data. It’s important to note that the form being used is the one which comes from the parent model, in other words the model that has many. In this case Family.

Step Five: Add the following code inside the Family form.

> <div class=”field”>
> <%= f.fields_for :people do |ts| %>
> <%= ts.label :first_name %><br />
> <%= ts.text_field :first_name %>
> </div>
> 
> <div class=”field”>
> <%= ts.label :last_name %><br />
> <%= ts.text_field :last_name %>
> </div>
> <% end %>

If you would like to see the full code see the [github commit.](https://github.com/lando2319/example_of_rails_form_with_nested_attributes/commit/4913f2daaaef5c7403b835db3f2d67551087cdbd) This would be a good point to run the app, if you haven’t already. Start your rails server and don’t forget to run rake db:migrate, then direct your browser to http://localhost:3000/families/new. You should get the error, “Can’t mass-assign protected attributes: people”

So now we need to make this new data attr_accessible.

Step Six: Add code to allow for mass-assignment.

In the Family Model add the following code to the attr_accessible

> , :people_attributes

Also in the Family Model add:

> accepts_nested_attributes_for :people

Related [Github Commit](https://github.com/lando2319/example_of_rails_form_with_nested_attributes/commit/38a236ab9095d7602f4660ff866fbcaed57b2a0f). Now the last step is to let Rails know where to put this data.

Step Seven: Add .build code to Family Controller under Def New.

> @family.people.build

Step Eight: Test and Confirm. At this point your app should be working. Direct your browser to http://localhost:3000/families/new and test out your new nested form. Once you have entered in some data, go to your Rails Console and run “Person.last” and “Family.last”. You should see the data you just created both with the same Family_id. WOW. And just think you were probably considering using a Gem.

I sincerely hope this post was helpful in setting up a Rails form with nested attributes… Happy Coding.

<ins>Mike Land is a Freelance Web Developer who enjoys technology, entrepreneurship, living in the future…</ins>
