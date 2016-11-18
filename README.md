# Google Pagespeed Insights 90-95 score website project

![Part of the Udacity Front-End Web Development Nanodegree](https://img.shields.io/badge/Udacity-Front--End%20Web%20Developer%20Nanodegree-02b3e4.svg)

## Overview

Optimised a slow website to perform between 90-95 on Google Pagespeed Insights.

## Installation

1. Fork the repository and clone to your desktop
2. Open index.html in your browser

### Tips if you wanna use Page Insights to examinne the page

1. You will need to run a local server on the directory. You can do this using phython. [Here's a great resource for running a HTTP server on your local director (http://www.linuxjournal.com/content/tech-tip-really-simple-http-server-python)]

2. Open a browser and visit localhost:8080 or the port number you specified

3. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

4. Run ngrok with ./ngrok http 8080


## Modifications to main.js

### Removed determineDx function

The first thing I did was to remove this function entirely. It was causing unnecessary jank and I didn't see the logic of do something like setting the width of a column in such a complicated way.

I left changeSliderLabel(size) as it. But then refactored the changePizzaSizes function. The widths of the pizza columns were always gonna be the same in percentages so I defined the directly in the switch cases. I also removed the "%" in the for loop.


### Deleted the function generator(adj, noun) & refactred the randomname function

The generator(adj, noun) function could be made irrelevant by adding the calls to the adjectives and nouns within the randomname function. I did this to make the function more efficient.


### Using requestAnimationFrame

I added requestAnimationFrame to to updatePositions call for more efficiency


### Using more efficient selectors

All across the board, I replaced instances of document.querySelectorAll with document.getElementsByClassName or document.getElementsByID - this was a tip from a Udacity forum post I stumbled upon.


### Pizza div creation in the for loop was unnecessary (line 520)

The var pizzasDiv = document.getElementById("randomPizzas"); within the for loop was overkill because the pizza div were being appended in the for loop itself


### Refactorinng updatePositions function

Phase value calculations

Most of the work went into optimising this function. The first thing I noticed was that the Phase values were always the same 5 values. So there was no need to be calculating these values within the for loop. So I moved the calculations out of the for loop and stored them in phaseArray. I could then call these values in the for loop by using the (i % 5) to cycle through each of the values repeatedly.

Obtaining the number of pizzas dynamically using window.innerHeight

200 pizza seemed like an overkill to me because at any given time you do not see 200 pizzas on screen. I created a global variable numberofPizzas = window.innerHeight / 256 * 8;

I then referenced numberofPizzas as the iterator instead of requiring 200 pizza to be generated each time because the number of pizzas that need to be generated really just depends on the visible window size.
