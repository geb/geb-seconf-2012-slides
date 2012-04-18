# Spock

Groovy (JUnit based) Testing Framework

## Executable Specifications

    class LoginSpec extends geb.spock.GebReportingSpec {
        def "redisplay form with error message with bad password"() {
            given:
            to LoginPage

            when:
            username = "user1@example.com"
            password = "badpassword"
            submitButton.click()

            then:
            at LoginPage
            invalidUsernameOrPasswordError.present
        }
    }

See [http://spockframework.org](http://spockframework.org) for more on Spock.
    