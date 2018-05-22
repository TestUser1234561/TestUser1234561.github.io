---
layout: post
title:      "Redux Project: DigiCI"
date:       2018-05-22 03:08:08 +0000
permalink:  redux_project_digici
---


For my final project I decided to make a ‘simple’ CI tool, however the current product falls a little short. A continuous integration tool should automatically clone, build, and test a repositories code and report back to the server with the results. The server should then push working code to the production environment, and release the binaries, with any number of extra features. Currently DigiCI has code cloning (to a fresh ubuntu server), building, and testing with reports sent back to the user, so it’s not technically a CI tool yet, more of an automated build and test system. There’s so much more that could be added to this project to truly make it a CI tool, however, I feel like adding more features would exceed the scope of what is mainly a front-end project. Currently DigiCI is a smooth one-page app that can pull, execute, and test any type of code on a Linux based system with live reporting and viewable statuses with logs. It was a fun but tedious project, and I’m pleased with how it turned out.
