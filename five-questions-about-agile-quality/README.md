# Five Questions about Agile Quality

This talk comes with [slides](five-questions-about-agile-quality.svg). Just download and open with your favourite web browser (Chrome runs them fastest).

## 1. What is (software) _quality_?

Well essentially software is a tool -- just like a hammer or a screw driver. It might be complex -- maybe more like a car or even a plane -- but it is still a tool.

So software quality should be pretty much the same as tool quality. If I think about a hammer I think the following quality features are most valuable to me:
- It does what it should -- in case of a hammer it should help me to get a nail into a wall. One could call this _usefulness_.
- It should not break -- when I hammer the nail the head of the hammer should stay fixed with the handle. This could be called _stability_.
- It does not confuse me -- a hammer needs a handle and a head, nothing more. I'd like to call that _usability_.
- It is fast -- it should not take too long to get the nail into the wall. So I care about the tool's _performance_.
- It should look good -- its look should go well with my other tools. This might not be as important than the other things but I think _beauty_ is a feature.
- And of course it should have a good test coverage... wait, what? I don't care about test coverage, I simply _expect_ that all the criteria I care about were properly tested!

This list is not complete but I think it shows what we really should care about when we develop software. Test coverage is just a help for us to achieve _real value_ like stability. It is not what the user really wants.

## 2. What is _agile_ software development?

In this talk I will mainly refer to Scrum and its vocabulary. However most (if not all) of the statements are valid for agile software development in general.

When we use Scrum to develop software there is a _Product Owner_ that will give user stories to the _Team_, that will develop the features described by the story and deliver it as shippable code. There is a Review meeting in which the Product Owner (and maybe some Stakeholders) accepts or declines the delivered code.

An important assert in this process is that the _Product Owner_ can not check the software wholly -- so he/she needs to _trust_ in the _Team_ to deliver _potentially shippable code_ which has no mayor quality issues.

## 3. Who is interested in _quality_ in an _agile_ development process?

It is the Stakeholders that really care about quality. The users want to use a good software that makes their work easier, the customers want their workers to be more efficient etc. In Scrum these Stakeholders are represented by the Product Owner so it is the Product Owner who should be interested for them (he/she is telling _User_ Stories).

Also the _Team_ has a certain interest to deliver quality work simply because producing good products feels better to them.

## 4. Who is responsible for _quality_?

The Product Owner steers the quality of the resulting product by formulating User Stories that ensure that features are implemented (_usefulness_) and by insisting on certain acceptance criteria for those stories ensuring that the software is as fast as needed (_performance_...). During the Review meeting the Product Owner and maybe some other present Stakeholders will notice if the software is easy to use or rather confusing (_usability_) and that it leaves a good impression (_beauty_).

However this leaves some quality criteria for the _Team_ since it could hide _stability_ issues that just don't appear within the limited time span of a Review meeting. And of course, the _Product Owner_ traditionally is a human and can therefore forget about asking certain demonstrations.

## 5. How can we ensure _quality_ in/by an _agile_ process?

### What to test?

