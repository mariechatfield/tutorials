---
layout: tutorial
title:  "JavaScript App | Step 1: Set up your development environment"
tutorial_overview: web-app
next_step: step2.html
---

---

## Pre-requisities

|--- 
| ![Pause Point]({{site.baseurl}}/assets/general/pause_point.png) | [What is a backend and why do I need one?]({{site.base-url}}/explanations/backend.htmlz) |

---

### Why JavaScript?

In this tutorial, we're going to use JavaScript to write a simple client web app and server.

JavaScript is the only programming language available in most modern browsers, so if you want to write scripts that can run on a website, you're going to have to use JavaScript.

You can also run JavaScript directly from your computer (instead of inside a browser) by using [Node.js](https://nodejs.org). Node.js is built using the same engine that runs JavaScript inside Chrome browsers, and can be used on most operating systems.

Node.js also comes with [npm](https://www.npmjs.com/) (node package manager), which is a powerful way to manage and install dependencies for JavaScript. npm allows you to easily use open source libraries in your own code, consistently across all contexts and machines.

One benefit of using JavaScript for your server-side code is that you can use a single language across your entire stack. As long as you've got Node and a browser installed on your machine, you can devlop a full web application with JavaScript.

Typically, if you decide to use JavaScript for a web application, you'll want to use frameworks (or libraries) that provide abstractions and handle common problems and requirements. These frameworks aren't strictly necessary, but they make writing web applications much faster and it's generally not recommended to write an app without one.

We'll build our client web app using [Ember](emberjs.com) and our server using [Express](http://expressjs.com/).

### Open the command line

This tutorial will largely consist of various commands to run in the command line. You can typically find your command line in a terminal app.

**The commands I'll be providing are written for Mac OS.** Most Linux machines will have fairly similar, if not identical, syntax. (That's because Mac OS and Linux are both descended from the UNIX operating system.) Windows typically has different syntax, so you may have to adapt these commands.

Some words that we'll be using:

* `command line`: a way of interacting directly with your computer via text prompts
* `CLI` (`command line interface`): a tool or program that runs via the command line. Instead of opening up as an application in its own window, you interact with this program via text commands.
* `shell`: a program that accepts commands as text input, and then displays any output from running those commands ([bash](https://www.gnu.org/software/bash/) is a well-known shell for UNIX machines)
* `terminal`: an application that runs one or many shells. May be used interchangeably with shell. Both OSX and Linus typically ship with an application named Terminal, but you can also install other terminal applications with extra features (like [iTerm](https://www.iterm2.com/version3.html)).
* `prompt`: the part of a shell where you provide text input. Typically, a shell will output some information before the prompt, which you can customize. The last character before the prompt is typically `$`.

Given a snippet like this:

```bash
some-dir $ echo "This command will output the quoted text on the next line."
This command will output the quoted text on the next line.
```

* `some-dir` is the name of the current directory. This is output by the shell. (Your shell may very well look different from this example.)
* `$` indicates the prompt, or end of the automatic output by the shell.
* `echo "This command will output the quoted text on the next line."` was typed by the user into the shell. The user then hit `enter` to make the shell evaluate the command.
* `This command will output the quoted text on the next line.` is the output printed by the shell after the `echo` command was run.

### Install Node.js

Before we can begin to write any code, we need to install all the software and tools we'll be using.

The first thing you'll need to do is [**install Node.js**](https://nodejs.org/en/download/) on your machine.

To see if you already have Node installed, try running `node -v` and `npm -v` in the command line. If Node is correctly installed, you should see versions output like this:

```bash
$ node -v
v6.9.1

$ npm -v
3.10.8
```

The precise version of Node doesn't matter — although if you have a very old version of Node, you may need to upgrade it.

If you don't have Node installed, you'll need to do so now. You can [download an installer directly from Node.js](https://nodejs.org/en/download/). Alternatively, you can [check if your preferred package manager supports Node](https://nodejs.org/en/download/package-manager).

Once you've downloaded Node via your preferred method, try running the two commands `node -v` and `npm -v` to ensure that everything is working correctly.

### Install Ember CLI

We're going to build our client side app with the Ember framework. Ember helpfully provides a command line interface called [Ember CLI](https://ember-cli.com/).

We can use Ember CLI to set up our base application, add new pieces, build our app, run it locally, test our app and more.

To get started, we can install Ember CLI using npm (which was installed with Node).

`npm install -g ember-cli`

If you run this command, npm will download Ember CLI and make it available globally on your machine. (Without this option, npm will make the package only available in whatever repository you run the command in.)

To ensure that Ember CLI was installed correctly, run `ember -v`. You should see something like the following output:

```bash
$ ember -v
ember-cli: 2.9.1
node: 6.9.1
os: darwin x64
```

### Install Bower

In order to use EmberCLI, we'll also need to use the `bower` CLI. [Bower](https://bower.io/) is another package manager, that Ember uses for some of its own dependencies. You can install Bower using npm as well:

`npm install -g bower`

Verify that Bower was installed successfully by checking its version.

```bash
$ bower -v
1.8.0
```

---

## Review

You have installed Node.js and npm on your machine. You used npm, Node's package manager, to globally install Ember CLI and Bower.

**[Proceed to the next step.](step2.html)**
