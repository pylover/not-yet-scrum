---
“Everything should be made as simple as possible, but no simpler.” 

This is one of the great quotes in science. Coming from Einstein, who 
simplified physics into general relativity, it is a great statement of how to 
conduct science.

---
# Not Yet Scrum

I named it `not-yet-scrum` because I think the Scrum methodology is too much 
for developing software projects (even large scale projects).

We won't focus on gathering comprehensive documents (as Agile says). Instead, 
the only information developer needs to implement a feature is a small bit of 
product specification which describes the whole definition of the feature 
(aka User Story). It helps us keep documents fresh and update them frequently 
as needed without worrying about outdating them.

Here I mentioned some tools and technologies because I believe the
`tools-matter` rule and choosing them based on simplicity and productivity 
will result in positive effects on the progress.


## Limitations

### Text Only

Any format other than text is not accepted for information at all.

Example list of not acceptable formats:

- Images 
- Formatted text documents such as `MSWord`, `Excel`, `Google-doc`, 
    `LibreOffice Writer` etc ...
- PDF


Example list of acceptable formats:

- reStructuredText
- Markdown
- Plain text

### Nugget

`Nugget` is what we deliver to developers to describe them what to do.

A `Nugget` May consist of:

- User Story
- BDD specification
- TDD definition which describes the exact input and output of the feature 
    and or API.
- Wireframe
- GUI prototype
- One or more test case(s)

---
**NOTE**

There is no other information allowed to deliver to developers other than the 
list above.

---

#### Nugget Examples

