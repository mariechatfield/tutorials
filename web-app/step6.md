---
layout: tutorial
title:  "JavaScript App | Step 6: Create a new GitHub repository"
tutorial_overview: web-app
previous_step: step5.html
next_step: step7.html
---

---

## Pre-requisities

| You should... | What to Review |
|------------ |-------- |
| ... have created an Ember route with a dynamic segment | [Step 5](step5.html) |
| ... saved all your changes | [Step 3](step3.html) |

---

### Create a new GitHub repository

Sign into your existing [GitHub](https://github.com/) account, or create a new one. (They're free!)

When you're signed in, you'll want to create a new repository. There should be a small plus (+) sign at the upper right corner. Click that and choose `New Repository`, or navigate directly to [https://github.com/new](https://github.com/new).

![Click New Repository]({{site.baseurl}}/assets/web-app/screenshot_github-new-repo-dropdown.png)

Give your repository a name that matchees your local directory (i.e. `my-new-app`) and click the `Create repository` button.

![Click New Repository]({{site.baseurl}}/assets/web-app/screenshot_github-new-repo.png)

You'll see directions to push an existing repository via the command line. Copy and paste those instructions into your command line.

![Directions to push repository to GitHub]({{site.baseurl}}/assets/web-app/screenshot_github-push-directions.png)

You should see something like this:

```bash
~/projects/my-new-app $ git remote add origin git@github.com:mchat/my-new-app.git
~/projects/my-new-app $ git push -u origin master
Counting objects: 64, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (53/53), done.
Writing objects: 100% (64/64), 10.85 KiB | 0 bytes/s, done.
Total 64 (delta 11), reused 0 (delta 0)
remote: Resolving deltas: 100% (11/11), done.
To github.com:mchat/my-new-app.git
 * [new branch]      master -> master
```

**Note:** you may be asked to provide your GitHub username and password on the command line if you are using HTTPS protocol. This is the default protocol. If you don't want to always enter your username and password, you should follow the instructions to [set up an SSH key](https://help.github.com/articles/about-ssh/) to authenticate your laptop with your GitHub account.

When you've successfully pushed your repository to GitHub, your repository page should show the same files you have locally (instead of the directions to set up a repository).

![GitHub repository with initial commits and files]({{site.baseurl}}/assets/web-app/screenshot_github-repo-with-initial-commits.png)

If you run into issues, check out the [GitHub help center](https://help.github.com/).

---

## Review

You created a new GitHub repository.

You pushed your local git repository to GitHub.

**[Proceed to the next step.](step7.html)**
