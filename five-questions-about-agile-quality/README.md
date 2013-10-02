# Five Questions about Agile Quality

- [ ] Finish [slides](five-questions-about-agile-quality.svg)
- [x] What is software quality?
- [x] What is agile software development?
- [x] Who is interested in quality?
- [x] Who is responsible for quality?
- [ ] How can we ensure quality in/by an agile process?


##1. What is (software) _quality_?

Well essentially software is a tool -- just like a hammer or a screw driver. It might be complex -- maybe more like a car or even a plane -- but it is still a tool.

So software quality should be pretty much the same as tool quality. If I think about a hammer I think the following quality features are most valuable to me:
- It does what it should -- in case of a hammer it should help me to get a nail into a wall. One could call this _usefulness_.
- It should not break -- when I hammer the nail the head of the hammer should stay fixed with the handle. This could be called _stability_.
- It does not confuse me -- a hammer needs a handle and a head, nothing more. I'd like to call that _usability_.
- It is fast -- it should not take to long to get the nail into the wall. So I care about the tools _performance_.
- It should look good -- its look should go well with my other tools. This might not be as important than the other things but I think _beauty_ is a feature.
- And of course it should have a good test coverage... wait, what? I don't care about test coverage, I simply _expect_ that all the other things were properly tested!

This list is not complete but I think it shows what we really should care about when we develop software. Test coverage is just a help for us to achieve _real value_ like stability. It is not what the user really wants.

##2. What is _agile_ software development?

In this talk I will mainly refer to Scrum and its vocabulary. However most (if not all) of the statements are valid for agile software development in general.

When we use Scrum to develop software there is a _Product Owner_ that will give user stories to the _Team_, that will develop the features described by the story and deliver it as shippable code. There is a Review in which the Product Owner (and maybe some Stakeholders) accepts of declines the delivered code.

An important assert in this process is that the _Product Owner_ can not check the software wholly -- so he/she needs to _trusts_ in the _Team_ to deliver _potentially shippable code_ which has no mayor quality issues.

##3. Who is interested in _quality_ in an _agile_ development process?

It is the Stakeholders that really care about quality. The users want to use a good software that makes their work easier, the customers want their workers to be more efficient etc. In Scrum there people are represented by the Product Owner so it is the Product Owner who should be interested for them (he/she is telling _User_ Stories).

Also the team has a certain interest to deliver quality work simply because producing good products feels better to them.

##4. Who is responsible for _quality_?

The Product Owner steers the quality of the resulting product by formulating User Stories that ensure that features are there (_usefulness_) and by insisting on certain acceptance criteria for those stories ensuring that the software is as fast as needed (_performance_...). In the Review the Product Owner and maybe some other present Stakeholders can see if the software in not confusing (_usability_) and that it leafs a good impression (_beauty_).

However this leafs some quality criteria for the _Team_ since it could hide _stability_ issues that just don't appear within the limited time span of a Review meeting. And of course the _Product Owner_ traditionally is a human and can therefore forget about asking certain demonstrations.

##5. How can we ensure _quality_ in/by an _agile_ process?

###What to test?

Well testing seams a good idea -- but what needs to be tested? In other words how do I test quality? Of course by testing everything that quality _is_ (see question 1).

###How/when to test?

Testing all the quality criteria of a software product that was developed in one sprint may be doable by hand of course... but in the next sprint the Team will change the product and that changes the software's behaviour... maybe even breaks a feature of the first sprint. So the needed test effort for _usefulness_ of a growing product rises with each developed feature.

At some point the consequently quality aware team will lower their velocity to almost 0 which will not be what the Product Owner wants.

The velocity aware team will keep their test effort at a certain limit that they can do without lowering their velocity... which will lead to unexpected bugs and to a reduced confidence about their own works quality. Statements like "come on, I can not test everything" or "it worked last time on my machine" are an indicators for such a situation.

Both are non existent extremes but somewhere between lies what I experienced in my carrier several times.

...TODO

###How to write tests that _embrace change_?

...TODO
