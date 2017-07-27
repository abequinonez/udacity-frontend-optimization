# Udacity Front-End Website Optimization Project

This project was developed as part of the Udacity Front-End Web Developer Nanodegree Program. With an understanding of the Critical Rendering Path and with the help of Google Chrome DevTools, the project guidelines called for speed and performance optimizations of an existing site. For index.html in the main directory, significant improvements have been made to increase its Google PageSpeed scores. For pizza.html in the views directory, various changes have been made to both views/js/main.js and views/css/style.css to improve the page's performance. See below for a list of the specific optimizations made.

## Instructions

1. After cloning or downloading this repository, you must upload the directory to an online web host. You may do this easily with GitHub pages. Paste either the main directory or the index.html link into [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights) and click the analyze button. Alternatively, you may visit the web page [here](https://abequinonez.github.io/udacity-frontend-optimization) and its PageSpeed Scores [here](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fabequinonez.github.io%2Fudacity-frontend-optimization%2F).

2. Next, open up the cloned or downloaded copy of views/pizza.html in a web browser. Alternatively, you may visit the page [here](https://abequinonez.github.io/udacity-frontend-optimization/views/pizza.html). For performance information, open the page in Google Chrome. Then open the DevTools Console by pressing ctrl + shift + j (Windows/Linux) or cmd + option + j (Mac). Reload the page and continually scroll through the page to print the page's performance information to the console. For more detailed performance information, you may analyze the page using the DevTools Performance tab.

## Optimizations

### Page Speed

index.html was optimized by:

1. Adding Google Web Font Loader to asynchronously download fonts
2. Moving all script tags (including the newly added Web Font Loader) to just above the closing body tag
3. Adding the 'async' attribute to the Google Analytics external script
4. Adding a media attribute with a value of 'print' to the print.css file
5. Removing the style rule related to portrait orientation from style.css and adding it to its own file, portrait.css, with a media attribute and value of 'orientation: portrait'
6. Minifying the style.css rules and then inlining them directly in index.html
7. Optimizing images using ImageOptim and adding a picture element with various image sizes/resolutions for the pizzeria image

As of writing this README, the page's score according to Google PageSpeed Insights is:

* Mobile: 94
* Desktop: 96

### Performance

views/pizza.html was optimized by:

* Reducing the time to resize pizzas using the pizza size slider (views/js/main.js)

  1. Removed the determineDX and sizeSwitcher functions. Added a switch statement instead to the changePizzaSizes function for determining the new width of the pizzas.

  2. Removed all document queries for .randomPizzaContainer from the for loop and instead created a variable, randomPizzas, containing a single query outside of the for loop. This variable is then used inside of the for loop.

* Reducing the time to generate random pizzas when the page loads (views/js/main.js)

  1. Moved pizzasDiv out of the for loop

  2. Decreased the number of pizzas that are created

* Improved page scrolling performance and frame-rate (views/js/main.js and views/css/style.css)

  1. Moved the scrollTop query and calculation out of the for loop in updatePositions

  2. Moved the items variable containing the .mover elements out of updatePositions and into the global scope. The variable is then assigned its value (the .mover elements) using getElementsByClassName instead of querySelectorAll. This assignment is made inside of the anonymous function assigned to the window.onload event (which has replaced the DOMContentLoaded listener).

  3. Moved the scroll listener to inside of the onload anonymous function to ensure that updatePositions does not try to access the items variable until it has been given a value.

  4. Decreased the number of moving pizzas that are created

  5. Added the will-change property to the .mover class in views/css/style.css to reduce the amount of painting that the browser has to do.