Well testing seams a good idea -- but what needs to be tested? In other words how do I test quality? Of course by testing everything that quality _is_ (see [question 1](#1-what-is-software-quality)).

This does not require any unit tests but high level black box tests for the _whole_ software system (that's why I like to call these _system tests_) since such tests can prove that the quality criteria are met.
These tests may come in quite different flavours requiring very different approaches:
- feature tests for _usefulness_
- stress tests for _stability_
- user click tests for _usability_ and _beauty_
- performance tests for _performance_

However testing single classes in _class tests_ is useful (and usually needed) for the team to coordinate their work since they give feedback more rapidly and help to structure work using test driven development.

Also testing interfaces of complex components like deployment units _is_ valuable for the same reasons and since they help to keep these components reusable.

So there are three essential categories of tests:
1. (and most important) _system tests_
2. _class tests_
3. _component tests_

In my humble opinion writing any test that does not fit one of these categories is a waste of time and resources.

### When to test?

As described in [question 2](#2-what-is-agile-software-development) the _Team_ is responsible to deliver _shippable code_. To know that the code actually _is_ shippable it needs to be tested. So the time to test is at the very least and latest right before the Review.

### How to test?

Testing all the quality criteria of a software product that was developed in one sprint may be doable by hand of course, but in the next sprints the Team will change the product and that changes the software's behaviour -- maybe even breaks a feature of the previous sprint. So the needed test effort for _usefulness_ of a growing product rises with each developed feature.

At some point the consequently quality aware team will lower their velocity to almost 0 which will not be what the Product Owner wants.

The velocity aware team will keep their test effort at a certain limit that they can do without lowering their velocity... which will lead to unexpected bugs and to a reduced confidence about their own works quality. Statements like "come on, I cannot test everything" or "it worked last time on my machine" are an indicators for such a situation.

Both are non existent extremes but somewhere between lies the usual truth.

So the only way to deliver quality after each sprint is _test automation_. While we develop a new feature in the product we should write a software that ensures that this feature works just like the Product Owner wants it to work. That software will grow and change as the product grows and changes, so it needs to be just as maintainable as the product itself.

Having such a functional acceptance test suite running every commit, every night, at the weekend or at least at the end of the sprint enables us to change the whole implementation while we can ensure that the product still works as requested.

### How to write tests that _respond to change_?

The [Agile Manifesto](http://agilemanifesto.org/) values "responding to change over following a plan". In agile software development sometimes a whole User Story becomes unwanted _after_ it was developed and accepted by the Product Owner for whatever reasons. Also there might be little changes to the workflows of the product. For instance there might be an additional checkbox in the login form of a web application. This is not a complex change at all, but if our valued acceptance tests need to do a login before they can do anything, then we would need to change almost every test case.

#### Non-semantic test example
Let' say we get a story A:
> As customer
> I want the users to login to the application with user name and password before they can use any feature of the application
> to be able to track the user's activities.

And of course we created acceptance tests for that:
```groovy
class LoginSpec extends AcceptanceTest {
    def "it should be possible to login with valid user name and password"() {
        given:
        String validUserName = "someuser"
        String validPassword = "somepassword"

        when:
        browser.to(LoginPage)
        browser.page.userNameField = validUserName
        browser.page.passwordField = validPassword
        browser.page.loginButton.click()
        
        then:
        browser.isAt(WelcomePage)
    }

    def "it should not be possible to login with invalid user name and password"() {
        given:
        String invalidUserName = "wronguser"
        String invalidPassword = "wrongpassword"
        
        when:
        browser.to(LoginPage)
        browser.page.userNameField = invalidUserName
        browser.page.passwordField = invalidUserName
        browser.page.loginButton.click()

        then:
        !browser.isAt(WelcomePage)
    }
}
```

Some sprints later we get story B:
> As legal department
> I want the users to accept the user service agreement
> so we can not be hold responsible for illegal actions of the users.

This story changes the login process and therefore we need to change _every_ test that uses that process, which can be easily 90% of all tests. This makes rather small change an incredible amount of work to do.

#### Semantic test example

If our test would just have implemented what the Story said, it would not be so difficult to do. Here is the semantic test for story A:
```groovy
class LoginSpec extends AcceptanceTest {
    def "it should be possible to login with valid user name and password"() {
        given:
        UserActor user = new User(userName: "someuser", password: "somepassword")

        when:
        user.login()

        then:
        user.isLoggedIn()
    }

    def "it should not be possible to login with invalid user name and password"() {
        given:
        UserActor user = new User(userName: "wronguser", password: "wrongpassword")

        when:
        user.login()

        then:
        !user.isLoggedIn()
    }
}
```

The `UserActor` capsules all the details of the workflow, so there is just one place that needs to be changed:
```groovy
class UserActor {
    
    void login() {
        browser.to(LoginPage)
        browser.page.userNameField = invalidUserName
        browser.page.passwordField = invalidUserName
        browser.page.userServiceAgreementCheckbox.check // only change for Story B
        browser.page.loginButton.click()
    }
    
    boolean isLoggedIn() {
        return browser.isAt(WelcomePage)
    }
}
```

Semantic tests like that obviously are also way better readable. Variants of workflows can be implemented very easily, new Team mates can understand the code rather quick and testers can be taught to write automated test cases relying on their fellow developers to write powerful Test Actor classes.
Even sceptical Product Owners can be introduced to the code so they can check if the test actually tests what was requested.

