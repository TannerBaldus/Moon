---
layout: post
title:  "Course Shopper"
date:   2016-05-02
excerpt: "Scraping my school's terrible classes page."
project: true
tag:
- python
- django
- web scraping
- selenium
comments: true
---

![](https://cloud.githubusercontent.com/assets/4913202/18624181/544dbd36-7dfa-11e6-9275-09ff8af0470f.jpg)

Course shopper was a project I tinkered with while in school. The idea was to scrape the classes from my school's awful courses website:
[classes.uoregon.edu](http://classes.uoregon.edu) and little known course evaluations reports
behind our student logins on duckweb.uoregon.edu to make a better course searching experience.
Never got around to the front end and api but did do the scraper.

Each part of the scraper would be ran with Django custom commands which
used the settings file to determine which function to use to update the course
[offerings](https://github.com/TannerBaldus/course_shopper/blob/master/better_courses/=
course_search/management/commands/update_offerings.py) and
[evals](https://github.com/TannerBaldus/course_shopper/blob/master/better_courses/=
course_search/management/commands/update_evals.py).
The idea being if someone from another school wanted to do the same thing
all they'd have to do is write a parser and plug in their functions in the
settings.

For the class info:
For each  subject code and term I  loaded the corresponding url for all the
classes of that subject in that term, [example page](http://classes.uoregon.edu/pls/prod/hwskdhnt.P_ListCrse?term_in=3D201601&s=
el_subj=3Ddummy&sel_day=3Ddummy&sel_schd=3Ddummy&sel_insm=3Ddummy&sel_camp=
=3Ddummy&sel_levl=3Ddummy&sel_sess=3Ddummy&sel_instr=3Ddummy&sel_ptrm=3Ddum=
my&sel_attr=3Ddummy&sel_cred=3Ddummy&sel_tuition=3Ddummy&sel_open=3Ddummy&s=
el_weekend=3Ddummy&sel_title=3D&sel_to_cred=3D&sel_from_cred=3D&sel_subj=3D=
CIS&sel_crse=3D&sel_crn=3D&sel_camp=3D%25&sel_levl=3D%25&sel_attr=3D%25&beg=
in_hh=3D0&begin_mi=3D0&begin_ap=3Da&end_hh=3D0&end_mi=3D0&end_ap=3Da&submit=
_btn=3DShow+Classes)
and parsed those search results [(code)](https://github.com/TannerBaldus/course_shopper/blob/master/better_courses/=
course_search/parsers/uoregon/search_page_parser.py)
and for each search result parses the details [(code)](https://github.com/TannerBaldus/course_shopper/blob/master/better_courses/=
course_search/parsers/uoregon/offering_page_parser.py).

For the evals:
The eval reports were behind a login on duckweb.uoregon.edu  (which I no
longer have credentials for so no example pages) and in a jframe so I
ended up extending the selenium web driver with some convenience functions
[(code)](https://github.com/TannerBaldus/course_shopper/tree/master/better_courses/=
course_search/logged_in_sessions) and using that to mimic a user to scrape the evals [(code)](https://github.com/TannerBaldus/course_shopper/blob/master/better_courses/=
course_search/parsers/uoregon/evals_parser.py)
