# Step 3: Write hard-coded data via the Javascript Library

## BEFORE

| You should... | What to Review |
|------------|--------|
| ...be able to view and manipulate data in your project's Database console. | [Step 2](step2_write_data_manually.md) |
| ...know **your-project-id**, the unique description of your database. | [Step 1](step1_setup.md) |
| ...understand the basics of how clients (like websites) interact with a backend to access data. | [What is a backend and why do I need one?](../../explanations/backend.md) |

## DURING

Manipulating data in our project's Database console is pretty cool, but not particularly useful for adding a lot of data or allowing other people to access the data.

Let's build out a simple website application. It's going to collect and display recommendations of **Talks You Should Watch**. For example, one of my favorite talks is [this TED Talk](https://www.ted.com/talks/chimamanda_adichie_the_danger_of_a_single_story) by Chimamanda Ngozi Adichie:

![TED Talk Screenshot](../images/screenshot_ted.png)

For each talk recommendation we want to collect:

* Title of the talk
* Name of the presenter
* Link to video recording of the talk

We probably want to assign each recommendation a unique ID so that we can keep track of it. Here's what a recommendation object might look like in our Firebase database:

![Recommendation object diagram](../images/diagram_app_recommendations.png)

If we wanted to represent my talk recommendation above as a JSON object, we could write:

```json
{
    "title": "The danger of a single story",
    "presenter": "Chimamanda Ngozi Adichie",
    "link": "https://www.ted.com/talks/chimamanda_adichie_the_danger_of_a_single_story"
}
```

Okay but how do we get that into our Firebase database? That's where our simple website comes into play.

![App Structure Part 1](../images/diagram_app_structure_01.png)

For now the website will only be available locally, on your computer. It will consist of two files, which should be located in the same directory (or folder) on your machine:

* application.html
* application.js

![App Structure Part 2](../images/diagram_app_structure_02.png)

**application.html** will define the layout of our website using HTML. It will also load **application.js**, which will perform different actions on our website using Javascript.

![App Structure Part 3](../images/diagram_app_structure_03.png)

Some of the actions defined by **application.js** will call out to our Firebase database to read or write data.

**application.html** will also load another Javascript file, which is the [Firebase Javascript library](https://firebase.google.com/docs/web/setup). Firebase provides this library to abstract away a lot of the work of making requests to the database.

**Before we take a look at the files, we need to update our project's security settings.**

Normally, we'd want fairly strict security settings, so that only people that should be using our app can read and write data. But to make developing our initial app a bit easier, we're going to change the settings so that anyone can read or write data. This means we can start developing without having to set up authentication.

From your project's Database console, navigate to the **RULES** tab.

![Database Rules](../images/screenshot_database_rules.png)

You'll see the default rules. Delete these and replace with the following rules, then click **PUBLISH**.

```javascript
// These rules give anyone, even people who are not users of your app,
// read and write access to your database
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

![Database Rules Updated](../images/screenshot_database_new_rules.png)

**Before publishing this app, you should update these rules and remove public read/write access without authentication.**

Okay, back to our regular programming. It's time to check out **application.html** and **application.js** and see how we're going to write data to our Database.

You can access the first version of **application.html** and **application.js** from the [`code_samples/v1`](https://github.com/mchat/tutorials/tree/master/firebase/code_samples/v1) directory of this tutorial.

#### Ways to view and edit code samples:

* Clone this repository from GitHub and open the files directly from the `firebase/code_samples/v1` directory on your local machine.
    - [Learn how to clone a repository.](https://help.github.com/articles/cloning-a-repository/)
    - [View the main page of this repository.](../../../../)
* Open the files [**application.html**](../code_samples/v1/application.html) and [**application.js**](../code_samples/v1/application.js). This shows you a nicely formatted version of the file. To access the raw file, click the **Raw** button at the top right of the file.
    - Right-click the raw file to save directly to your local machine.
    - Or, copy and paste the raw file into your text editor.
* Copy and paste the code below into your text editor.

Once you've saved these two files on your machine, open them in the text editor of your choice. They should look something like this:

####[application.html](../code_samples/v1/application.html)
```html
<html>
  <head>
    <!-- Load the Firebase base library before loading the body. -->
    <script src="https://www.gstatic.com/firebasejs/3.1.0/firebase.js"></script>
  </head>

  <body>
    <!-- Load the application script, which will save data to our Firebase app. -->
    <script src="application.js"></script>

    <!-- Honestly, we don't need this but otherwise this page is totally blank and it's kind of hard to tell that it's already loaded. -->
    <h1>Hello world!</h1>
  </body>
</html>
```

####[application.js](../code_samples/v1/application.js)
```javascript
// TODO: Replace with your project's config object. You can find this
// by navigating to your project's console overview page
// (https://console.firebase.google.com/project/your-project-id/overview)
// and clicking "Add Firebase to your web app"
var config = {
  apiKey: "<your-api-key>",
  authDomain: "<your-project-id>.firebaseapp.com",
  databaseURL: "https://<your-project-id>.firebaseio.com",
  storageBucket: "<your-project-id>.appspot.com",
};

// Initialize your Firebase app
firebase.initializeApp(config);

// Reference to your entire Firebase database
var myFirebase = firebase.database().ref();

// Get a reference to the recommendations object of your Firebase.
// Note: this doesn't exist yet. But when we write to our Firebase using
// this reference, it will create this object for us!
var recommendations = myFirebase.child("recommendations");

// Push our first recommendation to the end of the list and assign it a
// unique ID automatically.
recommendations.push({
    "title": "The danger of a single story",
    "presenter": "Chimamanda Ngozi Adichie",
    "link": "https://www.ted.com/talks/chimamanda_adichie_the_danger_of_a_single_story"
});
```

**Before these files will work, you'll have to replace the provided `config` object in application.js with your own project's `config` object.**

You can find your project's `config` object by navigating to your project's console overview page: __https://console.firebase.google.com/project/your-project-id/overview__. This was the first page we saw when we created our new project. You'll want to click the **Add Firebase to your web app** button.

![Project Overview](../images/screenshot_add_to_web_app.png)

That should open up a modal with some code. Copy just the `config` object (it should look similar to the code outlined in red below):

![Project's config object](../images/screenshot_project_config.png)

Replace the default `config` object in **application.js** with your copied `config` object. Now you're good to go!

Open **application.html** in any internet browser. It should work like opening any other website, but the URL will correspond to the path of **application.html** on your local machine instead of a proper internet address.

In the browser, you should see something that looks like this:

![Hello world!](../images/screenshot_hello_world.png)

Seems pretty boring. But go check your Firebase Dashboard.

![It added data!](../images/screenshot_add_first_recommendation.png)

There's data there! That you added! From a page on your computer!

And it added a really funky string thing. That's the unique URL of the recommendation object we just added. So if we wanted to reference that object, we could do something like:

So if we wanted to link directly to that object, we could open __https://your-project-name.firebaseio.com/recommendations/-KMpGWpa8JCkLUpNnlHW__.

![First recommendation](../images/screenshot_first_recommendation.png)

| ![Pause Point](../images/pause_point.png) | You just wrote data to a database in the cloud. That's so legit. If you've never done that before, go tweet about it or something. |
| --- | --- |

### EXTRA CREDIT

1. Move **application.js** to a different directory than **application.html** and figure out how to change the HTML file so that it still loads your Javascript.
2. Define `recommendations` in a single line of Javascript, instead of two. (Hint: read the documentation for the [`ref` method](https://firebase.google.com/docs/reference/js/firebase.database.Reference).)
3. Add another field to each recommendations object and update the Javascript to send this new field. Some ideas:
    * a number rating of the talk on a scale of 1 to 5
    * a text description of the talk
    * the name of the recommender
4. "Backfill" your existing recommendations objects by manually entering values for the new field in your database's Dashboard. You want to make sure that all the data in your database adheres to a consistent schema, and that it contains every field you expect it to have!

## AFTER

You can run and develop a simple website locally.

You can write hard-coded data to your database using the Firebase Javascript library.

**Step 4:** [Write user-generated data](step4_write_dynamic_data.md)
