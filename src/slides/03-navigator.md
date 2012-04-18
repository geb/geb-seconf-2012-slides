# The Navigator API

Do it like jQuery does it…

## The $() method

Returns a [Navigator](http://www.gebish.org/manual/current/api/geb-core/geb/navigator/Navigator.html) object.

General format:

    $(«css selector», «index/range», «attribute/text matchers»)

Examples:

    $("div") // all divs
    $("div", 0) // first div
    $("div", 0..2) // first three divs

    // The third section heading with text “Geb”
    $("h2", 2, id: "section", text: "Geb")

Built on top of `WebElement`.

## CSS Selectors

Full CSS3 if the target browser supports it.

    $("div.some-class p:first[title='something']")
    $("ul li a")
    $("table tr:nth-child(2n+1) td")
    $("div#content p:first-child::first-line")

Just delegates to WebDriver.

## Attribute/Text matching

Can match on attribute values:

    //<div foo="bar">
    $("div", foo: "bar")

The “text” attribute is special:

    //<div>foo</div>
    $("div", text: "foo")

Can use Regular Expressions:

    //<div>foo</div>
    $("div", text: ~/f.+/)

## Predicates

Geb supplies some handy predicates:

    // Partial searching
    $("p", text: startsWith("p"))
    
    // Case insensitivity
    $("p", class: iContains("section"))
    
    // Can use regular expressions
    $("p", id: endsWith(~/\d/))

There are [more of these](http://www.gebish.org/manual/current/navigator.html#attribute_and_text_matching).

## Relative Content

`$()` returns a [Navigator](http://www.gebish.org/manual/current/api/geb-core/geb/navigator/Navigator.html) that allows you to find relative content.

    $("p").previous()
    $("p").prevAll()
    $("p").next()
    $("p").nextAll()
    $("p").parent()
    $("p").siblings()
    $("div").children()

Most of these methods take selectors, indexes and attribute text/matchers too.

    $("p").nextAll(".listing")

## Additional methods

    $("a.help").click() // perform a click
    $("h1").text() // node text
    $("input[name=title]").value() // read value
    $("input[name=title]").value("Geb") // set value
    
Accessing the `WebElement` objects.

    WebElement firstParagraph = $("p").firstElement()
    WebElement lastParagraph = $("p").lastElement()
