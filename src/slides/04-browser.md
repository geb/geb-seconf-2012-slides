# geb.Browser

The API entry point.

## Browser

Wraps a `WebDriver`…

    import geb.Browser
    
    def browser = new Browser(new FirefoxDriver())
    browser.driver instanceof WebDriver
    
    browser.go "http://www.seleniumconf.org/"

And a _page_…

    browser.page instanceof geb.Page // default page
    browser.to myorg.SomePage
    browser.page instanceof myorg.SomePage

## Dynamically forwards to page

Any method calls/properties not handle by `browser` are forwarded to `page`.

    class SomePage extends geb.Page {
        def pageMethod() {}
    }
    
    browser.to SomePage
    
    // Following two lines equivalent
    browser.page.pageMethod()
    browser.pageMethod()

Cuts out noise.

## Hidden in test adapters

Test adapters forward all method calls etc. to underlying `Browser`.

    import geb.junit4.GebTest
    import org.junit.Test
    
    class SomeTest extends GebTest {
        @Test
        void testStuff() {
            to SomePage
            pageMethod()
        }
    }

## Specifications without REs

    import geb.junit4.GebTest
    import org.junit.Test

    class GoogleTest extends GebTest {
        @Test 
        void theFirstLinkShouldBeWikipedia() {
            to GoogleHomePage

            searchTerm = "wikipedia"
            
            at GoogleResultsPage
            assert firstResult.text() == "Wikipedia"

            firstResult.click()
            
            waitFor { at WikipediaPage }
        }
    }
