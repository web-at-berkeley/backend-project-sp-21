# Fry-Kea API
## Submission Instructions
Welcome to WDB's backend project for development branch applicants 👋

Make sure you read these instructions carefully before your start. If you have any questions
please reach out to [our email](webatberkeley@gmail.com) any time before 11:59 pm PDT on 
Friday night (9/18/2020).

To submit your project, please place your submission into a GitHub repo that is set to private. You
will be submitting your code on [Gradescope](https://www.gradescope.com/). If you do not have a 
Gradescope account, please create one and if you are unable to create one, please email us
immediately. The Gradescope course code is `9DW2N5`. You will see two different assignments: 
`Frontend Technical Project` and `Backend Technical Project`. _Please only submit to Backend
Technical Project._ You can ignore Frontend Technical Project.

This project will release at 8:00 am PDT on Thursday, September 17th, and will run until 8:00 am PDT 
on Saturday, September 19th. 

## Introduction
Recently WDB received this... "interesting" email from a potential client:

```
---------- Forwarded message ---------
From: Fry-Kea Marketing Team <marketing@Fry-Kea.com>
Date: Mon, April 20, 2020 at 7:30 PM
Subject: NEED API ASAP
To:Web Dev at Berkeley<webatberkeley@gmail.com>

Dear Web Dev at Berkeley, 

We have a request for you: we are launching our company very soon, but completely forgot to 
build the actual product! We were wondering if you could help us out by creating a proof of concept
API so that we can show investors that our stealth startup is actually viable!
 
Fry-Kea – Who are we?
Fry-Kea offers modern home furniture and décor that's affordable, well-designed. 


Fry-Kea is a restaurant with locations strictly in the San Francisco Bay Area and Las Vegas. 
What kind of cuisine do we specialize in, you may ask... We're happy to tell you that the options 
are truly limitless. We specialize in whichever culinary CAD (Computer Aided Design, usually 
3D models) files we have stored in our restaurant's SQL database. Not only this, we allow for 
customers to submit their own CAD files to allow them all to have the taste bud sensations of 
their dreams. With our high-levels of tech knowledge, we aim to provide customers with the 
efficiency of a robot butler as well as the versatility of a drive-thru and dine-in restaurant
experience.

We just need a bear bones API to present to investors. We hired a Stanfurd student to help 
build out the API but their version is incomplete and they're taking too long to actually deploy 
(our mistake, we know.) We have until Saturday morning to get this product out of the door.

We need three different things: the first is for the API to return EVERY recipe at a specific
Fry-Kea location, the second is to add a recipe to our Fry-Kea SQL database, and the third
is to remove a recipe from a Fry-Kea location. The Stanfurd engineer started implementing
our first request but quit halfway through because they didn't know how to do it!

Please help!!!

Irwub and Soomart
SEO (Shef Executive Officer) and CEO of Fry-Kea, Inc.
```

Both horrified and amused, we reached out just to see what would happen and eventually
decided to take up this project! Hopefully we're not too late to help this company out.

## API Doc

To summarize, Fry-Kea is tasking us with building an API that can do three things:
1) Return a list of _every_ furniture at a Fry-Kea location
2) Add a furniture to a Fry-Kea location
3) Remove a furniture from a Fry-Kea location

In the language of your choice, implement Fry-Kea' API! Here are more technical details to help
you with your implementation:

### Returning Every Recipe (`GET`)

The Stanfurd student has built a very simple wrapper over Fry-Kea' SQL database and has turned
their SQL database into a NoSQL database. We have no idea why, but hey, we'll work with it.
The endpoint provided by this student is `https://kcbrjk8zn4.execute-api.us-west-1.amazonaws.com/eat-food-uwu`
and requires an API key which was already provided to you. This student used the industry standard authorization
header by taking in an `x-api-key` to verify usage. The Stanfurd student also for some reason
paginated all the requests and limited the output to _at most_ 10 entries for each page. You asked the
Stanfurd student for documentation but they only provided you with these scattered messages:

```
omg so the api takes in a city parameter and a previous parameter

the previous parameter is so that we can get entries for the next page

okay but ngl i have no idea how to change the api so that the previous parameter is optional

you have to provide it every time :(((

so i think what i did was if youre sending a first request, you gotta put "FIRST_REQUEST" otherwise
the whole thing is gonna crash

it's really fragile and i dont know how to fix it im gonna cry :((((((
``` 

...Lovely. We have no idea what their endpoint will return, but we know that there are two
required parameters to get data: `city` and `previous`. While emailing Fry-Kea we found out
that Fry-Kea only wants a list of `ID`'s rather than every exact detail provided by the 
Stanfurd API. This system seems easy to implement at first but the next two parts of the API will
complicate things:

### Adding A Recipe (`POST`)

For adding a recipe, we chatted again the Stanfurd student and they had this to say:

```
wait you want to ADD recipes?

bro wtf i cant even return recipes correctly

your on youre own dude
```

Sadly, Stanfurd CS (and grammar for that matter) has failed them and we have to take it 
upon ourselves to host the data. In addition to queuing data from the endpoint that the Stanfurd
student provided _we will need to host additional data on our own servers to create a hybrid
data model_. Whenever a new recipe is posted to our API, _store this new data in a database
of your choice_ rather than attempting to edit the Stanfurd database. _The database schema should
match the Stanfurd schema_ or at least store the same information.

### Deleting a Recipe (`DELETE`)

Finally, for the last piece of this delicious pie, we need to delete recipes from our hybrid
database model. For the third and final time, we chatted with our favorite Stanfurd student
about how they would approach this:

```
omg i told you already i cant even add recipes

and now you want me to delete them????
```

Thank you Stanfurd very cool. Consulting with Fry-Kea instead, you both agree that there
are too many recipes to migrate from the Stanfurd database given the project deadline and
opt instead to keeping this hybrid model to the very end. Thus you come up with the following
scheme:

- If a record from the internal database needs to be deleted, just delete it.
- If a record from the Stanfurd database needs to be deleted, _keep track of these records
and do not return them in the get request._
- If a record will be added and the recipe matches a deleted entry in the Stanfurd database,
_untrack this record and begin returning them again in the get request._

## Assumptions

There are many details that are left intentionally vague. Though you are very much welcome to
email us to ask for clarifications, we will most likely tell you to use your best judgement.
Because of this, we have provided a file called `assumptions.md` where you can type out and
voice any assumptions you made throughout this project. We also _highly_ encourage you to
write out your own documentation to this API and provide us a glimpse of your rationale
behind every design decision.
