---
layout: post
title:      "React/Redux Portfolio Project -- Tailgator"
date:       2018-12-29 19:07:45 +0000
permalink:  react_redux_portfolio_project_--_tailgator
---


This is it -- the culmination of all my projects to the point of backend/frontend mastery.  While RoR is powerful, React/Redux is sexy.  Building single page apps with their own virtual DOM lets me feel like I'm crafting a Tesla instead of a Flatiron portfolio project.  That, however, doesn't mean I didn't thoroughly enjoy building this project.  To round out my time at Flatiron, I decided to not only use the shiny new React/Redux libraries at my disposal, but also to incorporate some external technology (Google Maps, and Braintree payments) that would make this demo pop.

My project, TAILGATOR, is a food-delivery app geared toward tailgators at sporting events.  Users can add products to an order, add their location, and pay with a debit card.

Here are the project requirements:

1. The code should be written in ES6 as much as possible.
2. Use the create-react-app generator to start your project.
3. Your app should have one HTML page to render your react-redux application.
4. There should be 2 container components.
5. There should be 5 stateless components.
6. There should be 3 routes.
7. The Application must make use of react-router and proper RESTful routing.
8. Use Redux middleware to respond to and modify state change.
9. Make use of async actions to send data to and receive data from a server.
10. Your Rails API should handle the data persistence. You should be using fetch() within your actions to GET and POST data from your API - do not use jQuery methods.
11. Your client-side application should handle the display of data with minimal data manipulation.
12. Your application should have some minimal styling.

### Redux and Rails

The first big thing to throw me for a loop was the fact that the Redux state completely resets on page refresh.  It makes sense if you think about it, the browser is re-reading the files and starting at the default Redux state defined.  However, encountering this for the first time is startling.

So, to ensure that the Redux state always matches your persisted user data, you need to query the backend for a current user and, if there is one, set the Redux state to match the relevant data on page load. Otherwise, your database and local state will never match.

### User Authentication

The next hurdle I ran into was figuring out a system for user authentication that would communicate well between my React frontend and my Rails backend. Since we aren't relying on our Rails backend to render view content, we don't have a way to determine wether the user matches the current user stored in the rails session store.  To remedy this disconnect, I used an awesome ruby gem called 'knock'.  Knock provides your backend with out of the box methods for setting and referencing current users, as well as methods for restricting access to certian controllers.  If data from a restricted controller is requested, Knock requires a unique token that it issued when the session was created. If the token isn't supplied witht he fetch request, the data from the controller is restricted.

### Packages to the Rescue

Overall, the biggest tip/trick I learned while building TAILGATOR was that npm packages are your friend.  If you are implementing external technology (like I did with Google Maps and Braintree), there's no need to go through the pain of modifying implementation to fit React. Instead, a package will implement the external technology for you while navigating the React structure.  For example, instead of translating the Google Maps Javascript API documentation into React implementable code, I downloaded the google-maps-react package and dropped it straight into my code.

### Conclusion

Without doubt, React is now the most important piece of technology that I have in my arsenal.  It's fast, customizable, and relatively straight forward. No wonder so many products and platforms are building in or transferring to React as its frontend framework.
