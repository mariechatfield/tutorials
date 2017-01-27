---
layout: tutorial
title:  "JavaScript App | Step 7: Deploy to Heroku"
tutorial_overview: web-app
previous_step: step7.html
---

---

## Pre-requisities

| You should... | What to Review |
|------------ |-------- |
| ...  pushed your app to a new GitHub repository| [Step 6](step6.html) |

---

### Create a new Heroku account

Sign into your existing [Heroku](https://heroku.com) account, or create a new one. (They're free!)

Follow the instructions to download and install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).

When you first install the CLI, you'll have to [enter your Heroku credentials](https://devcenter.heroku.com/articles/heroku-cli#getting-started) to connect the app with your Heroku account.

To verify that you've successfully installed the Heroku CLI, try `heroku --version` on your command line. You should see some version output.

```bash
~/projects/my-new-app $ heroku --version
heroku-toolbelt/3.43.14 (x86_64-darwin10.8.0) ruby/1.9.3
heroku-cli/5.5.2-e6595d8 (darwin-amd64) go1.7.3
You have no installed plugins.
```

### Create a new Heroku app

You're now ready to create your first Heroku app!

From within `my-new-app`, run `heroku create`. This will create a default app for you, and give it a unique name.

```bash
~/projects/my-new-app $ heroku create
Creating app... done, ⬢ agile-springs-63142
https://agile-springs-63142.herokuapp.com/ | https://git.heroku.com/agile-springs-63142.git
```

If you visit the link from the output, you'll see a generic landing page.

![Heroku landing page]({{site.baseurl}}/assets/web-app/screenshot_heroku-landing-page.png)

When you created your app, Heroku added a new remote to your local git repository. You can see it by running `git remote -v`:

```bash
~/projects/my-new-app $ git remote -v
heroku  https://git.heroku.com/agile-springs-63142.git (fetch)
heroku  https://git.heroku.com/agile-springs-63142.git (push)
origin  git@github.com:mchat/my-new-app.git (fetch)
origin  git@github.com:mchat/my-new-app.git (push)
```

Heroku has a concept of [buildpacks](https://devcenter.heroku.com/articles/buildpacks), which are a set of scripts which build your deployed into a functional app. For our app, we're first going to set up the Ember server. We'll need to use the [Ember buildpack](https://github.com/heroku/heroku-buildpack-emberjs).

Install the Ember buildpack with `heroku buildpacks:set https://codon-buildpacks.s3.amazonaws.com/buildpacks/heroku/emberjs.tgz`:

```bash
~/projects/my-new-app (master) $ heroku buildpacks:set https://codon-buildpacks.s3.amazonaws.com/buildpacks/heroku/emberjs.
Buildpack set. Next release on agile-springs-63142 will use https://codon-buildpacks.s3.amazonaws.com/buildpacks/heroku/emberjs.tgz.
```

### Deploy your app to Heroku

You can now deploy your app to Heroku using `git push heroku master`.

This is going to take a while, as your app is being deployed and built. When your script finally stops running, run `heroku open` to open your newly deployed app in a new browser window.

You should see the exact same index site as you see locally!

![Index with text box and button]({{site.baseurl}}/assets/web-app/screenshot_index-with-input.png)

Try clicking around. You may notice: everything but clicking the `Say Hello` button works as expected.

The reason the 



---

## Review

**[Proceed to the next step.](step7.html)**
