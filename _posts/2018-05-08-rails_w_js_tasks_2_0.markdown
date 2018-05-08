---
layout: post
title:      "Rails w/ JS: Tasks 2.0"
date:       2018-05-08 23:37:14 +0000
permalink:  rails_w_js_tasks_2_0
---



It’s been an interesting few days refactoring the initial version of the Tasks
app into a single page application, roughly 50% of the templates have been
removed or modified to fit somewhere else and substantial amounts of controller
code has simply disappeared as it’s no longer needed to power the server side of
the application. Subsequently the JavaScript required to replace the controller
is much more copious then the initial state of the app, especially since were
basically turning the client into a kind of pseudo-controller that navigates the
user around for us. But after finishing up the JavaScript adding a touch of CSS
and some nice quick animation you get a sleek single page app up and running.

One thing I noticed after finishing the SPA setup for Tasks is that for a tool
that allows users to work together and is quite responsive and quick to update
for a solo user, its lacking in updating the page when multiple users make
changes to a project. The solution I found for this was luckily a feature that
was already built into rails called Action Cable. Action Cable is a web socket
client / server setup already build to communicate between the user and the
rails server. Since with regular http the user only makes requests and gets a
response we can’t tell the user that there’s been an update to the page, but
with web sockets there is a persistent connection that allows the server and the
client to communicate with each other with no need for page loads or ajax calls.
Simply hooking up the web socket and telling the client to update whenever a
change is made to the project we can run an ajax fetch and update the page DOM.
Using this method, we get a very nice page that is always up to date with what
the server has!

