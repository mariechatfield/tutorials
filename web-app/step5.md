---
layout: tutorial
title:  "JavaScript App | Step 5: Add an interactive Ember route"
tutorial_overview: web-app
previous_step: step4.html
next_step: step6.html
---

---

## Pre-requisities

| You should... | What to Review |
|------------ |-------- |
| ... be running the Ember server with `--proxy` option | [Step 4](step4.html) |
| ... be running the Express server with nodemon | [Step 4](step4.html) |
| ... have a server endpoint for `api/greeting` | [Step 4](step4.html) |

---

### Create an Ember route with a dynamic segment

Now that we have defined behavior for `api/greeting`, let's use it in our Ember app. We can define a new greeting route and template. We'll start out by generating a new route with Ember CLI, the same way we created the about route:

`ember generate route greeting`

```bash
~/projects/my-new-app $ ember generate route greeting
installing route
  create app/routes/greeting.js
  create app/templates/greeting.hbs
updating router
  add route greeting
installing route-test
  create tests/unit/routes/greeting-test.js
```

Our route will dynamically display a greeting, based on the response from our `api/greeting` endpoint in the server. That endpoint expects a `name` argument to be passed to it. We'll want to allow our route to define a name.

So, for example, if we go to `/sayHelloTo/Marie`, we expect to be shown a greeting for Marie. We'll want to define a custom path for our route first.

In `app/router.js`, a new `greeting` route should have already been added for us by Ember CLI:

```js
this.route('greeting');
```

Let's define a `path` override with a dynamic segment for our route. Instead of showing up when we visit `/greeting`, we want our route to show up when we visit `/sayHelloTo`. And right after that segment of the URL, we want some extra information about what name to display. This will be our dynamic segment, `:name`.

```js
this.route('greeting', { path: 'sayHelloTo/:name' });
```

If we visit `/sayHelloTo/Marie`, our `greeting` route will be invoked with `name: 'Marie'` as a parameter.

We want to do something with this parameter when our route is invoked, so we'll add a model hook. The [model hook](http://emberjs.com/api/classes/Ember.Route.html#method_model) allows us to turn the URL of the route into a JavaScript object that we can use as the model. Our hook should return a promise that will be resolved with an object. The object will be transformed into an Ember object. The route will wait to finish loading until the promise is either resolved or rejected.

Open `app/routes/greeting.js` and add the following `model` function:

```js
export default Ember.Route.extend({
  model(params) {
    // Get firstName from route params
    const escapedName = encodeURIComponent(params.name);

    // Send request to server, get JSON back, and return as model object
    return Ember.$.getJSON(`/api/greeting?name=${escapedName}`);
  }
});
```

The `model` hook is passed a `params` object, which describes any parameters passed to the route via its URL. We assume that `params` has `name` defined, then escape that input with [`encodeURIComponent`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) so that we can send it to the server.

Using jQuery's [`getJSON`](http://api.jquery.com/jquery.getjson/) method, then make a GET request to our back end server at `/api/greeting`, passing the name we've just escaped as part of the query string. When the server returns a response, `getJSON` parses the response as JSON.

`getJSON` returns a promise to the route's `model` hook. When the promise resolves with an object parsed from the JSON response, that object is transformed into an Ember object, and is accessible within our route as `model`.

We can now display our `model` in `app/templates/greeting.hbs`. In our back end server, definition, we return an object with `greeting` defined: `{ greeting }`. Let's render `model.greeting` in our template for the route.

{% raw %}
```hbs
<h2>{{model.greeting}}</h2>
```
{% endraw %}

Visit `http://localhost:4200/sayHelloTo/Marie` and you should see something like this:

![Greeting for Marie]({{site.baseurl}}/assets/web-app/screenshot_greeting-marie.png)

Try changing the end of the URL from `Marie` to some other name, then refresh the page and see what happens!

### Add input on index route

We could just keep adding names to the URL, but we might also want to be able to transition to our new route from within our app. Let's add a text input on our index page and allow users to define their own names.

Replace the content of `app/template/index.hbs` with the following:

{% raw %}
```hbs
{{input value=name}}

<button onclick={{action 'sayHello'}}>Say hello to {{name}}.</button>
```
{% endraw %}

We'll render an `<input>` whose value comes from `firstName` as defined on our index controller. We'll also include a button that displays "Say hello to ...". Whenever the text box's value changes, the button's label will automatically update.

When the button is clicked, it will invoke the `sayHello` action on our index controller.

The only problem? We don't have an index controller yet! Let's create one with Ember CLI.

`ember generate controller index`

```bash
~/projects/my-new-app $ ember generate controller index
installing controller
  create app/controllers/index.js
installing controller-test
  create tests/unit/controllers/index-test.js
```

Open `app/controllers/index.js` and let's define `firstName` and `sayHello`.

```js
export default Ember.Controller.extend({
  name: null,

  actions: {
    sayHello() {
      this.transitionToRoute('greeting', this.get('name'));
    }
  }
});
```

`name` will start out as `null`, but as the user types into the text box it will be automatically updated.

We also need to define `actions`, a hash with the `sayHello` function defined inside it.

When we `sayHello`, we want to take the value of the input and pass that as the `name` parameter to our `greeting` route.

We can use the [`transitionToRoute`](http://emberjs.com/api/classes/Ember.Controller.html#method_transitionToRoute) function to transition to the `greeting` route (note that we use the route's name, not its URL). We pass `this.get('name')`, the attribute to which the value of the text box is bound.

Navigate to `http://localhost:4200/` and you should see a text box and a button:

![Index with text box and button]({{site.baseurl}}/assets/web-app/screenshot_index-with-input.png)

As you type into the text box, the button's label will update too! Try typing `Marie`.

![Index with text box and button with user input]({{site.baseurl}}/assets/web-app/screenshot_index-with-input-from-user.png)

If you click the button, you should see the URL change to `http://localhost:4200/sayHelloTo/Marie` and the same greeting as before will appear:

![Greeting for Marie]({{site.baseurl}}/assets/web-app/screenshot_greeting-marie.png)

Try navigating back to index using the `Home` button and adding a different name to the text box.

### Save your work

If you haven't already, save your changes again! For a refresher on how to do this, see [Step 3](http://localhost:4000/tutorials/web-app/step3.html#save-changes).

---

## Review

You created an Ember route with a dynamic segment.

You created a new controller using Ember CLI, and defined an action.

You transitioned from one Ember route to another.

**[Proceed to the next step.](step6.html)**
