---
layout: explanation
title:  "What is a backend and why do I need one?"
---

When we talk about web development, we can usually think in terms of **clients** and **servers**.

Users interact directly with **clients** such as websites or mobile apps. These clients then send requests over the network to **servers**, which are programs that are running on some machine somewhere in the world.

![Backend Diagram]({{site.baseurl}}/assets/backend/diagram_backend_01.png)

Servers are typically written in a language like Java/Ruby/Python/whatever you want really. Their main purpose is to run continually and listen to requests, and then serve back content depending on the type of request.

One type of content that a server might provide is **static assets**. Static assets refers to content that doesn't change. We typically refer to serving these assets as **hosting**.

For example, if we both log into Twitter in a web browser, we'll see the exact same HTML, styled by the exact same CSS, and manipulated by the exact same Javascript.

We'll see different Tweets in our feed, because we'll have different data. But the layout and style of the website is the same for every user.

![Backend Diagram with Static Assets]({{site.baseurl}}/assets/backend/diagram_backend_02.png)

Some clients (like websites) load all their static assets from a server. When you don't have internet access and you try to go to a website, there's a completely blank page because your browser can't make any requests to the server where all the HTML for that website lives.

Other clients (like mobile apps) store their static assets locally. When you first install an app on your phone, you download all the assets from a server. You can use an app without internet access because those static assets are stored on your phone.

Mind you, that app without internet access might not be particularly interesting. Most of the truly fun things we do with apps and websites requires some sort of data, which is another type of content that servers provide.

![Backend Diagram with Database]({{site.baseurl}}/assets/backend/diagram_backend_03.png)

Clients access servers that can store and serve data from a database. But databases (and servers) can be tricky to set up and manage over time. They should always be running and available, they should respond to requests quickly and accurately, they might want to enforce some security rules. They also take money to run — from the machines themselves to the electricity and internet they require.

There are different tools and companies that offer to take care of these problems for you, sometimes referred to as "Backend as a Service" (BAAS).

![Backend in the Cloud Diagram]({{site.baseurl}}/assets/backend/diagram_backend_04.png)

You might want to use these services because they simplify your life and can cost less than setting up your own backend. From your perspective, you just get to send off requests from your clients to the ambigious **cloud**, which exists somewhere in the internet. And it returns your data or assets to you.

Those machines running those servers and databases still exist, but they aren't your problem anymore. You can just focus on doing what you want to do with the content being served, or how to improve the content that you store.