---
layout: post
title:      "When You're Obsessed . . ."
date:       2019-12-02 17:10:23 +0000
permalink:  when_youre_obsessed
---


For the Sinatra Project, I bounced around several ideas as to what the focus of the projecet should be. My wife had suggested creating a type of forum that allowed users to share recipes with one another and suggest recipes based on what you had in the fridge. I additionally thought about listing reviews for board games, since they are a personal hobby of mine. As I kept starting each idea, I found that it just wasn't something that I wanted to do for this project and scrapped each idea early on.

That was until I decided that I could take one of my current obsessions and apply it to this project: Pokémon.

I've been playing Pokémon Sword for a while now every morning before I began coding, and I had just finished the game's Pokédex. It was easy to say that I was (am) a bit obsessed about the game and the series as a whole, so I decided that I could create a website that made entries for the different Pokémon in the game as if researching them myself! I've always wanted to do that as a kid and decided to seize this opportunity.

# The Design
I thought about what would be necessary as models for this kind of project. It seemed fairly straight forward that I needed Pokémon, Assistants  (Users), and Entries. I considered a few more pieces like Moves and Types, but I found that things were going to be a bit too difficult to run that way.

Assistants only needed a few pieces of information. They had to have a name and a password. They needed to be able to write entries and have many of them. The model and table for them came together very quickly as there was not too much information required of them.

Entries needed to have content, and needed to be associated with an Assistant and a Pokémon. Their model and table came together even quicker than that of the Assistant.

Pokémon, on the other hand, proved to be a bit more of a challenge. It was not because the process was any different, but because I was getting in my own way. In  my mind, I had been playing a game in which Pokémon have species, two types, abilities, moves, natures, genders, and six different stats. I mulled over how to tackle all of this data but ultimately landed on breaking things into digestable pieces. The main pieces that most people see when they take a peek into Pokémon is that they have a species, such as Pikachu, and a type, such as Electric. As such, those were the pieces that I decided to take into my design.

# The Map
Now that I had all of the pieces of data and models set up, I needed to teach my program how to navigate it all. RESTful Routes were very useful during this step with a few minor exceptions that we will get to later. I mostly needed to decide how to handle accessing specific Pokémon, Assistants, and Entries. It made sense for Entries to be accessed via I.D. number since I had them labeled as "Entry #1" and so on. Assistants and Pokemon, however, seemed like it would be a challenge to find what you want via the URL if you didn't already know an I.D. number. Instead, I decided that slugging them was the better way to go.

As I kept working on my website, eventually I passed it over to my wife to work with. She was having a good time clicking around on all the buttons and correcting some of my grammar, and ultimately asked me a few questions regarding what she could and couldn't do. She wanted to see if she could see all Pokémon of a certain type. She also wanted to make sure my tables were centered on the page.

The table was handled easily enough, but the Types made me challenge myself in how to perceive the RESTful Routes.

# To Be or Not To Be . . . RESTful
I talked this over with myself and with my professor and there was no clear answer. Types are a quality of Pokémon and only Pokémon (at least in terms of my website) so should it be accessed under the umbrella of "/pokemon/types"? If not, are they stand alone enough to be accessed through "/types"? Both sides could be argued either way, but I ultimately landed on the former.

My reasoning for this decision pertained to the quality of types. Since they were a feature of a Pokémon and not stand alone themselves, it did not make sense to me to give them their own controller and route. Additionally, each type pointed back to a list of Pokémon. The strict relationship of Pokémon and their types made it seem silly to give them their own section.

The issue, then, came with how do you handle naming the ERB files appropriately. I decided to go with a method of naming them by what they were associated with. Since there was going to be a webpage for ALL Types, it functioned as an index page. I named it "types_index.erb". A specific type was then listed as a show page using the same format.

# Is It My Job To Make It Pretty?
This was one of the first questions that came out of my wife's mouth when she was playing around with the site. She had said to me, "I like that there are things to do and it is very functional. Is it your job to make it pretty, or would that be somebody else's responsibility?"

And that sat with me for a moment. It came down to identifying who else was working on this project. Nobody. So yes, it was my job! In other cases, I may have had a team with some people working specifically on UX/UI while I worked on the back end. However, this is not the case on my project.

I immediately got to work coloring the website the same as the famous red of the Pokédex. Additionally, I styled my tables to be nicer looking. I found a way to format my tables based on the Pokémon's type and give it a different color, which made it feel great!

I was then left with an awesome looking website with some pretty ugly grey square buttons. I knew I needed to change those, too, but wasn't sure how to at first. I researched replacing the appearance of buttons with CSS as well as the standard button dimensions (88px x 31px) and got to work.

I opened up a program I use for art called ClipStudioPaint and created these buttons! I used inspiration from the most recent game to create  the icons, having read through the fair use of products for Nintendo. After several hours of playing around with them, I got to the point you see now!

The only challenge was the form buttons(submitting, editing, and deleting) were not giving the same visual response as my other buttons since the cursor didn't change. I was playing around with trying to get them to be different button types, but I ultimately found that there was just a CSS feature that did it for me called "cursor."

And with that, it was indeed pretty.

# Reflection
Overall, I'm very pleased with my project. I understand that it plays hard into my nerd knowledge, but I also believe that is a firm part of who I am. Anyone looking to hire me will quickly learn that I am somebody who loves games and has a passion for many things in the nerdy and geeky realm. Once the project "looked pretty" I couldn't help but smile as I clicked around the site and pressed all my different buttons.

The most challenging part of the entire process was holding back myself from geeking out on the project and biting off more than I could chew. I didn't need to recreate Pokémon on this site, I just needed to highlight them.
