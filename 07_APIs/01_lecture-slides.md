Accessing Databases via Web APIs
========================================================
author: PS239T
date: "06 March, 2019"

What is an API?
========================================================

* API stands for **Application Programming Interface**

* a set of rules and procedures that facilitate interactions between computers and their applications

* This is an API (thanks to Quora for the example):
![](figures/apis_metaphor.jpeg)

Web APIs
========================================================

* allows users to query a remote database over the internet

* take on a variety of formats 

* majority adhere to a particular style known as **Representational State Transfer** or **REST**

* "RESTful" APIs are convenient because we can use them to query databases using URLs 

RESTful Web APIs are All Around You...
========================================================

Consider a simple Google search.

Go ahead and search something.

Ever wonder what all that extra stuff in the address bar was all about?  

RESTful Web APIs are All Around You...
========================================================

It looks like Google makes its query by taking the search terms, separating each of them with a "`+`", and appending them to the link:

`https://www.google.com/#q=`

So that we have

`https://www.google.com/#q=search1+search2`

So can change our Google search by adding some terms to the URL.

Some Basic Terminology: URL
========================================================

* Uniform Resource Location
* a string of characters that, when interpreted via the Hypertext Transfer Protocol (HTTP)
* points to a data resource, notably files written in Hypertext Markup Language (HTML) or a subset of a database.


Some Basic Terminology: HTTP Methods / Verbs
========================================================

* *GET*: requests a representation of a data resource corresponding to a particular URL.  The process of executing the GET method is often referred to as a "GET request" and is the main method used for querying RESTful databases.
    
*  *HEAD*, *POST*, *PUT*, *DELETE*: other common methods, though mostly never used for database querying.

How Do GET Requests Work?  A Web Browsing Example
========================================================

* Surfing the Web = Making a bunch of GET Requests

* For instance, I open my web browser and type in http://www.wikipedia.org.  Once I hit return, I'd see a webpage.

* Several different processes occured, however, between me hitting "return" and the page finally being rendered. 

Step 1: The GET Request
========================================================

* web browser took the entered character string 
* used the command-line tool "Curl" to write a properly formatted HTTP GET request 
* submitted it to the server that hosts the Wikipedia homepage.

STEP 2: The Response
========================================================

* Wikipedia's server receives this request
* send back an HTTP response
* from which Curl extracted the HTML code for the page


```
[1] "<!DOCTYPE html>\n<html lang=\"mul\" class=\"no-js\">\n<head>\n<meta charset=\"utf-8\">\n<title>Wikipedia</title>\n<meta name=\"description\" content=\"Wikipedia is a free online encyclopedia, created and edited by volunteers around the world and hosted by the Wikimedia Foundation.\">\n<![if gt IE 7]>\n<script>\ndocum"
```

STEP 3: The Formatting
========================================================

* raw HTML code was formatted and executed by the web browser
* rendering the page as seen in the window.

RESTful Database Querying: The GET Request
========================================================

* URL we supply must be constructed so that the resulting request can be interpreted and succesfully acted upon by the server.  

* Likely that the character string must encode **search terms and/or filtering parameters**, as well as one or more **authentication codes**.  

* While the terms are often similar across APIs, most are API-specific.

RESTful Database Querying: The Response
========================================================

* unlike web browsing, the content of the server's response that is extracted by Curl is unlikely to be HTML code. 

* will likely be **raw text** response that can be parsed into one of a few file formats commonly used for data storage.  

* usual suspects include .csv, .xml, and .json files.

RESTful Database Querying: The Formatting
========================================================

* web browser parsed the HTML code, 
* but **we need R, Python, or other programming languages** to parse the server response 
* and convert it into a format for local storage (e.g. matrices, dataframes, databases, lists, etc.).

The Question
========================================================

### How has interest in Adam Rippon fluctuated over time? 


**YOUR CHALLENGE:** Characterize the popularity of Adam Rippon over the past 10 years. Specifically, what trends do you see?

STEP 1: Finding Data Resources
========================================================

* Popularity = How frequently or widely something is referenced over time
* Popularity = Frequency in Newspapers
* Popularity = Frequency in New York Times

[NYT Article API](http://developer.nytimes.com/)

STEP 2: Getting API Access
========================================================

* For most APIs, a key or other user credentials are required
* Most APIs are set up for developers, so you’ll likely be asked to register an "application"
* rate limits = total number of calls / time
* NYT API = 10 calls per second and 10,000 calls per day

[NYT Article API Keys](http://developer.nytimes.com/apps/mykeys)

STEP 3: Constructing API GET Request
========================================================

Most GET request URLs for API querying have three or four components:

1. **Base URL**: a link stub that will be at the beginning of all calls

2. **Authenication Key/Token**: a user-specific character string

3. **Response Format**: a character string indicating how the response should be formatted; usually one of .csv, .json, or .xml

4. **Search Parameters**: a character string telling the server what to extract from the database; basically a series of filters used to point to specific parts of a database

STEP 3: Constructing API GET Request
========================================================

* Common architectures, but each API has its own unique quirks.
* Carefully reviewing the API documentation is critical!!
* Fortunately, the NYT Article API is [very well documented!](http://developer.nytimes.com/docs/read/article_search_api_v2)

Try it Out
========================================================

http://developer.nytimes.com/io-docs
