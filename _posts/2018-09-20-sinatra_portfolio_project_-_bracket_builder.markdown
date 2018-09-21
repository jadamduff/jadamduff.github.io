---
layout: post
title:      "Sinatra Portfolio Project - Bracket Builder"
date:       2018-09-20 18:14:09 -0400
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

## User to User

I realized early on in bilding Bracket Builder that my blueprint for the application would require a few techniques outside the scope of the assignment. The first technique involves the way users create friendships.

If you think about it, creating friendships between users would require a User has_many Users relationship.  This, on it's face, sounds not so complicated, but when you sit down to flesh it out, you realize it's not possible to simply declare that a user has many users through friendships.  How would you get a list of a user's friends? User.users? No, something smells off about that. Could you do User.friendships? Well how would you even create that join table? If they're both users, would the table columns be user_id  and user_id? That won't work.

Soon I discovered the technique I'd need to use.  It's called Self-Referential Association, achieved by renaming a foriegn key in the join table, while declaring that the class is still User (or whatever class you are joining).  That way, we can say that a User has_many friends through friendships; friend being our alias for "another user".  Let me show you:

User model:
```
class User < ActiveRecord::Base
  has_many :friendships
  has_many :friends, through: :friendships
end
```

Friendship model:
```
class Friendship < ActiveRecord::Base
  belongs_to :user
  belongs_to :friend, :class_name => "User"
end
```

And here you can see the line that creates the self-referential association: **belongs_to :friend, :class_name => "User"**

Now if we'd like to retrieve a list of the current user's friends, we would say:
```
current_user.friends
```
and the friendships model will connect us to each user where the friendship user_id isn't the current user's id. Pretty neat.

## The Necessity for jQuery

Thus far in the Flatiron curriculum, we haven't touched at all upon javascript. I wanted to respect the curriculum and only use languages and concepts that we've learned about.  However, to display users' brackets appropriately and give users all the functionality necessary, I realized I'd have to break pace with our curriculum.  Fortunately, through previous schooling, I have enough knowledge of javascript/jQuery to build what needed to be built.

I used jQuery in two ways:

1. Since brackets can vary alot in number of teams, number of rounds, etc., I needed a way to tell the page how to alter the layout depending on these factors.  When the bracket view page loads, jQuery reads the number of rounds, games, teams, and the status of each game and sets element css to move all the games into their appropriate places.  If a game has been won or lost, jQuery sets the "won" buttons appropriately. Additionally, it listens for clicks on "won" buttons and updates game display boxes with the appropriate team names.
2. The other way I utilized jQuery was to populate a hidden form to submit to the Brackets controller.  It would have been possible to make a POST call to the Bracket controller *each* time a user clicks a "won" button to declare the winner of a game.  In that case, the bracket form would be submitted, the bracket would be updated and the page would be relodaded. But, as a user, can you imagine how annoying that would be, especially on a large bracket?  Every time you want to update a game, your page would refresha and you'd have to re-scroll to the part of the bracket you were at. Instead, I created a hidden form with a field for every team in the bracket. When a user is finished updating the bracket view and clicks "Save", jQuery loops through each team display field and maps it to the corresponding hidden form field.  When the hidden form is completely updated, the form is submitted with all the desired changes to be made at once in the Bracket controller.


## Expansion

There are a ton of directions to take Bracket Builder from here.  And if you have any of your own ides, I'd love to hear them. However, here are a few immediate ideas I have for expansion:

1. An easy feature to add is a social timeline for users.  On a social timeline, Users would see updates about brackets that their friends have created or are competing in.  For example, a user could see an update such as "JohnDoe created a new bracket called John's Bracket", or "JaneDoe just placed 4th in a bracket of 18 teams." These updates would also allow users to like the update and leave a message.
2. Right now, only one user can be attached to a team within a bracket.  A nice feature would be for users to createa their own preset teams of x number of people and have that team included in a bracket.
3. It would also be nice for users to be able to easily communicate about a bracket they are in.  A bracket chat box would be a great place for users to talk about the bracket or talk smack to opponents.


