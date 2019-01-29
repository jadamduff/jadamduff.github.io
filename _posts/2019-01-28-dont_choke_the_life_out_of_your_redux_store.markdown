---
layout: post
title:      "Don't choke the life out of your Redux store."
date:       2019-01-29 00:11:48 +0000
permalink:  dont_choke_the_life_out_of_your_redux_store
---


I've seen a couple schools of thought on the best practice for using Redux to handle application state.  One says that Redux is there to be used; that the whole point is to take state away from controllers and drop it into a universal store.  Developers in this camp will throw everything from external data to input placeholders in the store.  If a component could potentially use it, throw it in there.  This also means that virtually every controller needs to be connected to the store.

The other schgool of thought is a bit more conservatuve.  It says "Let's not abuse this. Let's only put core application data into the store."  If it's not core to the application, meaning it will be reused by multiple components, there's no need to take that piece of state away from the controller.  After all, the need for Redux in the first place comes from the complexity of passing controller state to children and grandchildren.  In a large application, it's quite easy to get lost in your web of state inheritence and forget where any of this data came from in the first place.  Moving all that mess to the Redux store doesn't solve the problem... it just moves the mess to a different location.

The important thing to rember when delegating responsibility between your Redux store and your components is *separation of concerns*.  The best way to implement separation of concerns is to ask yourself a couple questions when building component state.

1. Does this piece of data apply to any components other than this one?
2. Is this data that is being passed to the backend, or just data used for operation of the component.

When you get in a habit of only sending server-necessary data (such as user info, table info, etc.) and data that is used by multiple components to your Redux store, you'll notice that your store will feel ultra lean, operable, and most likely a fairly accurate representation of a portion of your backend.

So, in summary, do yourself a favor and think real hard before you send something to your Redux store.
