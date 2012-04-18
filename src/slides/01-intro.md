# Geb

A better way to WebDriver

## What is Geb?

Geb is a developer focussed DSL for WebDriver.

It brings together the…

* Cross browser automation capabilities of *WebDriver*
* Elegance of *jQuery* content selection
* Expressiveness of the *Groovy* language
* Robustness of *Page Object* modelling

Does stuff for you that you're probably doing.

## About the Project

Free Open Source, Apache License, Version 2.0.

Currently at version **0.7.0**, preparing for **1.0.0** release.

* Home Page — [http://www.gebish.org](http://www.gebish.org)
* **The Book of Geb** — [http://www.gebish.org/manual/current](http://www.gebish.org/manual/current)
* Source Code — [https://github.com/geb/geb](https://github.com/geb/geb)
* User Mailing List — [http://xircles.codehaus.org/projects/geb/lists](http://xircles.codehaus.org/projects/geb/lists)
* In Maven Central — [http://mvnrepository.com/artifact/org.codehaus.geb](http://mvnrepository.com/artifact/org.codehaus.geb)

Built by [Gradle](http://www.gradle.org).

## Project Components

The heart is the **geb-core** component which is all you really need (plus WebDriver).

For testing, you probably also want one of these adapters as well:

* geb-spock
* geb-junit3
* geb-junit4
* geb-testng
* geb-easyb

Can be used with [Cucumber JVM](https://github.com/cucumber/cucumber-jvm) (no adapter needed).

There is also a [Grails](http://grails.org/) plugin.
