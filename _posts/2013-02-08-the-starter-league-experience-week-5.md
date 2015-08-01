---
layout:     post
title:      The Starter League Experience - Week 5
date:       2013-02-08 11:21:29
summary:    Today I am completing week 5 in The Starter League Web Development class. One thing 
categories: The-Starter-League bootcamp
---

Today I am completing week 5 in [The Starter League](http://www.starterleague.com/) Web Development class. One thing I have learned is that an error can be more than just an indicator, an error can actually be a valuable tool. Error Driven Development... as the name suggests, entails using errors to guide your development.

Let me show you an example, after creating a new rails application (the framework for the website being developed) there are a few steps you need to perform before you can display your first custom page, you need a Route, a Controller, and a View Page. The route is going to direct the browser, the Controller is going to contain some business logic, and the View Page is going to be what the user actually sees. Basically there needs to be code in three different places in order for this page to be displayed in the browser.

Now the old me probably would have added all of this code all at once, crossed my fingers, and hoped it worked. This was before discovering the power of Error Driven Development. First thing I do is direct myself to the page I intend to create, I do this knowing that it will not be displayed. This gives me the following predictable error:

![desk](https://lando2319.github.io/assets/20130208/route_error.png)

I directed my browser to the page “comments” of my new app and recieved a routing error. Now you may be asking yourself, “If I knew that I had not created the route why do I need rails to confirm this?”, the answer is because had rails NOT given you this error, then you know that there is ALREADY an issue with your application even before you attempt to setup your route. In this case things appear to be on track, I didn’t setup my route and now rails is asking for exactly that (also in typical rails’ fashion it provides a handy suggestion telling me to ‘rake routes’).

For now I can move on to the next step of creating my route. So I go ahead and add my code to my routes file. The code I am using for my route will call for my CommentsController, which I have not setup, but again in the spirit of Error Driven Development I will attempt to load the page anyways giving me this error:

![desk](https://lando2319.github.io/assets/20130208/controller_error.png)

This error serves to confirm that my route was indeed setup properly. Had my route been setup incorrectly I would have received a different error depending on where the mistake was made. However in this case everything looks good and I am ready to proceed to my next step. If at anytime I am unclear on what the next step is, the best place to start is to read the error message, which in this case is telling me to initialize a constant in my Controller. After adding the necessary code I receive the following error:

![desk](https://lando2319.github.io/assets/20130208/index_error.png)

After reading this error I can immediately tell that I made a mistake with the code I just added, had I written my code correctly I should have received an error about my View Template, NOT my CommentsController. This goes to illustrate the power of Error Driven Development, had I waited until the end to run my app this mistake would have been much more difficult to isolate. But since the only acton I took since last running app was adding to my Controller file, I can immediately go and fix my code, which when run results in following error:

![desk](https://lando2319.github.io/assets/20130208/template_error.png)

Success, a template error like the one above confirms that my Controller code is NOW correct. The next step, as the error suggests, is to setup my View Page Template. After setting up the message, “Hello World” in my View Page, I run my application and see the following page:

![desk](https://lando2319.github.io/assets/20130208/view_page.png)

As you can see our web page is working and through Error Driven Development we were able to work through any issues right away. The real value in Error Driven Development is that it allows us to build our app through iterations. This allows the developer to make sure each step is correct before moving onto the next one.
