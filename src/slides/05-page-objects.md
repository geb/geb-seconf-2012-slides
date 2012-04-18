# Page Objects

DSL > @nnotations

## Page Objects

Must extend `geb.Page`

    import geb.Page
    
    class GoogleHomePage extends Page {
        static url = "http://google.com/"
        static at = { title == "Google" }
        static content = {
            searchField { $("input[name=q]") }
        }
    }

A DSL approach, opposed to annotation.

## Content DSL

Named content factories/templates.

    class GoogleResultsPage extends Page {
        static content = {
            results { $("li.g") }
            result { i -> results[i] }
            resultLink { i -> result(i).find("a.l", 0) }
            firstResultLink { resultLink(0) }
        }
    }

The content becomes methods and properties on the page.

    browser.at GoogleResultsPage
    browser.resultLink(3).text() == "Something…"

## Content is Required

    <p class="a">Some text!</p>

Geb will fail fast if content is not found.

    class SomePage extends Page {
        static content = {
            paragraphA { $("p.a") }
            paragraphB { $("p.b") }
            paragraphC(required: false) { $("p.c") }
        }
    }

Yields…

    paragraphA.text() == "Some text!"
    paragraphB // will throw geb.exception.RequiredPageContentNotPresent
    paragraphC.empty == true

## Content specifies navigation

Embed the structure of your application in the DSL.

    class FrontPage extends Page {
        static content = { helpLink(to: HelpPage) { $("a.help") } }
    }
    class HelpPage extends Page { 
        static content = { heading { $("h1") } }
    }

When the content is clicked, the browser's page is updated.

    browser.at FrontPage
    browser.helpLink.click()
    assert browser.heading.text() == "Help Page"

## Content can be waited on

Keep waiting out of your test code (i.e. the specification).

    class DynamicPage extends Page {
        static content = {
            errorMsg(wait: true) { $("p.errorMsg") }
        }
    }

Geb will wait an amount of time for the content to appear, retrying regularly.

Is configurable…

    takesLong(wait: 30) { … }
    verySlow(wait: "slow") { … }

Presets (i.e. `"slow"`) are specified by configuration mechanism.

## Content can be anything

Content doesn't have to be a `Navigator`.

    class DynamicPage extends Page {
        static content = {
            errorMsg(wait: true) { $("p.errorMsg").text() }
        }
    }

Can be any data type at all.

    assert browser.errorMsg == "Something bad happened!"
    