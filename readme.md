# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Web Services, APIs & Python Fundamentals


### LEARNING OBJECTIVES
*After this lesson, you will be able to:*
- Identify all the HTTP Verbs & their uses.
- Describe APIs and how to make calls and consume API data.
- Access public APIs and get information back.
- Read and write data in JSON format
- Understand Python Fundamentals



## Opening (5 mins)

In this lesson we will be diving into the world of API's, but more specifically we will be taking a tour of one of the most accessible sources of data on the internet.



## First, What is an API?

API stands for "Application Program Interface", and technically applies to all of software design. However, since the explosion of information technology, the term now commonly refers to web URLs that can be accessed for raw data.

APIs publish data for public use. As third-party software developers, we can access an organization's API and use their data within our own applications.

### Famous APIs:  Facebook

Facebook provides an API for interacting with their service.  At a glance:

- View your posts
- View websites, people, posts, pages that you've liked
- View activity on apps from you and your friends
  - Movies watched
  - Music listened
  - Games played
- View places traveled / check-ins
- Relationships


### Famous APIs:  Yelp

Yelp provides a way for developers to access:

- Reviews
 - Services
 - Restaraunts / Bars / Cafes
 - Businesses
- Business meta-data

### Famouse APIs:  Echonest

Echonest consolidates access to many entertainment service APIs in one place.  It has a huge list of features and connected services including:

- Spotify
- Pandora
- Rdio
- Gracenote
- SoundHound
- Shazam

Some Echonest features include:

- Music waveform identification (like Shazam, Soundhound music ID)
- Playlist recommendations
- Detailed artist, album, and track lookup
 - Bio / Origins / Contemporaries / Noteworthy Accomplishments
 - Official twitter / website / social media links
 - BPM / Mood / Popularity / Genre(s)
 - Images / Videos / Media
- Detailed movie, actor, product lookup
- Concert Schedules and ticket metadata


## Web APIs

The prevalance of web APIs have increased 10x with the rise of Javascript and advent of web programming techniques allowing the communication of small pieces of data, without having to refresh the entire page.

With the growth of highly interactive websites, provided by AJAX programming techniques in Javascript, many languages started co-opting standards to communicate data to and from web servers mainly for two reasons:
- Ease of integration
- Consistent standards

## You Do: Research APIs (15 minutes)
1. Search for an API that interests you
2. Read through the documentation to see what data is available to you
3. Jot down three project ideas you'd be interested in pursuing using this API

<a name="introduction"></a>
## Introduction

In order to talk about APIs, we need first to introduce the _separation of concerns_. In computer science, _separation of concerns_ (SoC) is a design principle for separating a computer program into distinct sections, such that each section addresses a separate concern. A concern is a set of informations that affects the code of a computer program. In particular, when building a web application, it's best practice to separate the website logic from data models. This not only allows for cleaner code, but is an easier way to manipulate our layouts and interactions. Separation of concerns becomes ever more important when working with outside data.

API calls are really a fancy term for making _HTTP requests_ to a server and sending/receiving structured data from that endpoint. We are still communicating with URLs, however instead of receiving markup, like we do with HTML pages, we receive data.

