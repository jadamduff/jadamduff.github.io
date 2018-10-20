---
layout: post
title:      "Rails Portfolio Project -- Commission Tracker"
date:       2018-10-20 03:18:04 +0000
permalink:  rails_portfolio_project_--_commission_tracker
---


Commission tracker was a really fun app to build. In some ways it felt like the easiest projuct so far, even though I wrote much more logic for Commission Tracker than my Super Bowl Bracketeer or Bracket Builder apps. I have rails and all it's helpers and gems to thank for that.  For example, with the 'omniauth' gem and just a few lines of code I can make calls to Facebook's api and allow user's to login via their Facebook account. How cool is that?

Commission Tracker is a web app for sales managers and their employees.  Sales managers can create products, set commission, and track revenue, while their employees can log sales and track how much they've earned. When a manager creates a product, they set the title, price, commission percent, and identification color. When employees log a sale, they choose from a list of all their manager's products and how many of the product they sold. As employees log sales, their commission earnings is automatically calculated and the product's sales statistics are updated for the manager.

Here were the project requirements:

1. Use the Ruby on Rails framework.
2. Include at least one has_many, at least one belongs_to, and at least one has_many :through relationship.
3. Include a many-to-many relationship with a model acting as a join table. That join table must include a user-submittable attribute.
4. Include reasonable validations for the simple attributes.
5. Include at least one class level ActiveRecord scope method. The scope method must be chainable, meaning that you must use ActiveRecord Query methods within it.
6. Provide standard user authentication, including signup, login, logout, and passwords.
7. Allow login from some other service. Facebook, Twitter, Foursquare, Github, etc...
8. Include and make use of a nested resource with the appropriate RESTful URLs.
9. Forms should correctly display validation errors. Fields should be enclosed within a fields_with_errors class. Error messages describing the validation failures must be present within the view.
10. Must be, within reason, a DRY (Do-Not-Repeat-Yourself) rails app.
11. Must not use scaffolding.

## Clean and Lean

Rails provides some awesome ways to keep your code lean and DRY. Unlike Sinatra, rails provides helper methods that you can do a bunch with. For example, I wrote a require_login helper method to check whether the user is logged in and redirect them to the login page if not.  Here's the code:

```
def require_login
    redirect_to login_path if !logged_in?
  end
```

Instead of writing this method in each controller action, rails allows you to store this in a helper file and call it whithin the controller. Not only that, rails allows you to declare, in one place, which controller actions should run this method before running the rest of the action's logic. This is called a before_action.

I used helper methods for various things, including requiring that a user is logged in, checking whether a user is a manger or employee, checking whether it is the current user's profile, etc. By building my app with helper methods, I saw first hand why Rails has become such a popular web framework. Instead of building out  my own helper method framework, rails did it for me.

## Expansion
Commission Tracker is a feature that would work best in a CRM environment.  The most sensical way to expand on the work I've done, would be to add CRM features such as client interaction tracking and the ability to build a sales funnel.  It might do well as a Salesforce plugin, etc.

Additionally, there are some micro improvements to be made. For example, users could be grouped into companies and companies could be related via partnerships. Employee users should be able to have multiple managers.  When logging a sale, employees should be able to add more than one product, and should have access to add-on products that don't exist as standalone products, but just as an addition.

If you have any other ideas, I'd love to hear them!




