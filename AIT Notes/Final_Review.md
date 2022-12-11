



## Agenda

* Format
* topicss
* how to prep
* quick high level view of what we've learned
* question from u



## Format

* same as midterm exam
* 1 - 3 written questions
* Multiple Choice, Multiple Selection, Fill in Blanks, Matching, ord
* logistics
    * during class time on Tuesday
    * show up to zoom session
        * instructions
        * ask questions
    * less than class time (first few min will be instructions)
    * accommodations - lmk if post exam doesn't work



## Topics

* Sort of cumulative - I won't ask specific questions that target only first semester material. 

* Everything from midterm forward

1. continue with mongoose
2. authentication
3. client side js
    * manipulating the DOM
4. AJAX
    * xhr / fetch
    * SOP, CORS
5. websockets via socket.io
6. react

Not included for this section

* routing 
* next

Not on the exam:

* passport
* webpack intergration with express
* flexbox
* socket.io rooms
* no class based functional component



## Preparation

1. Look at HW + in class activities if u found written questions challenging

    * In class activities: 
        * AJAX
        * React
        * Socket.io

    * def ask for partial implementation
    * just have express running
    * fresh create react app
    * mongodb

2. MC / MS

    * slides + lectures
    * if u did hw, and it worked, but u don't understand why
        * look at associated slides
        * ask during review, ed, OHs, tutoring
    * watch the time, ROI..... don't spend too much time, go back and check rather than spend even more time

3. matching

    * read code from slides
    * read code from uploaded examples
    * up reading comprehension skills





## Routings

### Server side routing

* path ---> some action
    * /foo
    * regex, url param, query string
* browser:
    * it shows the correct url
    * back / forward
* maybe middleware

### possible on client

* event handlers

    * clicking on link will 
        * hide / show dom elements
        * add / remove dom elements
        * where elements represent a page

* inspect the url

    * window.location
    * new URL()..... domain and pathname
    * show dom element appropriately

* capture all anchor, submit... prevent default

* forward and back, showing the right url

    * history.push

    * popstate ... event triggered by forward and back buttons

* tl;dr ... non trivial



Use a library ... React Router