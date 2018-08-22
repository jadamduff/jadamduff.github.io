---
layout: post
title:      "CLI Data Gem Project -- Super Bowl Bracketeer"
date:       2018-08-22 15:01:54 -0400
permalink:  test_blog_post
---


I've recently finished working on my CLI Data Gem project for Flatiron School, a project to build a Ruby Gem using Nokogiri and OpenURI to scrape data from a web page and display it using a CLI.  Additionally, our CLI was to have at least one nested menu where a user could request and receive additional data.

You can check out my code on GitHub [here](https://github.com/jadamduff/sb_bracketeer).

## Why NFL Playoff Brackets?

My first order of business in designing my Gem was to choose what kind of data I'd want to provide my user. On top of that, it would have to be a type of data that was rich enough for me to provide a <i>second layer</i> of data -- data about data. I quickly realized that I could entirely limit the design of my Gem by choosing the wrong data type to scrape.

Let's say, for example, I wanted to build a Gem that would return all recent posts from a popular food blogger.  I could design my gem to:

          1. Display the post with a title.
          2. Upon user request, display the recipe for a dish discussed in the article.

And, yes, this would satisfy the two layer menu requirement.  The user would be shown a piece of data and receive more data upon request.  But in this example, those are the *only two things* that my program can do.  Food blogs don't really go much deeper than that.

I wanted the ability to let my mind wander and create something really cool. This would require choosing the right subject.




