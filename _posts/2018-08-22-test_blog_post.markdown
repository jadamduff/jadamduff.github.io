---
layout: post
title:      "CLI Data Gem Project -- Super Bowl Bracketeer"
date:       2018-08-22 15:01:54 -0400
permalink:  test_blog_post
---


I've recently finished working on my CLI Data Gem project for Flatiron School, a project to build a Ruby Gem using Nokogiri and OpenURI to scrape data from a web page and display it using a CLI.  Additionally, our CLI was to have at least one nested menu where a user could request and receive additional data. Our instructions asked that we prove our mastery of Object Relationships by, instead of scraping data into massive hashes, building elegant and efficient Objects to store and operate on our scraped data.

You can check out my code on GitHub [here](https://github.com/jadamduff/sb_bracketeer).

### Why NFL Playoff Brackets?

My first order of business in designing my Gem was to choose what kind of data I'd want to provide my user. On top of that, it would have to be a type of data that was rich enough for me to provide a <i>second layer</i> of data -- data about data. I quickly realized that I could entirely limit the design of my Gem by choosing the wrong data type to scrape.

Let's say, for example, I wanted to build a Gem that would return all recent posts from a popular food blogger.  I could design my gem to:

1. Display the post with a title.
2. Upon user request, display the recipe for a dish discussed in the article.

And, yes, this would satisfy the two layer menu requirement.  The user would be shown a piece of data and receive more data upon request.  But in this example, those are the *only two things* that my program can do.  Food blogs don't really go much deeper than that.

I wanted the ability to let my mind wander and create something really cool. This would require choosing the right subject. I needed a subject that could dive off into a million different interconnecting worm holes with a million different entries.  It felt like i needed something like... hmm...

Of course! Sports!

As any casual sports fan knows, sports communities keep better records than the IRS.  And with hundreds of thousands of games played by even more players, I'd have plenty of options when designing my Gem.  So I chose to make a sports gem -- more specifically an NFL Football Gem because I like that kind the best. I thought it would be fun to let people reminisce on their favorite games from NFL Playoff past and who was on their favorite team's roster that year.

So that's what I did.  My gem allows users to:

1. Enter a year from 1990-2017 (the era of modern playoffs with four wildcard games) and receive a playoff bracket for that year. Each game in the bracket includes its date, title, team names, and score.
2. Enter the name of a team from the bracket and receive an entire roster with player numbers from that year.

Like our cooking blog example, my Gem performs two functions. However, unlike the cooking blog, I got to *choose* these two functions. They weren't forced on me. I could have designed it a ton of other ways with other datasets (individual player stats, game stats, etc.) but I didnt. I designed it how I wanted to.

### Objects Only

There's another thing about the design of my Gem that made building the codebase really fun: **I was forced to follow the rules.** The sheer design of my Gem made it impossible for me to break my project requirements. Let me explain.

One of the project requirements was as follows:

> Use good OO design patterns. You should be creating a collection of objects, not hashes, to store your data.

Basically, this requirement is meant to keep us from doing something like this:

```
bracket_data = { :wildcard_game1 => "Scraped wildcard game data", :wildcard_game2 => "Scraped wildcard game data", etc... }

puts bracket_data[:wildcard_game1]
puts bracket_data[:wildcard_game2]
```

We were instructed *not* to scrape a bunch of data into a pre-defined hash and then dump that hash out into the terminal. With something like the cooking blog, this hash scrape and dump is possible. We could scrape data into a hash

```
blog_post = {
:post_title => '',
:post_body => '',
:publish_date => '',
:recipe_title => '',
:ingredient_arr => []
}
```

and iterate over blog_post, puts-ing each key value in perfect order.

But with Super Bowl Bracketeer, I couldnt get away with this -- mainly because the playoff data I was scraping *didn't come in bracket format*.  Take a look at the way the data is displayed on [footballdb.com](https://www.footballdb.com/):

![](https://i.imgur.com/EhTSZJx.png)

Its ordered by date! And dates don't do much for helping us figure out bracket order.  Brackets are ordered by wins, not dates.  Imagine if I just used the data as-is and spit it out into the terminal... It would be a mess.  Yes, the teams in each round would be correct, but the games wouldn't connect to eachother. So, instead of scraping and dumping, I was *forced* to store the data in Object instances and perform logic on it via Object Methods.

I ended up creating a group of Object relationships `bracket -> round -> game -> team`, each working together to fill the bracket and get it in the correct order.

### Expansion

I think Super Bowl Bracketeer is pretty cool, but I'd like to note a couple ideas for future expansion.

#### 1. Increase the year range for bracket search

Currently the year range is 1990-2017 because 1990 is the year that the NFL implemented a 4 wild card game playoff. For some time before 1990 there were only two wild card games and at some point even earlier there were none.  With some additional logic, the year range could be expanded to include every NFL playoff ever played.

#### 2. Add another data layer

I think it would be cool for the user to get game and season stats for an individual player on a team roster.  This would require adding a Player class and a player_scraper method to the Scraper class.


If you're reading this, please feel free to take what I've done and run with it.

Enjoy!
