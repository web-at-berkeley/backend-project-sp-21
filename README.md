# Fry-Kea API
## Submission Instructions
Welcome to WDB's backend project for development branch applicants 👋

Make sure you read these instructions carefully before your start. If you have any questions
please reach out to [our email](webatberkeley@gmail.com).

To submit your project, please place your submission into a GitHub repo that is set to private. You
will be submitting your code on [Gradescope](https://www.gradescope.com/). If you do not have a 
Gradescope account, please create one and if you are unable to create one, please email us
immediately. The Gradescope course code is `BP347P`. You will see two different assignments: 
`Frontend Technical Project` and `Backend Technical Project`. _Please only submit to Backend
Technical Project._ You can ignore Frontend Technical Project.

The technical project will be due at 8:00 am PT on Monday, Febuary 8th. We will be unable to respond to clarification emails sent in after 11:59 pm PST on Sunday, February 7th, so if you have any questions about the project, please let us know before then. 


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
Fry-Kea offers modern home **fruitniture** and décor that's affordable, well-designed, and... juicy! We specialize in fusing 
the look of fresh and juicy fruits with ordinary home furniture to provide our customers with the 
finest, most interesting, and most delicious hosue furnishment experience. 

We are a furniture store located in the San Francisco Bay Area and Las Vegas. For our furniture store,
we provide the customers with the ability to create their own **fruitniture** by combining a fruit with 
a furniture.

We just need a bear bones API to present to investors. We hired a Stanfurd student to help 
build out the API but their version is incomplete and they're taking too long to actually deploy 
(our mistake, we know.) We have until Saturday morning to get this product out of the door.

We need three different things: the first is for the API to return EVERY type of **fruitniture** that
we have in store, the second is to allow the customer to add their own fruit / furniture combination
 to our Fry-Kea SQL database, and the third is to remove a combination from a Fry-Kea location. 
The Stanfurd engineer started implementing our first request but quit halfway through because they didn't know how to do it!

Please help!!!

Irwub and Soomart
SEO (Shef Executive Officer) and CEO of Fry-Kea, Inc.
```

Both horrified and amused, we reached out just to see what would happen and eventually
decided to take up this project! Hopefully we're not too late to help this company out.

## API Doc

To summarize, Fry-Kea is tasking us with building an API that can do three things:
1) Return a list of **fruitniture** by combining fruit and furniture. 
2) Add a single / combination of fruit and furniture to a database.
3) Remove a combination / single fruit or furniture from a database.

In the language of your choice, implement Fry-Kea' API! Here are more technical details to help
you with your implementation:

### Returning Every **Fruitniture** (`GET`)

The Stanfurd student has built a very simple wrapper over Fry-Kea' SQL database and has turned
their SQL database into a NoSQL database. We have no idea why, but hey, we'll work with it.
The endpoints provided by this student are:

1. http://fry-kea-api.herokuapp.com/api/fry
2. http://fry-kea-api.herokuapp.com/api/kea


The "fry" endpoint returns a list of fruits, and the "kea" endpoint returns a list of furniture. 
Fry-kea requires you to return a list of **fruitniture** instead! which means that you need to 
join the two lists by combining fruit & furniture that *share the same first character*.

### Adding A Fruit, Furniture, or a **Fruitniture** (`POST`)

For adding a recipe, we chatted with the Stanfurd student and they had this to say:

```
wait you want to ADD a new Fruitniture?

bro wtf i cant even return fuirnitures correctly

your on youre own dude
```

Sadly, Stanfurd CS (and grammar for that matter) has failed them and we have to take it 
upon ourselves to host the data. In addition to queuing data from the endpoint that the Stanfurd
student provided _we will need to host additional data on our own servers to create a hybrid
data model_. Whenever a new fruit, a new furniture, or a new Fruitniture is posted to our API, _store this new data in a database
of your choice_ rather than attempting to edit the Stanfurd database. 

For the hybrid data model that you will be creating, remember that the user can choose to add a fruit, a furniture, or a combination of fruitniture. 
This means that if a new fruit is added, say blackberry. When using the "GET" endpoint, any furniture that starts with "b" provided by the Stanford API needs
to also join the newly added blackberry as well. This is the same for any newly added furniture. 

For fruitniture, both the fruit and the furniture need to be able to join with any other existing fruit and furniture as well!

### Deleting a Fruit or Furniture (`DELETE`)

Finally, for the last piece of this delicious pie, we need to delete data from our hybrid
database model. For the third and final time, we chatted with our favorite Stanfurd student
about how they would approach this:

```
omg i told you already i cant even add fruits

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
