---
layout: tutorial
title:  "JavaScript App | Step 3: Add more content to your Ember app"
tutorial_overview: web-app
previous_step: step2.html
next_step: step4.html
---

---

## Pre-requisities

| You should... | What to Review |
|------------ |-------- |
| ... have created a new Ember app using Ember CLI | [Step 2](step2.html) |
| ... be running your Ember app locally | [Step 2](step2.html) |

---

### Add content to the index route

Currently, our Ember application isn't rendering any content based on the route — it's only rendering content for the entire application.

Given our URL `http://localhost:4200/`, Ember is going to render our index route and template. (Specifically, this is because the URL ends with `/`, which is a shorthand for `index.html`.)

Let's add an index template with `ember generate template index`:

```
$ ember generate template index
installing template
  create app/templates/index.hbs
```

Open `app/templates/index.hbs` and add some content:

```hbs
<h3>This is the index route.</h3>
```

Go back to `http://localhost:4200/` in the browser. **Nothing should change — we'll still see Hello world without our new content.**

This is because we're not allowing our parent `application` route to render any content from its child routes.

We'll need to add an [`outlet`](http://emberjs.com/api/classes/Ember.Templates.helpers.html#method_outlet) to `app/templates/application.hbs` so that any child routes can render their own content.

{% raw %}
```hbs
<h1>Hello world.</h1>

{{outlet}}
```
{% endraw %}

Note that the curly braces around `outlet` indicate here that this is a Handlebars helper, and not straight HTML. This only works because Ember parses Handlebars templates into HTML before asking the browser to render it.

Now if we look back at `http://localhost:4200/`, we should see both the heading from our `app/templates/application.hbs` and our `app/templates/index.hbs`:

![Hello World with Index Route]({{site.baseurl}}/assets/web-app/screenshot_hello-world-with-index.png)

### Add another route

We can add another route and see that the `application.hbs` content is still displayed there.

Let's make an About page. The index route is predefined in every Ember application, so we didn't have to explicitly create it. However, we'll need to create both the template and the route to get an About page to show up in our app.

`ember generate route about`

```bash
~/projects/hello-world $ ember generate route about
installing route
  create app/routes/about.js
  create app/templates/about.hbs
updating router
  add route about
installing route-test
  create tests/unit/routes/about-test.js
```

Ember CLI did a bit more work here. It added two new app files, updated our router, and then added a test file.

For now, let's just add some content to `app/templates/about.hbs`.

It should already be created with an `outlet`:

{% raw %}
```hbs
{{outlet}}
```
{% endraw %}

We can delete that and replace it with text:

```hbs
This is the about route.
```

If we now navigate to `http://localhost:4200/about` in the browser, we should see the application header and the about template.

![Hello World with About Route]({{site.baseurl}}/assets/web-app/screenshot_hello-world-with-about.png)

### Transition between routes

Let's make it possible to navigate between our routes without having to manually update the URL.

We can add some naviagation to our application by updating `app/templates/application.hbs`:

{% raw %}
```hbs
<h1>Hello world!</h1>

<ul>
  <li>{{#link-to "index"}}Home{{/link-to}}</li>
  <li>{{#link-to "about"}}About{{/link-to}}</li>
</ul>

{{outlet}}
```
{% endraw %}

This uses the [`link-to`](http://emberjs.com/api/classes/Ember.Templates.helpers.html#method_link-to) Handlebars helper to generate links to different Ember routes.

When we look back at our page, we should see two links to our two routes. We can click between them and see Ember automatically updating our view and URL based on which route we're looking at.

![Hello World with About Route with Navigation]({{site.baseurl}}/assets/web-app/screenshot_hello-world-with-about-with-links.png)

### Save changes

If you haven't already, this would be a good time to save all your changes with Git. You can stage all your changes with `git add -A` and then commit them with `git commit -m "your commit message"`.

```
~/projects/hello-world $ git add -A
~/projects/hello-world $ git commit -m "Add index route and about route."
[master b65ae85] Add index route and about route.
 7 files changed, 26 insertions(+), 1 deletion(-)
 create mode 100644 app/routes/about.js
 create mode 100644 app/templates/about.hbs
 create mode 100644 app/templates/application.hbs
 create mode 100644 app/templates/index.hbs
 create mode 100644 tests/unit/routes/about-test.js
```

---

## Review

You added content to the index route of your Ember application and learned about {% raw %}`{{outlet}}`{% endraw %} Handlebars helper and nested routes.

You created a new route and template using Ember CLI.

You used the Handlebars {% raw %}`{{link-to}}`{% endraw %} helper to add links to different routes in your application.

You have saved all your changes by committing them with Git.

**[Proceed to the next step.](step4.html)**
