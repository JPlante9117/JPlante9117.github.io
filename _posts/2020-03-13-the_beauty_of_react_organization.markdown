---
layout: post
title:      "The Beauty of React Organization"
date:       2020-03-13 17:03:34 +0000
permalink:  the_beauty_of_react_organization
---


When you code, organization is key. Sometimes, organization comes down to creating comments that separate your code in a few long files. Other times, it comes down to putting different files in different folders. The last thing that you would want is somebody to collaborate on your project and not be able to find what is going on when a bug appears, or be unable to change a typo simply because they cannot find where it is in the first place. That is what React does so well. Separating each piece into its own file and importing it when needed helps to keep code readable and organized.

## React Helps You Organize

There are two main pieces in React: Components and Containers. The only difference in them, technically, is which folder you put them in. In practice, however, there is a significant difference in what each one does. As somebody who has worked with Ruby a decent amount, I can liken it to the difference between the views and the instance variables called in the controller.

#### Components

React Components are like Ruby instance variables. These components are simply there to render a specific div and show specific data. My `Goal.js` component is not at all worried about what my `GoalForm.js` component is doing. All that each component is responsible for is itself (kinda self involved, don't you think?). 

#### Containers

These are the Ruby Views of React. When you are making a container, you are painting the page in a specific way. For example, in my application, I had a container called `Goals.js` that was responsible for rendering anything I wanted to see on the page such as Past Due Goals, Current Goals, Completed Goals, and a Modal. You can also think about containers like the director of a production: they tell the components where to be and when to be there.

## Why It Matters

React conventions helping to keep you organized does more than just keep code in certain files.

It keeps it **DRY** by calling the components when they are needed. When I needed to edit the way each goal looked, I knew I needed to make changes in `Goal.js` component and **only** that component. Additionally, when things aren't appearing where I think they should be on any of my pages, I know it is likely something in my Containers. I can make one change to a Goal and it will change everywhere on the application. Organization means **DRY code**.

It makes it **readable**. When I go back to look at some of my older applications, particularly the ones in JavaScript, I see a large file that has a bunch of functions called throughout. and I feel like there is a long string of function names I have to follow in order to find where a certain bug is happening. React, however, does not have this kind of issue. There is *some* passing of information between containers and components, but that is only one level, or two if you are working with grandparent containers. Like I was stating above, if there was a bug in my code, I knew to look in a specific file or two to find the fix for it rather than sort through 500 lines of code.

And finally, it's **inclusive**. What do I mean by inclusive? It uses JSX to make things much easier to work with. If I wanted to put an <h1> tag on the page, I put an <h1> tag in my component. I don't have to go through the mess of creating a dom element, setting it's attributes, and appending it to the page. I get to do everything inline, which makes it easy to work with. It removes **tons** of lines from my code just on HTML declaration alone. Plus, it's much less abstract to look at.

## Use React

All I can say after having used React is that I love using it. Even though it is more file switching than the JavaScript programs I had worked in, I feel like there is not really a downside to how things are handled. State can become a bit messy, but introducing Redux makes it much easier to manage.
