# Groovy

[http://groovy-lang.org](http://groovy-lang.org)

## Dynamic JVM Language

Groovy is…

* Compiled, never interpreted
* Dynamic, optionally typed
* 99% Java syntax compatible
* Concise, clear and pragmattic
* Great for DSLs
* A comfortable Java alternative for most

## The Type System

Groovy is a strong, optionally, typed language.

    def v = "a"
    v.toUpperCase() // java.lang.String method
    
    v = 1
    v.doubleValue() // java.lang.Integer method

Types are enforced at runtime.

    Integer i = "some string" // runtime error

## Dynamic

Method calls and property access are not bound at compile time.

    class UpCaser {
        def methodMissing(String name, args) {
            name.toUpperCase()
        }
    }

    def upCaser = new UpCaser()

    assert upCaser.abc() == "ABC"

Allows for dynamic behaviour and open classes.

Great for DSLs (redefine the concept of a method).

## Closures

Like function pointers, Ruby blocks etc.

    def doubler = { it * 2 }
    assert doubler(2) == 4

Used extensively in Geb. For example, when waiting…

    waitFor { heading == "Selenium Conf!" }

For DSLs…

    content = {
        heading { $("h1") }
        paragraphs { $("p") }
    }

## Compile Time Transforms

Implicitly turns certain statements into assertions. For example, when waiting:

    waitFor { title == "Page Title" }

Is transformed at compile time (kinda) into…

    waitFor { 
        assert title == "Page Title" 
        return title == "Page Title"
    }

(this feature allows Geb to provide helpful error messages on wait timeouts)

    title == "Page Title"
    |     |
    |     false
    Something else

## Clarity

Geb uses Groovy's dynamism to remove boilerplate.

    import geb.*

    Browser.drive {
        to GoogleHomePage

        searchTerm = "wikipedia"
        searchButton.click()

        at GoogleResultsPage
        assert firstResult.text() == "Wikipedia"

        firstResultLink.click()
        waitFor { at WikipediaPage }
    }
