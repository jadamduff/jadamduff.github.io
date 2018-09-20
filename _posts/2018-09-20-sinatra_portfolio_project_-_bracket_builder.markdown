---
layout: post
title:      "Sinatra Portfolio Project - Bracket Builder"
date:       2018-09-20 22:14:09 +0000
permalink:  sinatra_portfolio_project_-_bracket_builder
---


I've finished another project for the Flatiron School -- this time built with the Sinatra web framework with jQuery and CSS. Our project guidelines were as follows:

1. Use Sinatra to build the app.
2. Use ActiveRecord for storing information in a database.
3. Include more than one model class (list of model class names e.g. User, Post, Category).
4. Include at least one has_many relationship on your User model (x has_many y, e.g. User has_many Posts).
5. Include at least one belongs_to relationship on another model (x belongs_to y, e.g. Post belongs_to User).
6. Include user accounts.
7. Ensure that users can't modify content created by other users.
8. Ensure that the belongs_to resource has routes for Creating, Reading, Updating and Destroying.
9. Include user input validations.
10. Display validation failures to user with error message (example form URL e.g. /posts/new).

I saw these guidelines as a perfect opportunity to build off of my concept of building tournament brackets from my first project in the course, SB-Bracketeer. You can read more about that project [here](http://adamduffdev.com/test_blog_post) and find the project repo [here](https://github.com/jadamduff/sb_bracketeer). With Bracket Builder, I constructed a web app that, instead of filling in historical bracket data, allows users to record their own brackets among friends.  Bracket builder doesn't just record winners and losers, it connects people to eachother through the brackets they're competing in.
