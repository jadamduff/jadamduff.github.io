---
layout: post
title:      "Rails with Javascript Portfolio Project -- Commission Tracker"
date:       2018-11-26 21:42:51 +0000
permalink:  rails_with_javascript_portfolio_project_--_commission_tracker
---


This project is an expansion on my previous project, building Commission Tracker with RoR only.  Check out my blog post talking about that project [here](http://adamduffdev.com/rails_portfolio_project_--_commission_tracker).  I won't be covering much of the actual functionality in this post, because the Rails with Javascript project is all about jQuery and Ajax.

Here were the project requirements:

1. Must render at least one index page (index resource - 'list of things') via JavaScript and an Active Model Serialization JSON Backend.
2. Must render at least one show page (show resource - 'one specific thing') via JavaScript and an Active Model Serialization JSON Backend.
3. Your Rails application must dynamically render on the page at least one 'has-many' relationship through JSON using JavaScript.
4. Must use your Rails application and JavaScript to render a form for creating a resource that submits dynamically.
5. Must translate the JSON responses into JavaScript Model Objects using either ES6 class or constructor syntax. The Model Objects must have at least one method on the prototype. Formatters work really well for this.

Commission tracker is meant to feel like a native app.  It works best when users can recieve and submit new data without constant page reloads and in-your-face http requests. As it stood prior to this project, Commission Tracker had a page for everything.  Creating a new product or sale required navigation away from and back to the user dashboard, breaking the user experience.  With Ajax, Commission Tracker keeps the user in one page and lets their user profile update dynamically.

## Forms with jQuery

My first order of business in transforming Commission Tracker into its new, dynamic self, was to provide a dropdown form on the user's dashboard for creating new Products and Sales.  Instead of navigating away from the dashboard to a new page with a submit form, I translated the form into a new div that would appear right below the "New" button in the header.  Additionally, when the form is visible, the "New" button becomes a "Cancel" button that resets and hides the form.

I built the functionality of the form using jQuery to hide the form div on page load and show via an event listener on the .button class.  However, while working to get the form positioning correctly, I wasn't looking forward to how finicky getting the form to show in the right place (perfectly below the "New" button) was going to be, while ensuring that it maintained that position on page scroll and resize.

I ran across an awesome JS library called Tether that saved a ton of headache.  Tether allowed me to declare which elements should be anchored to eachother and how they should respond to page changes. If you want to see more of how it works, check out their site [here](http://tether.io/).


## turbolinks

Turbolinks is an awesome JS library included by default in Rails 5.0. Instead of reloading the entire page on browser refresh, it only throws out and reloads the parts of the DOM that have changed. However, as sleek and powerful as turbolinks is,  jQuery has some trouble figuring out when it needs to go searching for elements since it's changing the way the DOM is loaded. $(document).ready() doesn't work because the DOM can change without the $(document) object being reloaded.

Instead, I found it necessary to use $(document).on('turbolinks:load'); in the place of $(document).ready();. This allows jQuery to accurately interact with the DOM, while letting turbolinks dynamically refresh the page.


After using Ajax to submit data to my controllers, creating json serializers, and getting a json response, I perfectly understand the power of Ajax. 

