---
layout: post
title:      "Use Tux & Seed Files!!"
date:       2018-03-30 11:22:22 +0000
permalink:  use_tux_and_seed_files
---


I recently completed my Sinatra portfolio project, a website called stagNot which encourages people to try a new thing every day. In stagNot, you can add your new activity to a tracker which acts as a sort of diary of your adventures. You can also search for new activities and add them to your Wishlist for inspiration. 

At face value, this seems like a straightforward project with a database of Users and Activities, however I quickly realized that creating a has-many to has-many relationship between users and activities would get complicated, especially since the relationship could be in either the form of a user completing an activity or a user adding an activity to their wishlist. 

Determining the database structure and the relationships between objects is the foundation of this project, and if this initial piece wasn't correct the rest of the project would fail. It was critical that I extensively test my database before moving forward - and here I found the immense value of the tux gem and using seed data.

I decided to create four tables - Users, Activities, Completes, and Wishlists - to execute my has-many to has-many relationship. I had never worked with two joins tables for the same data (users and activities) before, and the task initially seemed daunting. However, by creating placeholder data in a seeds.rb file and incorperating it into my database with rake & ActiveRecord by running rake db:seed, I was able to populate my database.

I also needed a way to test my data and play with the relationships before I felt comfortable enough to move on in my project. The ruby gem tux facilitates this sort of testing; by requiring tux in my Gemfile and typing 'tux' into the terminal, I was able to enter a sort of data playground where I could call on data objects and see how they behaved. This proved immensely useful later in my project when trying to determine the correct queries. 

Creating a database without actively testing at every step is impossible at worst and dangerous at best, since creating Sinatra views and controllers based on incorrect assumptions about your database will ruin an entire project. The tux gem and seed data are essential for programmers to understand exactly how their models interact and how they can correctly access their database. 
