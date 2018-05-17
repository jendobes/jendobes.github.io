---
layout: post
title:      "Swag for beginners: Stying a Ruby App with Materialize"
date:       2018-05-17 18:30:31 +0000
permalink:  swag_for_beginners_stying_a_ruby_app_with_materialize
---


I was really proud with the progress I made on my Rails application (a petfinder website for pets in shelters) but was weary of showing off my project since it looked like a poorly done site from the 90's. Bootstrap's default stying made this marginally better, but I wanted some style that I could be proud of while avoiding a 5 hour workflow. 

[Materialize](https://materializecss.com) was the perfect solution; it was incredibly quick to set up, the documentation is straightforward, and within an hour I had a website that didn't look like amateur hour. 

## Setup
Add the materialize gem to your gemfile and run 'bundle install'
```
#Gemfile

gem 'materialize-sass
```
Next, append the application's stylesheet filename with .scss and add the following code to that file:
```
/* assets/stylesheets/application.css.scss

@import  "materialize";
```

Voila, you're ready to start swagging.

## Adding in style to layouts/application.html.erb
Adding in features with Materialize is as simple as adding classes to HTML elements. Each class creates a different effect, which is outlined in detail in the docs.

Since I didn't want to spend a lot of time styling my website, I wanted to add features that would make the greatest impact: images, containers, and a fun nav bar. 

First, I found some images to use as clickable links on my homepage to navigate to the most important parts of my website. I also found an image for the 'login with facebook' link that made my website feel more legitimate. 

![](https://imgur.com/GQcvF8i)

The majority of my styling was done in view/layouts/application.html.erb, since this file affects all the views of my app. To give my content some margin and have it centered correctly, I added in the following div between the body elements: 

```
<!-- layouts/application.html.erb --!

<body>
     <div class="container">
		 <%= yield %>
		 </div>
</body>
```

the "container" class did all the heavy lifting.

Next, I added the class "nav-wrapper" to my navbar div, which created the below navbar with built in hover response. The default color is coral, but you can change it to any color in the [materialize color library](https://materializecss.com/color.html) with the below code:
```
<div class ="nav-wrapper teal lighten-4"
```

![](https://imgur.com/fyKbuES)

To finish off the navbar, I created a clickable logo that would take the user back to the homepage
```
<nav>
  <div class='nav-wrapper'>
    <%= link_to '/' do %> <%= image_tag("logo.png", :class => "brand-logo center") %> <%end%>
	. . .
</nav>
```

![](https://imgur.com/LlDR3CP)

Already my homepage has some swag!


## Creating cards for #show pages
Cards quickly took my pet #show pages from blah to 'ok, pretty stylish'
Cards are basically a wrapper for small bits of information and can include an image, which was ideal for showing off my pet images and essential tidbits.

```

<div class="row">
  <div class="col s12 m7">
    <div class="card">
      <div class="card-image">
        <%= image_tag @pet.image.url(:medium) %>
        <span class="card-title"><%= @pet.name %></span>
      </div>
      <div class="card-content">
        <ul>
          <!-- erb code -->
        </ul>
      </div>
    </div>
  </div>
</div>
```

![](https://imgur.com/JE5MGlf)

## Styling forms
By default, materialize styles forms pretty nicely, however I was really frustrated to fidn that I couldn't click my buttons correctly once materialize was downloaded. 
To keep your forms working correctly, you MUST put label_tags AFTER the helper tag, per the below example text from my project:
```
<div class="center-align">
  <%= form_tag('/pets', :method => 'get') do %>

    <%= radio_button_tag :select, "dogs" %>
    <%= label_tag :select_dogs, "Dogs" %>
    |
    <%= radio_button_tag :select, "cats" %>
    <%= label_tag :select_cats, "Cats" %>
    |
    <%= radio_button_tag :select, "high_risk"%>
    <%= label_tag :select_high_risk, "High-risk" %>
    |
    <%= radio_button_tag :select, "all"%>
    <%= label_tag :select_all, "All Pets" %>
    <br>
    <button class="btn waves-effect waves-light" type="submit" name="action">Search</button>
  <% end %>
</div>
```

I replaced the default form_tag button with the html button tag shown in the above code, which gave me a nicely styled button.
![](https://imgur.com/cDsAxXx)


Overall Materialize is a great tool for beginners since it is not only quick and easy to use, but also is very unintrusive to the existing code -- you are basically only adding in classes to HTML elements that already exist in your code. 




