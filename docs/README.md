# Welcome to the e-mission documentation!

[![Documentation Status](https://readthedocs.org/projects/e-mission/badge/?version=latest)](https://e-mission.readthedocs.io/en/latest/?badge=latest)

This repo contains all the documentation for the e-mission project, and [almost ALL THE ISSUES](https://github.com/e-mission/e-mission-docs/issues/). The rationale behind the change can be found in the [migration reasons](contribute_to_the_doc/migration_reason.md).

There are some specialized READMEs [in the individual repositories](https://github.com/e-mission), but they are gradually being moved in here. This means that if you have any questions, you should first search here and if you don't find any [existing issues](https://github.com/e-mission/e-mission-docs/issues/), you should [file an issue here](https://github.com/e-mission/e-missiond-docs/issue).

### Thanks to [@PatGendre](https://github.com/PatGendre) from [FabMob](https://github.com/fabmob/), you can now [ReadTheDocs](https://e-mission.readthedocs.io/en/latest/)



### [e-mission website](https://e-mission.eecs.berkeley.edu/) | [CODE on GitHub](https://github.com/e-mission) | [LICENCE BSD-3](https://github.com/e-mission/e-mission-docs/blob/master/docs/LICENSE.md) 



## What is e-mission?

E-mission is an open source mobility platform developed at the [RISE](http://rise.cs.berkeley.edu/) and [BETS](https://bets.cs.berkeley.edu/) labs in the UC Berkeley EECS Department. 

E-mission includes a mobile application for Android and iOS, which with user consent, automatically collects the user's travel patterns and sends them to the server to derive personal mobility information and analyses. Depending on the user's consent for sharing his/her data, this data can also be used for aggregate mobility data studies. The application is also a tool for collecting information filled-in by the user (such as trip incidents, ground truth information about his/her trip purpose and transportation mode, or answers to questions asked in external surveys).  

The server is a python web application, the data is stored in a mongoDB database;  the client is a Cordova application for both Android and iOS.

The application has been initially designed to be used in research and academic projects either for conducting travel surveys and as a good learning project for CS students. It is also freely reusable for [any other use-cases](https://github.com/e-mission/e-mission-docs/blob/master/docs/use/deployments.md).

If you are using e-mission in your work, please submit a PR or send shankari@eecs.berkeley.edu an email so that you can be added to this list.

## Overview
Read these papers for understand context.

- [TRB paper describing how to use e-mission functionality](https://people.eecs.berkeley.edu/~shankari/emission_trb_2017_paper.pdf)  
- [The in-review paper on the e-mission architecture, please do not distribute](https://people.eecs.berkeley.edu/~shankari/em-arch.pdf)  

## Roadmap
- The next features and enhancement can be guessed from the [ISSUES](https://github.com/e-mission/e-mission-docs/issues)  
- We have formed a project commmittee and are discussing options for [joining an open source foundation for long-term IP and financial support](dev/future/foundations.md)
- The current large scale research features are described in [Develop/Future](dev/future/overview.md)   
