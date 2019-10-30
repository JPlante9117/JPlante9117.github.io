---
layout: post
title:      "Finding Your Inner Scraper"
date:       2019-10-30 19:55:00 +0000
permalink:  finding_your_inner_scraper
---


After many days of working on the CLI Project, I have finally finished everything out! The journey wasn't easy, especially not at first. I went through nearly two full days of trying to figure out ways to scrape the websites I was looking at. I kept getting stuck due to JavaScript, forms, and filters that were making scraping incredibly unpredictable and sometimes inaccessible. After these two days, the motivation was being drained out of me, but I finally landed on GameStop's website, and I thought to myself that this looks more approachable than others have been.

The first level of scraping on the homepage was easy enough. I had decided to select the new games that are out and the games that are coming soon. The main page nicely has these two sections split inside the HTML, so it was easy to scrape. Each game was created as an object with a title and URL attribute.

# The Challenge . . .

This was the portion where the main challenge began. The second level of scraping was going to use the url associated with each game to scrape more information about each game. The challenge, however, was that the URLs were inconsistent. Some of them went directly to the information page, others went to a collection of all merchandise of that game, and others led to a search of that title.

How do we deal with that?

On the second level of scraping, I decided to check what type of url I received.

* If it was a direct page, nothing changed
* If it was a collection, translate the url to a search page based on the title.
* If it was a search page, iterate through the items on the page to find the specific item that matches the title of the game exactly, and set the url to that direct item url.
* If no titles match, then use the most relevant option (the first)

The game's URL attribute is changed to this result.

# The Calm After . . .

Once this piece was working, all the work comparatively was really easy to deal with. I initially wanted to have the title, ESRB, release date, publisher, user rating, price, and platforms. However, the pages were all inconsistent with how user reviews were accessed, and the one uniform place was littered with JavaScript that made it unable to be scraped with what I was using. Instead, I passed on that one piece and used the rest.

Each game was updated to have the newly scraped information as an attribute. Multiple scrapes are prevented by only scraping this page if that game does not have a price attribute.

# The Polish . . .

Then came the really fun part! Once things completely work, you can play around with how things look and making things super efficient. I worked hard to make my code DRY, and I wrote flexible methods that can be used between the different sections of the code. I implemented the Colorize gem to make the CLI look pretty!

# The Gist . . .

Basically, the most important thing I learned from this is that scraping can be difficult to manipulate at times, but once you get a greater understanding of it and have some patience while working, you can get a lot done with just a few lines of code.
