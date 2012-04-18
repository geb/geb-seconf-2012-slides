# Feature Tour!

More info @ http://gebish.org/manual/current

## Screenshots and HTML reports

Geb's test adapters automatically do this after each test method.

File system location is determined by class name and test name.

    target/test-reports/myorg/tests/SomeTest/
                    001-001-I test some stuff-end.html
                    001-001-I test some stuff-end.png
                    002-001-I test some more stuff-end.html
                    002-001-I test some more stuff-end.png

Manual grabs can be made any time…

    browser.to SomePage
    browser.report "at SomePage" // report label

    target/test-reports/myorg/tests/SomeTest/
                    001-002-I test some stuff-at SomePage.html

## Driver Management

Geb caches the `WebDriver` instance (per thread) and shares it across test cases.

Manages clearing cookies and is configurable.

This can be disabled and tuned.

## Configuration Management

Looks for `GebConfig` class or `GebConfig.groovy` file on classpath.

    driver = { 
        new FirefoxDriver()
    }

    waiting {
        timeout = 2
        slow { timeout = 100 }
    }

    reportsDir = "geb-reports"

    environments {
        chrome { driver = "chrome" }
    }

`mvn test -Dgeb.env=chrome`

## At Checking

The “at checking” mechanism enables fail fast and less debugging.

    class LoginPage extends Page {
        static at = { $("h1").text() == "Please log in" }
    }

    browser.at LoginPage

Will throw an exception if every statement of the at check is not true.

## Adhoc waiting

The `waitFor` method can be used anywhere to wait for any condition to be true.

Groovy's flexible notion of “truth” makes this powerful.

    waitFor { $("p.errorMsg") }.text() == "Error!"
    waitFor { $("p.errorMsg").text() } == "Error!"

Waiting options are configurable…

    waitFor(timeout: 10, retry: 0.1) { … }
    waitFor("fast") { … }

Defaults and named presets controlled by configuration.

## Implicit (power) Assertions

Implicitly turns certain statements into assertions. For example, when waiting:

    waitFor { title == "Page Title" }
    waitFor { assert title == "Page Title" } // equivalent (sorta)

Gives informative error message…

    geb.waiting.WaitTimeoutException: condition did not pass in 5.0 seconds (failed with exception)
        …
    Caused by: Assertion failed:

    title == "Page Title"
    |     |
    |     false
    Something else

## Implicit (power) Assertions

Applies to waiting content…

    class DynamicPage extends Page {
        static content = {
            errorMsg(wait: true) { $("p.errorMsg") }
        }
    }

And page “at checks”

    class GoogleHomePage extends Page {
        static at = { title == "Google" }
    }

## Direct Downloading

Examine binary resources easily, with the session state.

    Browser.drive {
        go "http://myapp.com/login"

        // login
        username = "me"
        password = "secret"
        login().click()
        def downloadLink = $("a.pdf-download-link")

        // now get the pdf bytes (that requires authentication)
        def bytes = downloadBytes(downloadLink.@href)
    }

Also `downloadStream()` and `downloadText()`.

## Interaction DSL (Actions)

DSL for building actions…

    class SomeClass extends Page {
        static content = {
            someContent { $("div.someContent") }
        }
    }
    
    interact {
        clickAndHold someContent
        moveByOffset 15, 15
        release()
    }

Builds on top of WebDriver's `Actions` support.

## Form Shortcuts

Geb makes it easy to deal with all form controls. Read and write `input`s like properties.

Finds first `input`|`select`|`textarea` with the given name.

    // Sets the value of the first “control”
    // named “firstName” and sets its value
    browser.firstName = "Luke"
    
    // read the value
    assert browser.firstName == "Luke"

Unified API for all element types.

## JavaScript Interface

    <script>
        var globalVar;
        function globalFunction(arg1) {
            …
        }
    </script>

Can access global JS variables and functions with Groovy code…

    browser.js.globalVar = 1
    assert browser.js.globalVar = 1
    
    browser.js.globalFunction("the arg")

## jQuery Adapter

Geb makes it easy to get a jQuery object for content.

    $("input").jquery.keydown()

Useful for simulating interactions that are difficult/unreliable with the WebDriver API.

The `jquery` property is a proxy for an equivalent jQuery object in the JS runtime.

**Not to be abused!**

## Frame / Window Support

Jumping to frames temporarily…

    withFrame($('#footer')) { assert $('span') == 'frame text' }

Focussing on an open window…

    withWindow({ title == "Another Window" }) {
        // do some stuff with the window
    }
    // back to the previous window

Managing opening new windows…

    withNewWindow({ $('a').click() }) {
        // do some stuff with the new window
    }
    // back to the previous window