[here](https://github.com/Carrene/dolphin/issues/263) is an example of
`Nugget`.


#### BDD

All tests should meet the `BDD` standards:

```bdd
Feature: User trades stocks
  Scenario: User requests a sell before close of trading
    Given I have 100 shares of MSFT stock
       And I have 150 shares of APPL stock
       And the time is before close of trading

    When I ask to sell 20 shares of MSFT stock
     
     Then I should have 80 shares of MSFT stock
      And I should have 150 shares of APPL stock
      And a sell order for 20 shares of MSFT stock should have been executed
```

Check [here](https://martinfowler.com/bliki/GivenWhenThen.html) for more info
about the BDD scenario.

This an example of how I save the BDD skeleton in test files to increase 
readability using the [bddrest](https://github.com/pylover/bddrest).

```python
with Given(
        'Creating an organization.',
        '/apiv1/organizations',
        'CREATE',
        form=dict(title=title)
    ):
    assert status == 200
    assert response.json['title'] == title
    assert response.json['logo'] is None
    assert response.json['url'] is None
    assert response.json['domain'] is None
    assert response.json['createdAt'] is not None
    assert response.json['modifiedAt'] is None

    when(
        'Organization is already exist',
        form=dict(title='organization-title')
    )
    assert status == '600 Repetitive Title'

    when(
        'Title is invalid',
        form=dict(title='my organ')
    )
    assert status == '747 Invalid Title Format'
```

### Tools

| Problem | Solution | Why |
|---|---|---|
| Version Control | GIT | Kidding Me? |
| Remote repository | Github | Simple, Free private repos, Powerful CI/CD, Issue tracking |
| Issue tracking & Kanban | Github | Simplicity & Integrity |
| Main Language(s) | Python, C, GoLang and any portable language | Ease of develop and useful tools for BDD |
| IDE | Vim | Productivity |
| Platform | Any POSIX | Portability |


### Naming

I folow the [Nomanclature](https://en.wikipedia.org/wiki/Nomenclature) for the 
naming purpose.


### Code coverage

Code coverage is most important factor. the first commit comes with `100%`
code coverage and should not descerased even `.0000001%` with any commit and 
or pull request.


## Workflow


```
DIAGRAM: Nugget flow                                                                                                                   
author: Vahid Mardani                                                                                                                        
version: 1.0                                                                                                                           
                                                                                                                                       
+---------------+              +-----------------+       +-----------------+              +---------+ +-----------+         +---------+
| Product Owner |              | Product Manager |       | Technical Chef  |              | UX & UI | | Developer |         | QA & QC |
+---------------+              +-----------------+       +-----------------+              +---------+ +-----------+         +---------+
        |                               |                         |                            |            |                    |     
        |~~~Epic(Travel to the Moon)~~~>|                         |                            |            |                    |     
        |                               |~~~Story(Moon landing)~~>|                            |            |                    |     
        |                               |                         |                            |            |                    |     
        |                               |                ********************************************       |                    |     
        |                               |                * if Design needed?                        *       |                    |     
        |                               |                ********************************************       |                    |     
        |                               |                         |                            |            |                    |     
        |                               |                         |~~~Desing(Nugget)~~~~~~~~~~>|            |                    |     
        |                               |                         |                            |            |                    |     
        |                               |                         |<--Wireframe & Prototype----|            |                    |     
        |                               |                         |                            |            |                    |     
        |                               |                ********************************************       |                    |     
        |                               |                * end if                                   *       |                    |     
        |                               |                ********************************************       |                    |     
        |                               |                         |                            |            |                    |     
        |                               |                ----------------------------------------------------------              |     
        |                               |                | Note:                                                  |              |     
        |                               |                |                                                        |              |     
        |                               |                | The Nugget may be split into two or more Nuggets.      |              |     
        |                               |                ----------------------------------------------------------              |     
        |                               |                         |                            |            |                    |     
        |                               |                         |~~~Nugget~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~>|                    |     
        |                               |                         |                            |            |~~~Test(Feature)~~~>|     
        |                               |                         |                            |            |                    |     
        |                               |                         |                            |      *********************************
        |                               |                         |                            |      * while Need more work?         *
        |                               |                         |                            |      *********************************
        |                               |                         |                            |            |                    |     
        |                               |                         |                            |            |<~~Feedback~~~~~~~~~|     
        |                               |                         |                            |            |                    |     
        |                               |                         |                            |            |------------------->|     
        |                               |                         |                            |            |                    |     
        |                               |                         |                            |      *********************************
        |                               |                         |                            |      * end while                     *
        |                               |                         |                            |      *********************************
        |                               |                         |                            |            |                    |     
        |                               |                         |                            |            |<--Confirm----------|     
        |                               |                         |<--Pull Request--------------------------|                    |     
        |                               |<--Release---------------|                            |            |                    |     
        |<--Working feature-------------|                         |                            |            |                    |     
        |                               |                         |                            |            |                    |     
+---------------+              +-----------------+       +-----------------+              +---------+ +-----------+         +---------+
| Product Owner |              | Product Manager |       | Technical Chef  |              | UX & UI | | Developer |         | QA & QC |
+---------------+              +-----------------+       +-----------------+              +---------+ +-----------+         +---------+
                                                                                                                                       
```

The above diagram is generated by [adia](https://github.com/pylover/adia) from 
this source file which is a good example of how I deal with diagrams.

```adia
diagram: Nugget flow
version: 1.0
author: Vahid Mardani

sequence: 

po.title: Product Owner
pm.title: Product Manager
dev.title: Developer
tc.title: Technical Chef
qa.title: QA & QC
uix.title: UX & UI

po -> pm: Epic(Travel to the Moon) -> Working feature
  pm -> tc: Story(Moon landing) -> Release
    if: Design needed?
      tc -> uix: Desing(Nugget) -> Wireframe & Prototype
    @tc ~ dev: |
      Note: 
      
      The Nugget may be split into two or more Nuggets.
      
    tc -> dev: Nugget -> Pull Request
      dev -> qa: Test(Feature) -> Confirm
        while: Need more work?
          qa -> dev: Feedback
    
```


## Some good tips to decide what to do

### The Zen of Python, by Tim Peters

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Complex is better than complicated.
- Flat is better than nested.
- Sparse is better than dense.
- Readability counts.
- Special cases aren't special enough to break the rules.
- Although practicality beats purity.
- Errors should never pass silently.
- Unless explicitly silenced.
- In the face of ambiguity, refuse the temptation to guess.
- There should be one-- and preferably only one --obvious way to do it.
- Although that way may not be obvious at first unless you're Dutch.
- Now is better than never.
- Although never is often better than *right* now.
- If the implementation is hard to explain, it's a bad idea.
- If the implementation is easy to explain, it may be a good idea.
- Namespaces are one honking great idea -- let's do more of those!


### SOLID Principle

*from [Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/SOLID)*


In software engineering, SOLID is a mnemonic acronym for five design 
principles intended to make software designs more understandable, flexible, 
and maintainable. The principles are a subset of many principles promoted by 
American software engineer and instructor Robert C. Martin, first introduced 
in his 2000 paper Design Principles and Design Patterns.

The SOLID acronym was introduced later, around 2004, by Michael Feathers.

#### The SOLID concepts are:

##### Single-responsibility principle: 

`There should never be more than one reason for a class to change.` 

In other words, every class should have only one responsibility.


##### Open–closed principle: 

`Software entities ... should be open for extension, but closed for modification.`

##### Liskov substitution principle: 

`Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.` 

See also design by contract.

##### Interface segregation principle: 

`Many client-specific interfaces are better than one general-purpose interface.`


##### Dependency inversion principle: 

`Depend upon abstractions, [not] concretions.`


#### Conclusion

Although the SOLID principles apply to any object-oriented design, they can 
also form a core philosophy for methodologies such as agile development or 
adaptive software development.

