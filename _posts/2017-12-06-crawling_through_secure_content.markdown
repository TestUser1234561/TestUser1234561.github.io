---
layout: post
title:      "Crawling through secure content"
date:       2017-12-06 23:46:23 +0000
permalink:  crawling_through_secure_content
---


One of the biggest challenges while programming my steam web scraper was being
redirected to different user verification pages when trying to scrape data from
any games with mature content.

While debating whether I should ignore any pages with that redirected to an
unknown page I played around with the steam website to figure out if there is
any way to bypass the age verification. Luckily while playing around in the web
inspector I noticed that steam stores cookies when a user submits a birthdate or
agrees to view mature content.


![](https://i.gyazo.com/20689cf91ecd2a3f6889c7448af1ef5e.gif)


Awesome! A way to bypass these code braking pages, now all we need is to figure
out how to set custom cookies when opening a page with OpenURI and Nokogiri!
Sadly, after many attempts at searching and implementing different methods of
supposedly setting cookies in OpenURI nothing would work. This is when I
stumbled upon a very useful gem called
[Mechanize](https://github.com/sparklemotion/mechanize).

Mechanize is built on top of Nokogiri so implementing the new gem for scraping
was surprisingly simple, just switch `Nokogiri::HTML(open(url)) ` to
`Mechanize.new ` and load the page with `mech.get(url) ` after that all your
original Nokogiri code will work exactly the same! Now to the useful stuff,
Mechanize adds many extra features that are useful for scraping, like link
following and form submission, but what we need here is the cookie saving a
loading feature.

All we need to do now is add in our custom cookies to get past these pesky
verification pages. Since there isn’t much documentation on the cookie feature
or how to write the file that the cookie method loads I found the best way was
to simply load a page and use the `cookie_jar.save ` method that will simply save
a YAML file with any generated cookies inside of it.

After inspecting the file, we can simply add the cookies that we see load when
accepting any verification prompts we get in browser, for my case on
steampowered.com I found that for all the pages that I encountered we can get
past by setting `mature_content = 1`, `lastagecheckage = '1-January-1965'`, and
`birthtime ='-725833799'` then were done! Now when we try to load any game page
we simply go directly to it instead of getting redirected to an age or mature
content verification and breaking our code.


