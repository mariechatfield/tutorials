---
layout: tutorial
title:  "Firebase | Step 6: Advanced topics in data wizardry"
tutorial_overview: firebase
previous_step: step5.html
---

## BEFORE

| You should... | What to Review |
|------------|--------|
| ...be able to read and write real-time user-generated data to your Firebase database using the Javascript library. | [Step 5](step5.html) |
| ...understand the basics of asynchronous code execution. | [What is asynchronous code execution?]({{site.baseurl}}/explanations/asynchronous-code.html) | 
| ...understand the basics of how clients (like websites) interact with a backend to access data. | [What is a backend and why do I need one?]({{site.baseurl}}/explanations/backend.html) |

## DURING

You've got a simple website, and it reads and writes data! To the cloud!

That's pretty legit. But there's some more stuff you should probably do. You might have some of these questions:

**Wait a second, what's preventing anyone from writing and reading all the data in my database? Or deleting it? Or keeping random stuff in my database that doesn't have anything to do with talk recommendations?**

Nothing. You're right to be concerned about that. You should probably edit the awful security rules we added in [Step 3](step3.html) and replace them with better security rules. Read the [Security docs](https://firebase.google.com/docs/reference/security/database/) on Firebase to learn how to limit access to your database, and validate that requests are sending the right kind of data.

**What if I want people to be able to log in to my website/app? Can I have users?**

Yes, you can! Firebase makes it very easy for you to add users. They can log in via email/password, or by authenticating with Google/Facebook/Twitter/GitHub. You can also have anonymous user sessions! Learn more in the [Authentication docs](https://firebase.google.com/docs/auth/). If you're security minded, you can even use your Users data to prevent someone from seeing data that isn't theirs while using your app.

**Okay so this works on my machine, but how do I share this with other people?**

You'll want to host your static assets (i.e. your HTML/Javascript/CSS/images) somewhere, and give people a URL to that place. If you don't already have a hosting platform, you can host your website with Firebase. Check out the [Hosting docs](https://firebase.google.com/docs/hosting/) for more information.

**Websites are so 2000. I want to make an iOS/Android app. Can I still use Firebase?**

Yeah you can! Although all of these examples use Firebase's [Javascript library](https://firebase.google.com/docs/web/setup), they also provide an [iOS library](https://firebase.google.com/docs/ios/setup) and an [Android library](https://firebase.google.com/docs/android/setup).

**What if I'm not writing in Javascript, or for iOS or Android?**

Those libraries are built to abstract away the details of Firebase's REST API. You can use the API directly by sending HTTP requests to Firebase endpoints directly. Learn more in the [REST docs](https://firebase.google.com/docs/database/rest/start). There are some helpful third-party libraries already provided for common languages like Python and Ruby, but you can also write the requests yourself if you're working in a different language or you want an extra challenge.

### EXTRA CREDIT

1. Add some security rules to your database, so that only your website can read or write data to your database.
    - [Security & Rules](https://firebase.google.com/docs/database/security/) - guide to setting up security for your Firebase
    - Hint: if you don't want to authenticate with users yet, you probably want to give your website access to a **secret** and authenticate with that secret. However, this isn't a great option if you want to host your website. You'll have to make that secret public in order to give it to your website, which sort of defeats the purpose.
2. Automatically log in all users anonymously and require authentication to write data to your database.
    - [Anonymous Authentication](https://firebase.google.com/docs/auth/web/anonymous-auth) - guide to anonymous authentication with the Javascript library
3. Add some validation rules to your database, so that only data with required fields and appropriate security rules can be written.
    - [Securing Your Data](https://firebase.google.com/docs/database/security/securing-data) - guide to adding security rules to your Firebase database
    - [.validate](https://firebase.google.com/docs/reference/security/database/#validate) - documentation on the `validate` rule
4. Host your website using Firebase's hosting service so that other people can also add their recommendations to your database.
    - [Hosting Quickstart](https://firebase.google.com/docs/hosting/) - guide to hosting your static assets with Firebase
5. Allow users to log in with Facebook/Twitter/Google/GitHub and save the recommender's user id with the recommendation data.
    - [User Authentication](https://firebase.google.com/docs/auth/web/google-signin) - guide to authenticating users with Firebase's Javascript library
    - [User Based Security](https://firebase.google.com/docs/database/security/user-security) - guide to setting up security rules related to user authentication
6. The free version of Firebase limits how many connections to the database you can have at a time. Figure out when you don't need to persist your connection to the database, and turn off your connection.
    - [firebase.database.Database.goOffline()](https://firebase.google.com/docs/reference/js/firebase.database.Database#goOffline) - documentation on the `goOffline()` method of Firebase's Javascript library
    - [firebase.database.Database.goOnline()](https://firebase.google.com/docs/reference/js/firebase.database.Database#goOnline) - documentation on the `goOnline()` method of Firebase's Javascript library
    - [Firebase Pricing](https://firebase.google.com/pricing/) - explanation of limits on free tier

### EXTRA, EXTRA CREDIT

Made it this far? Here are some more ideas for cool things you can do with your website using Firebase. Have fun!

1. Allow users to set up their own username and display the username of a user along with their recommendation.
2. Allow users to see all their previous recommendations in one place.
3. Allow users to edit one of their previous recommendations (but prevent them from editing any recommendation they did not originally submit).
4. Allow users to toggle a setting so that their recommendations are private (i.e. no one but that user can read their recommendations).
5. Add a field to each recommendation indicating a vote score and allow users to "upvote". You'll need to watch out for race conditions, and make sure that only one request can edit the score of a recommendation at a time. (Hint: check out [`Reference.transaction()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#transaction))

## AFTER

You can use advanced features of Firebase by reading documentation and guides. (This is a big deal, you know - the ability to learn and teach yourself new skills is highly valued in tech.)

You are a data wizard and you can do magic and build awesome things. Use your powers for good, and let me know if this tutorial has helped you make something cool! (You can reach me [@mariechatfield](http://twitter.com/mariechatfield).)