[Representational state transfer (REST)](http://stackoverflow.com/questions/551933/can-you-explain-the-web-concept-of-restful) is the most common architecture style for passing information to and from these API endpoints.

Before we start consuming these services however, it's important to understand the fundamentals of the underlying communication layer: HTTP.


### HTTP: Recap

HTTP is a protocol - a system of rules - that determines how web pages (see:'hypertext') get sent (see:'transferred') from one place to another. Among other things, it defines the format of the messages passed between HTTP clients and HTTP servers.

![Web Architecture](./assets/images/webserver_to_rails_setup.jpeg "Web Architecture")

Since the web is a service, it works through a combination of clients which _make_ requests and servers (which _receive_ requests).

#### HTTP Client

HTTP Clients make or generate HTTP Requests. Some types of clients are:

* Browsers - Chrome, Firefox and Safari.
* Command Line programs - [curl](http://curl.haxx.se/docs/) and [wget](http://www.gnu.org/software/wget/manual/wget.html).

HTTP Clients respond to HTTP Responses from a Web Server. They process the data being returned form a Web Server, aka HTTP Server.

#### HTTP/Web Server

All _Web Servers_ receive _HTTP Requests_ and generate _HTTP Responses_. Often Web Servers are just the middleman, passing HTTP Request and Responses between the client and web application. Two of the most popular _HTTP or Web servers_ are [Apache](http://httpd.apache.org/) and [Nginx](http://nginx.com/), But there are lots different [web servers](http://en.wikipedia.org/wiki/Comparison_of_web_server_software) out there.


### Web Applications

Web Applications are programs that run on a web server, process the HTTP requests that the server receives, and generate HTTP Responses.

![HTTP Request and Response](./assets/images/http_req_resp.gif)

Lost? Here's the play-by-play.

1. A client sends a HTTP Request to a HTTP Server running on a remote machine.  
  * The _hostname_ given in the URL, indicates which server will receive the request.  
2. The HTTP server processes the HTTP Request. This may entail passing the request to some Web Application, which creates a HTTP Response.
3. The response gets sent back to the client.
4. The client processes the response.

How does the server know what the request is asking for? This is specified by the URL, a special kind of path that specifies where a resource can be found on the web.

![URL](./assets/images/http1-url-structure.png)

**Check:** can anyone explain what a client and a server are?

<a name="demo"></a>
## Demo: HTTP (15 min)

Lets explore HTTP resources. We'll start by looking at HTTP requests and responses using the Chrome Inspector.

![HTTP Request and Response](./assets/images/http_request_response.jpeg "HTTP Request and Response")

* In Chrome, open up Chrome Inspector (*command + option + 'i', or ctrl + click and select 'inspect element'*).
* Select the Network tab. It should look something like this:

![Chrome Inspector](./assets/images/chrome_inspector.png)

* Next, go to the URL https://generalassemb.ly/

  You should be able to see a few HTTP Requests and Responses in the Network tab; for each request you'll see a **Path**, **Method**, **Status**, **Type**, and **Size**, along with info about how long it took to get each of these resources.
  *Most of this information comes from the HTTP Request and Response.*

  * Some HTTP requests are for CSS, JavaScript and images that are referenced by the HTML.
  * Select `generalassemb.ly` in the Path column on the far left.
  * Select the Headers tab. **Headers** are meta-data properties of an HTTP request or response, separate from the body of the message.

### HTTP Request

The first word in the request line, _GET_, is the **HTTP Request's Method**.

![HTTP Request](./assets/images/http_request.jpeg "HTTP Request")

**HTTP Request Methods:**   

* **GET** => Retrieve a resource.  
* **POST** => Create a resource.  
* **PATCH** (_or **PUT**, but **PATCH** is recommended_) => Update an existing resource.  
* **DELETE** => Delete a resource.  
* **HEAD** => Retrieve the headers for a resource.

Of these, **GET** and **POST** are the most widely used.

**HTTP Request Structure:**

```
[http request method] [URL] [http version]  
[list of headers]

[request body]
```

*Notice, that the Request Header is separated from the Request Body by a new line.*


**HTTP Request Method Example: (No Body)**

    GET http://vermonster.com HTTP/1.1  
    Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8  
    Accept-Encoding:gzip,deflate,sdch
    Accept-Language:en-US,en;q=0.8  
    Connection:keep-alive  
    Host:vermonster.com  
    User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_5)  
    AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1659.2 Safari/537.36  

### HTTP Response

![HTTP Response](./assets/images/http_response.jpeg "HTTP Response")

When a client sends a request, the server sends back a response; the standard format for this response is:

```
[http version] [status] [reason]  
[list of headers]

[response body] # typically HTML, JSON, ...  
```

**Check:** what is a request?


* HTTP version should be 1.1

**[Status Codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)** have standard meanings; here are a few.
>
|Code|Reason|
|:---|:-----|
|200| OK
|301| Moved Permanently
|302| Moved Temporarily
|307| Temporary Redirect
|400| Bad Request
|403| Forbidden
|404| Not Found
|500| Internal Server Error

<a name="introduction_2"></a>
## JSON (10 min)  

JSON is short for _JavaScript Object Notation_, and is a way to store information in an organized, easy-to-access manner. In a nutshell, it gives us a human-readable collection of data that we can access in a really logical manner.

JSON is built on two structures:

* A collection of name/value pairs. In various languages, this is realized as an object, record, structure, dictionary, hash table, keyed list, or associative array.
* An ordered list of values. In most languages, this is realized as an array, vector, list, or sequence.

These are universal data structures. Virtually all modern programming languages support them in one form or another. It makes sense that a data format that is interchangeable with programming languages also be based on these structures.

##### Objects

An object is an unordered set of name/value pairs. An object begins with `{` (left brace) and ends with `}` (right brace). Each name is followed by `:` (colon) and the name/value pairs are separated by `,` (comma).

The syntax is as follows:

```
{ string : value, .......}
```
like:
```
{"count": 1, ...}
```

##### Array

An array is an ordered collection of values. An array starts and ends with `[` and `]`. Between them, a number of values can reside. If there are more than one values reside, they are separated by `,`.


The syntax is as follows:

```
[ value, .......]
```
like:
```
[1, 2, 3, ...]
```

**Check:** what kind of data can go into an array?
> We know that data can be stored as a string in double quotes, or a number, or true or false or null, or an object or an array.

<a name="ind-practice_1"></a>
## Independent Practice: Validate JSON (10 min)
JSON is very simple to use if correctly structured. One of the resources to validate JSON and check if the syntax is correct is [JSON Viewer](http://codebeautify.org/jsonviewer).

For this exercise, copy the JSON data from the starter code folder and insert it in the web app above, click "Validate".

If you see "Valid JSON", click "Beautify" and you will see a more readable way of JSON. If you do not see the message "Valid JSON", it means that there is a syntax error.

* first, correct errors if there are any
* then, work in pairs to identify the structure of the JSON:

    - what is a root element?
    - are there any arrays?
    - how many objects are there?
    - what are the attributes of an object?


<a name="guided-practice/"></a>
## Guided Practice: Pulling data from API (15 min)

APIs are methods and data formats to tell people how to "talk" to a system. A couple of examples will clarify:

### Example 1: Movies
The internet movie database is a large collection of data about movies. It can be browsed at the address: http://www.imdb.com/.

What if we wanted to programatically access the data in the database? Unless we are employees of IMDB.com, we probably don't have direct access to their internal database, so we cannot perform SQL queries on their data.

We could use scraping, a software technique to extra data from the web page. In some cases, we will have to do exactly that.
Note: check the "Terms of Service" before you scrape a website, you could be infringing their terms.

In other cases, the website offers a way to programatically access data from their database. That's an API.

In the case of movies, this is offered by http://www.omdbapi.com/


1. Let's try for example to retrieve the data about the "Avengers" movie in 2015:

In a browser paste:
    http://www.omdbapi.com/?t=avengers&y=2015&plot=short&r=json

you should see something like:

    {
    Title: "Avengers: Age of Ultron",
    Year: "2015",
    Rated: "PG-13",
    Released: "01 May 2015",
    Runtime: "141 min",
    Genre: "Action, Adventure, Sci-Fi",
    Director: "Joss Whedon",
    Writer: "Joss Whedon, Stan Lee (Marvel comics), Jack Kirby (Marvel comics)",
    Actors: "Robert Downey Jr., Chris Hemsworth, Mark Ruffalo, Chris Evans",
    Plot: "When Tony Stark and Bruce Banner try to jump-start a dormant peacekeeping program called Ultron, things go horribly wrong and it's up to Earth's Mightiest Heroes to stop the villainous Ultron from enacting his terrible plans.",
    Language: "English",
    Country: "USA",
    Awards: "2 wins & 37 nominations.",
    Poster: "http://ia.media-imdb.com/images/M/MV5BMTM4OGJmNWMtOTM4Ni00NTE3LTg3MDItZmQxYjc4N2JhNmUxXkEyXkFqcGdeQXVyNTgzMDMzMTg@._V1_SX300.jpg",
    Metascore: "66",
    imdbRating: "7.5",
    imdbVotes: "420,714",
    imdbID: "tt2395427",
    Type: "movie",
    Response: "True"
    }

Notice what happened: we interrogated a url and we received json as an answer.

2. Try submitting a couple more queries to familiarize with the API.
- You can also query an API from the command line using the app `curl`. Try typing:

    curl http://www.omdbapi.com/?t=whiplash&plot=short&r=json

you should see something like:

    {"Title":"Whiplash","Year":"2014","Rated":"R","Released":"15 Oct 2014","Runtime":"107 min","Genre":"Drama, Music","Director":"Damien Chazelle","Writer":"Damien Chazelle","Actors":"Miles Teller, J.K. Simmons, Paul Reiser, Melissa Benoist","Plot":"A promising young drummer enrolls at a cut-throat music conservatory where his dreams of greatness are mentored by an instructor who will stop at nothing to realize a student's potential.","Language":"English","Country":"USA","Awards":"Won 3 Oscars. Another 84 wins & 125 nominations.","Poster":"http://ia.media-imdb.com/images/M/MV5BMTU4OTQ3MDUyMV5BMl5BanBnXkFtZTgwOTA2MjU0MjE@._V1_SX300.jpg","Metascore":"88","imdbRating":"8.5","imdbVotes":"368,942","imdbID":"tt2582802","Type":"movie","Response":"True"}


### Example 2: Google Geocode API

Google offers a freely accessible API to query their GEO databases.

Try pasting the following line in your browser:

    https://maps.googleapis.com/maps/api/geocode/json?address=033+BELDEN+PL+San+Francisco+CA

you should see something like:

    {
    results: [
    {
    address_components: [
    {
    long_name: "33",
    short_name: "33",
    types: [
    "street_number"
    ]
    },
    {
    long_name: "Belden Place",
    short_name: "Belden Pl",
    types: [
    "route"
    ]
    },
    {
    long_name: "Financial District",
    short_name: "Financial District",
    types: [
    "neighborhood",
    "political"
    ]
    },
    {
    long_name: "San Francisco",
    short_name: "SF",
    types: [
    "locality",
    "political"
    ]
    },
    {
    long_name: "San Francisco County",
    short_name: "San Francisco County",
    types: [
    "administrative_area_level_2",
    "political"
    ]
    },
    {
    long_name: "California",
    short_name: "CA",
    types: [
    "administrative_area_level_1",
    "political"
    ]
    },
    {
    long_name: "United States",
    short_name: "US",
    types: [
    "country",
    "political"
    ]
    },
    {
    long_name: "94104",
    short_name: "94104",
    types: [
    "postal_code"
    ]
    }
    ],
    formatted_address: "33 Belden Pl, San Francisco, CA 94104, USA",
    geometry: {
    bounds: {
    northeast: {
    lat: 37.7913528,
    lng: -122.4038195
    },
    southwest: {
    lat: 37.7913502,
    lng: -122.4038379
    }
    },
    location: {
    lat: 37.7913502,
    lng: -122.4038379
    },
    location_type: "RANGE_INTERPOLATED",
    viewport: {
    northeast: {
    lat: 37.7927004802915,
    lng: -122.4024797197085
    },
    southwest: {
    lat: 37.7900025197085,
    lng: -122.4051776802915
    }
    }
    },
    place_id: "EiozMyBCZWxkZW4gUGwsIFNhbiBGcmFuY2lzY28sIENBIDk0MTA0LCBVU0E",
    types: [
    "street_address"
    ]
    }
    ],
    status: "OK"
    }

We queried an address and got back a lot of JSON data stored in Google's databases for that address.


### OAUTH

Many APIs are not free to access. You first need to register as a developer and obtain an authorization key. In most cases, this is also accompanied by a temporary token that needs to be renewed after some time. This is a way to prevent abuse on the server's resources.

You can read more about it here: http://oauth.net/2/


<a name="ind-practice_2/"></a>
## Independent Practice: A Closer Look at an API Request (15 min)

Let's make a basic HTTP request to an API. While we can technically just do this in the browser, we're going to use Postman - a Chrome plug-in for making HTTP requests - so we can look at it in more detail.  
Steps  
  1. [Download Postman](https://www.getpostman.com/).  
  2. Type in the "url" of an API call.  
  3. Ensure the "method" is "GET".  
  4. Press "Send".  

There is an immense number of APIs out there from which you can pull data. Try these ones out.

| API | Sample URL |
|-----|------------|
| **[This for That](http://itsthisforthat.com/)** | http://itsthisforthat.com/api.php?json |
| **[iTunes](https://www.apple.com/itunes/affiliates/resources/documentation/itunes-store-web-service-search-api.html)** | http://itunes.apple.com/search?term=adele |
| **[Giphy](https://github.com/Giphy/GiphyAPI)** | http://api.giphy.com/v1/gifs/search?q=funny+cat&api_key=dc6zaTOxFJmzC |
| **[OMDB API](http://www.omdbapi.com/)** | http://www.omdbapi.com/?t=Game%20of%20Thrones&Season=1 |
| **[StarWars](http://swapi.co/)** | http://swapi.co/api/people/3 |
| **[Stocks](http://dev.markitondemand.com/MODApis/)** | http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL |

Here's an example of a successful `200 OK` API call...

![Postman screenshot success](http://i.imgur.com/2TADr4J.png)

And here's an example of an unsuccessful `403 Forbidden` API call.

![Postman screenshot fail](http://i.imgur.com/r3nIhGH.png)

### Python Fundamentals

In the next class, we'll be building our own APIs using the Python framework Django. Let's learn some Python fundamentals to get prepared.


**What is Python?**

- Python was created by Guido Van Rossum in 1991
- Emphasizes **productivity** and **readability**
	* The language is easy to pick up and learn
	* This gentle learning curve brings makes it easier for many to contribute to production level code
	* Readable code means that almost anyone can pick up a piece of code and understand what it is doing
- Interpreted, object-oriented, high-level programming language with dynamic semantics
	* **Interpreted**: Code implementations execute instructions without having to *compile* them into machine-language instruction.
	* **Object-oriented** (OO): Instead of concentrating on isolated "actions", object-orientation enables us to focus on "objects" that contain data (attributes). Objects have specific procedures, known as methods (code) that can access and modify the attributes of the object.
		* OO makes it easier to write and reuse code in other programs
	* **High-level programming**: Related to the code readability mentioned earlier
		* Python syntax is similar to English, which makes it easy to use and automate!
	* **Dynamic semantics**: Once data has been specified, the machine must be instructed to perform operations on the data. Dynamic semantics provides flexibility at run-time.

**So why Python?**

* Python is extremely fun to develop in!
* Everything can be done with Python!
* If something can't be done, you can easily create an extension for it :)
* Everything can not only be done, but it can be done **fast**. For example, a program that takes you weeks in C++ might only take you a day to write in Python.
* Great for individual prototyping and commercial settings.
* Because it is a modern, elegant, highest level language.
* Because it is highly expressive, i.e., you will earn higher productivity.
* Because it comes with "batteries included", i.e. libraries for whatever you want.
* Because it is well documented and has a well-established and growing community.

#### Python: shell vs scripts

We can write code that is executed immediately by the Python interpreter by using a shell. This means we are able to "interact" with the results of the commands we pass. We can do this via :

- **python shell**: A python shell has a similar look and feel to a regular terminal shell. You can launch a python shell with:

```
> python
```

In many cases you may want to execute a program and simply get our results without interacting with the code. In those cases, we would need to create a Python script. We can use any *plain text editor* of our choice and save the code in a `.py` file.

#### Putting it all together

Let's create and save a file called `hi.py`.

And add the following code:

```python
print("Hello world!")
```

Now, to run our script by passing it as a Python command in our terminal, we would *also* need to write:

```python
> python hi.py
```

Voila! You've just run your first python script!!

## Programming fundamentals

Understanding core programming concepts and why they are used is just as important as knowing how to write code.

Before we start, let's review some basic programming concepts:

- **Syntax**: the syntax of a programming language is the set of rules that define the combinations of symbols that result in structured programs for that language.

- **Variables**: A variable is a storage location and an associated symbolic name that contains a value (in other words, a known or unknown quantity or piece of information). Variables can be of different `types`.
	- Strings
	- Integers
	- etc

- **Data Structures**: Data structurse are a particular way of storing and organizing data in a computer so that it can be used efficiently. Some examples include:
	- Lists
	- Tuples
	- Arrays
	- Matrices
	- Dataframes

- **Control Structures**: A control structure is a block of programming that analyses variables and chooses a direction in which to go based on given parameters. The term flow control details the direction the program takes (which way program control “flows”). Hence it is the basic decision-making process in computing; flow control determines how a computer will respond when given certain conditions and parameters. Some typical structures include
	- `If` statement
	- `For` loop
	- Functions

The interrelationship of these elements make it possible for us to write programs that implement algorithms and solve problems!

### You Do: Python Data Types (25 minutes)

Read through this portion of the lesson and execute the commands using the Python shell or a `.py` file.

#### Integers
Integers are numeric values and can be stored, manipulated, and expressed inside variables without quotes.

```bash
23
```
and it returns:
```bash
23
```

```bash
-44
```
and it returns:
```bash
-44
```

You can also perform basic math using integers as well. In iPython notebook type:
```bash
45-19
```
and it returns:
```bash
26
```

#### Strings
Strings are a type. They are the basic unit of text in Python and all the other types except integers may contain strings.

```bash
"I love Darth Vader"
```
and it returns:
```bash
'I love Darth Vader'
```

You can also make a variable refer to a string.
```bash
x= "Luke, I am your father"
```
Now type:
```bash
x
```
and it returns:
```bash
'Luke, I am your father'
```
Now type:
```bash
print(x)
```
and it returns:
```bash
Luke, I am your father
```

The print command prints the value that 'x' stands for on the screen. It removes the quotations. Whenever you type something into a type that isn't an integer, syntax (the commands that you give python, such as print), or variable (such as x just was) you need to put it into quotations. You can use 'single' or "double" quotations.

#### Tuples
A tuple is an unchangeable sequence of values.
When you typed ('I love Python') you only included one element.

```bash
x = ("Kirk", "Picard", "Spock")
```
When you do this you create a tuple with three elements. You can access these elements individually by typing the variable and the then inside brackets directly to the right of the variable type the number of the element to which you are referring.

Now type:
```bash
print(x[1])
```
and it returns:
```bash
Picard
```

You may think that it is odd that it returned element 2 instead of element 1. The reason that it did this is because Python starts numbering at 0. element 1 = 0, element 2= 1, element 3= 2. You can also call on the elements in reverse order.

Now type:
```bash
print(x[-1])
```
and it returns:
```bash
Spock
```

#### Lists
A list is a changeable sequence of data. A list is contained by square brackets i.e. [1,2,3]

```bash
x = ["Lord", "of", "the", "Rings"]
x[2] = "Frodo"
print(x)
```

and it returns:
```bash
['Lord', 'of', 'Frodo', 'Rings']
```

The code above changes element number 2 in x.

#### Dictionaries
Dictionaries contain a key and a value. { } enclose dictionaries (Note, that you can also construct a set with curly brackets. The first input in a dictionary pair is the 'key'. The second input in a
dictionary pair is the 'value'. The general format looks like this:
key1:value1


```bash
x = {'key1':'value1', 'key2':'value2'}
```

Now type:
```bash
print(x)
```

These may not be in the exact order in which you typed them. The reason for the different order is because dictionaries have no order. You cannot type x[0] and be referring to 'key1':'value1' . What you do to refer to a value is type the key.

```bash
x[key1] = 'I love Python'
```

Now type:
```bash
print(x)
```

and it returns:
```bash
{'key2': 'value2', 'key1': 'value1', 'I love Python': 'I love Python'}
```

The keys stay the same but the values are changeable. You can also only have one occurrence of a key in a dictionary, but you may have the values all be the same.

Now type:
```bash
x = {'key':'value1', 'key':'value2'}
```

Then type:
```bash
print(x)
```

and it returns:
```bash
{'key': 'value2'}
```

The first key is overwritten by the second.

Now type:
```bash
x = {'key1':'value', 'key2':'value'}
```

Then type:
```bash
print(x)
```

and it returns:
```bash
{'key2': 'value', 'key1': 'value'}
```

This example shows that you can create two separate keys with the same value.

[Integers, Strings, Tuples, Lists, Dictionaries](https://en.wikiversity.org/wiki/Python/Basic_data_types)

**Check:** Define/describe: integer, string, tuple, list, dictionary

### Control Flow

* The term `control flow` details the direction the program takes (which way control “flows” through the program). In other words, it determines how a computer will respond when given certain conditions and parameters.

#### **If**

An `if` statement is a conditional structure that, if proved true, performs a function or displays information.

Think of this as a decision that moves the flow of your program depending on the answer to a TRUE-FALSE question.

```
IF a person is older than 18
THEN they can vote
ELSE they cannot vote
```

We can express the pseudo-code above in Python as follows:

```python
if age_person > 18:
	return "They can vote"
else:
	return "They cannot vote"
```

Let's see another example:

```python
A = 10
B = 100
if A>B:
	print("A is larger than B")
elif A==B:
	print("A is equal to B")
else:
	print("A is smaller than B")
```

#### **For loop**

A loop statement in programming performs a predefined set of instructions or tasks until a predetermined condition is met. Think of this as a repetitive action that has to be performed until a specific condition occurs.

```
FOR each user of a service in a list
   PRINT greet them
```

In the pseudo-code above, the condition we are asked is to greet each user in a list. We stop the repetition when we reach the end of the list.

We can express this loop in Python as follows:

```python
users = ["Jeff", "Jay", "Theresa"]

for user in users:
    print("Hello %s" % user)
```

**Tip**: When creating a `for` loop, make sure the condition will always be met in order to prevent an endless loop, which can crash your environment.

Let's see another example. Can you explain what the program is doing?

```python
for x in [1,2,3]:
    print(x)

for key, value in params.items():
    print(key + " = " + str(value))
```

#### **Functions**

A function is a group of instructions, also known as a `named procedure`, used by programming languages to return a single result or a set of results.

Functions are a convenient way to divide our code into useful blocks, providing us with order as well as making the code more readable and reusable.

Here is how you define a function in python:

```python
def function_name(input1, input2...):
    1st block of instructions
    2nd block of instructions
    ...
```

Let us define a function that returns the square of the input value:

```python
def square(x):
	"""
	Return the square of x.
	"""
	return x ** 2
```

We can call this function as follows:

```python
var1 = 7

var2 = square(var1)

print(var2)
```
## Independent Practice: More Python Practice (25 mins)

<details>
<summary>1. A recipe you are reading states how many grams you need for the ingredient. Unfortunately, your store only sells items in ounces. Create a program to convert grams to ounces.

`ounces = 28.3495231 * grams`
</summary>
```python
def gr2oz(x):
	return 28.3495231 * x

grams = 10
ounces = gr2oz(grams)
print(ounces)
```
</details>

<details>
<summary>
2. Read in a Fahrenheit temperature. Calculate and display the equivalent centigrade temperature. The following formula is used for the conversion:

`C = (5 / 9) * (F – 32)`
</summary>
```python
def F2C(F):
    return (5.0/9.0) * (F - 32)

f=86
c= F2C(f)

print("{0} Fahrenheit is {1} centigrade".format(f,c))
```
</details>

<details>
<summary>
3. Calculate the amount obtained by investing the principal P for N years at the rate of R. The following formula is used for the conversion:

`A = P * (1 + R) ^ N`
</summary>
```python
def compound_interest(P, R, N):
    return P * (1 + R)**N

P = 1000
R = 0.1
N = 2

Interest = compound_interest(P, R, N)

print(Interest)
```
</details>
