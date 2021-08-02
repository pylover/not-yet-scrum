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


#### BDD Test case example

```python
    with oauth_mockup_server(),  self.given(
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
            'The organization title is exist',
            form=dict(title='organization-title')
        )
        assert status == '600 Repetitive Title'

        when(
            'The title format is invalid',
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
| Platform | Any Posix | Portability |


### Naming

I folow the [Nomanclature](https://en.wikipedia.org/wiki/Nomenclature) for the 
naming purpose.


### Code coverage

Code coverage is most important factor. the first commit comes with `100%`
code coverage and should not descerased even `.0000001%` with any commit and 
or pull request.


### BDD

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

Check [here](https://martinfowler.com/bliki/GivenWhenThen.html) for more info.


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
        |                               |~~~Story(Moon landin)~~~>|                            |            |                    |     
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
  pm -> tc: Story(Moon landin) -> Release
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
