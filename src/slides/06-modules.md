# Modules

Reuse FTW.

## Modules

Modules are repeating and/or reappearing content.

    import geb.*

    class GoogleSearchModule extends Module {
        static content = {
            field { $("input", name: "q") }
            button(to: GoogleResultsPage) { btnG() }
        }

        void forTerm(term) {
            field.value term
            waitFor { button.displayed }
            button.click()
        }
    }

## Modules

Applied via the `module` keyword.

    class GoogleHomePage extends Page {
        static content = {
            search { module GoogleSearchModule }
        }
    }

    class GoogleResultsPage extends Page {
        static content = {
            search { module GoogleSearchModule }
        }
    }
    
    browser.search.forTerm("Selenium Conf")

## Modules

    <table>
      <thead>
        <tr>
          <th>Title</th><th>Author</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Zero History</td><td>William Gibson</td>
        </tr>
        <tr>
          <td>The Evolutionary Void</td><td>Peter F. Hamilton</td>
        </tr>
      </tbody>
    </table>

Modules can be used for repeating content.

## Modules

Modules have a *base*, from which all content lookups are relative.

    class BooksPage extends Page {
      static content = {
        bookResults { rowNum ->
          module BookRow, $("table tr", rowNum)
        }
      }
    }

    class BookRow extends Module {
      static content = {
        cell { colNum -> $("td", colNum) }
        title { cell(0).text() }
        author { cell(1).text() }
      }
    }

## Modules

We now have a reusable model for any row in our table.

    bookResults(0).title == "Zero History"
    bookResults(1).author == "Peter F. Hamilton

Great for for any reused/repeating content.
