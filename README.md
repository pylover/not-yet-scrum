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

### Tools

| Problem | Solution | Why |
|---|---|---|
| Version Control | GIT | Kidding Me? |
| Remote repository | Github | Simple, Free private repos, Powerful CI/CD, Issue tracking |
| Issue tracking & Canban | Github | Simplicity & Integrity |
| Main Language(s) | Python, C, GoLang and any portable language | these covers all we need as portable languages. |
| IDE | Vim | Productivity |
| Platform | Any Posix | Portability |

### Naming

I folow the [Nomanclature](https://en.wikipedia.org/wiki/Nomenclature) for the 
naming purpose.

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
