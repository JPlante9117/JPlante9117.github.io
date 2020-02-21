---
layout: post
title:      "The Impacts of Revisiting Projects"
date:       2020-02-21 16:06:21 +0000
permalink:  the_impacts_of_revisiting_projects
---


Last week, I submitted my JavaScript Project which was a simple organizer for my (extensive) game collection. It allows for me to sort the games by medium and then filter them further by name, player count, and more. Personally, I have found myself using this application already when having company over or just deciding what games I can play by myself at home. However, the target of this blog is not to gush over the personal usefulness of the app, but instead to focus on how looking at other people's projects made me **come back** to mine in order to make it even better.

## Design-Wise . . .

Looking at my project design wise, the first page looks very modern in terms of clicking a button and it loading the results. But the page that it loaded wasn't anything particularly special. It was a table with labeled columns. While useful, I thought it was kind of ugly after stepping away and coming back to the project. My cohort does a great job sharing their projects once finished, so I took a look at a few. Many of my colleagues with a strong grasp on web design used tiles. I then looked around on the internet for other examples. When I visit a website, sometimes there are tables, but more often I find myself seeing a more tiled design. I thought to myself, "How do I turn a table into tiles?"

After a moment of brainstorming (and scribbling in my art program on the look) I came to the conclusion that inline divs would be exactly what I'm looking for. I started by copying the formula for creating table rows and transferred them into creating divs on a page. Some CSS later, I ended up with this:

![](http://tinyimg.io/i/EZgNAmo.png)

I had to look up how to create some shapes with CSS like the trapezoids in the upper left and the magnifying glass in the bottom right, but I felt that it came out pretty close to how I wanted it to. In order to create a more unique look to each tile, I also added a "imageURL" attribute to my model which I used for the background image of each tile. I had to change a few fetch requests to make it all work, and in moments I had something I could easily work with as a user. With games rendering as tiles on the screen, I felt that the website looked much better quality than a simple table on the page. I still wanted to offer the ability to see everything on a table, though, so I created quick button that toggles between the tile view and the table view.

## Hosting-Wise . . .

After a little while, I started to research how to host this application online using Heroku and GitHub Pages. With the help of some of my colleagues, I was able to navigate the changes from the sqlite3 gem to the pg gem. After many hours of figuring out why the database still failed to be hosted, I ran the Heroku commands for migrating and seeding the database and had no issues ever since.

GitHub pages was easy to do, as I had hosted a short C++ Command Line game turned JavaScript already (if you're interested and enjoy factoring, go play my [Rune Number Game](http://jplante9117.github.io/RuneNumberGameJS)). Or so I thought.

Turns out, GitHub Pages needs the index.html to be on the root of the repository for it to work. It makes sense; how would it know which folder to go find the correct file in otherwise? I was faced with the challenge, though, of not wanting to move my index.html from the frontend folder. I instead researched a way to redirect you to the folder upon loading the page. This fancy snippet of code does the trick:

```
<meta http-equiv="refresh" content="0; url=https://JPlante9117.github.io/javascript_project/js_frontend/index.html">
```

Putting this line in the header tells the page to redirect to the supplied url in content, which in this case, will be the route to the index.html file I want to use.

Before the page could interact with my database, I had to switch my BASE_URL variable (something I realized made changing database locations so much easier) to the Heroku database. Once done, I loaded up the page and after a moment, GitHub had everything up and running. One problem, though: my Heroku hosted database didn't have my data in it. Darn! I should have expected it (because why would it have sent my data when I never told it to), but it slipped my mind.

I started populating the database bit by bit, and then tested my filters. Strangely, none of them worked. That seemed odd. Why would they work on my local database, but not on my Heroku? The answer was actually really simple: **it didn't work in either place**. I had completely forgotten to update the way filters were handled once I replaced the table with tiles!

## Functionality-Wise . . .

What I thought was going to be an hour of work migrating the database turned into a whole day of fixing bugs I forgot to test. I opened the console, scanning for errors, but nothing was being posted, at least not on the tile side. I swapped to the table view, and found that the way I was handling how things were generated, the table showed an error:

```
"cannot set style of undefined"
```

I looked into my code and found that the table was trying to also set the tile style in addition to itself. Since the tiles weren't on the page, it broke the code and stopped trying to update with the filters.

Great! This little piece in code actually saved me from tearing through my project trying to find what was wrong. In each of the filters, I had to determine what was being changed: the tile or the table. To do so, I used the boolean variable I had for the view toggle (called viewAsTiles) to determine which items we were grabbing. A few moments later, I got the name filter working with this:

```
function filterByName() {
    let input, filter, a, i, txtValue;
    input = d.getElementById("filterField");
    filter = input.value.toUpperCase();
    let items
    if (viewAsTiles){
        items = d.getElementsByClassName('gameContainer')
        i = 0
    } else {
        items = d.getElementsByTagName('tr');
        i = 1
    }
    for (i; i < items.length; i++) {
        if (viewAsTiles){
            a = items[i].getElementsByTagName("p")[0]
        } else {
            a = items[i].getElementsByTagName("a")[0]
        }
        txtValue = a.textContent || a.innerText;
        if (txtValue.toUpperCase().indexOf(filter) > -1) {
            items[i].style.display = "";
        } else {
            items[i].style.display = "none";
        }
    }
}
```

That was easy enough! I just had to change around a couple lines: change what 'items' stood for, change the value of i to accomodate the presence (or lack thereof) of a table header row, and grab the right kind of tag for the name attribute.

I went to apply the same logic to the rest of the filters, but very quickly ran into an issue: the tiles **don't** have any of the genre, player, playtime, or challenge information on them anywhere! This meant that I couldn't use the same kind of logic in doing the other filters...or could I?

I took a step back a moment and thought to myself, "Self, how do you pass information in HTML that is GRABBABLE but not visible?" The answer came quickly. I could do it the same way I was doing the filtering in the first place: ```something.style.display = "none"```

I could create invisible divs inside each of the tiles, give them a class that could identify them, and store the information there. It was perfect! I went up to the portion of my code handling the creation of game tiles and created these invisible divs. The rest of the filters came easily after that point since I could do the same process as the name filter.

## Conclusion . . .

Looking at other projects got me thinking on how I could improve the design of my own project. I was able to revamp the idea aesthetically, and in turn that required me to revamp a few ideas physically. I'm sure that in a few weeks, I will come back to this project again and change things around and repeat this process. Being able to continually improve my project makes me feel right at home in the new career path that I've chosen.

If you'd like to take a look at the project mentioned here, you can visit [my Game Organizer](http://jplante9117.github.io/javascript_project) or take a look through [the repository](https://github.com/JPlante9117/javascript_project).

NOTE: If the website hasn't been used in a while, the server might be asleep. Give it a moment after your first click to wake up, and you'll have speedy service thereafter!
