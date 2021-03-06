# Geb @ Selenium Conf 2012

This repository contains the build for the slide deck used for this talk.

The slides are HTML and JavaScript. You can download a pre-built zip from [here](https://github.com/downloads/geb/geb-seconf-2012-slides/geb-seconf-20120-slides.zip).

## How to build the slides

To build the slides locally, simply check this repository out and run…

    ./gradlew slideshow

Then open `build/slideshow/index.html` in your browser.

## How to use the slides

Once you've opened the `index.html` file in your browser, simply use the → and ← keys to navigate through the slides.

## About the tooling

The tooling used to build the slides is something I put together and is an experiment. It uses:

* [deck.js](http://imakewebthings.com/deck.js/ "deck.js &raquo; Modern HTML Presentations")
* [LessCSS](http://lesscss.org/ "LESS &laquo; The Dynamic Stylesheet language")
* [jHighlight](http://www.ohloh.net/p/jhighlight "jhighlight")
* [PegDown](https://github.com/sirthias/pegdown "sirthias/pegdown · GitHub")
* [JSoup](http://jsoup.org/ "jsoup Java HTML Parser, with best of DOM, CSS, and jquery")

[Gradle](http://www.gradle.org/ "Gradle - Build Automation Evolved") is used to build the final HTML from [Markdown](http://daringfireball.net/projects/markdown/ "Daring Fireball: Markdown") and JavaScript input.

This will eventually be packaged up into a more user friendly, standalone, toolchain.