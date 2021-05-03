# Mini-Monolith Architecture

This repository contains documentation of the Mini-Monolith
application design pattern.

## What is a Mini-Monolith?

Mini-Monoliths are applications that encapsulate a single
Domain of services where all possible transactions within
that Domain are contained within the Mini-Monolith except to
push data to ACID compliant data sources.

Typically a Mini-Monolith will be deployed and managed via
containers or through a hosted web server such as Azure App
Services which can leverage automatic or otherwise managed
deployments directly from source code repositories.

Mini-Monoliths should be hosted in services that can automatically
scale and spawn instances as necessary to meet demand or act
redundantly in the event of a failure of a mini-monolith.

## Problems Solved

Mini-Monoliths are a refinement of the Microservices architecture
to eliminate the complexity and pain of managing a deployed
Microservice platform.  Such pain points include:

* [Cross-service Communication](https://blog.revdebug.com/top-issues-with-microservices)
* Cross-service Transactions
* [Testing](https://blog.revdebug.com/top-issues-with-microservices)
* [Debugging Failures and Logic]()
* Versioning of Dependent Services
* Caching

Full monoliths typically don't have these difficulties due to
services being deployed within a single application where there
is not any exposure to Cross-service Communication or
Cross-service Transaction issues.  Also, Logging for monoliths is
much easier and simpler as you don't need a log collector to
consolidate logged messages from multiple services.

Monoliths also eliminate the need to deploy Dependent Services
that may easily become out of sync with the deployment of
dependent microservice that become brittle.

## Technologies Involved

Mini-Monoliths maintain all of these benefits by being built
on existing frameworks such ASP.Net WebAPI which provides a
robust environment for design, documenting, building and deploying
service architectures.  Mini-Monoliths refine these frameworks
by refining the scope of the encapsulated services exposed by
the framework.

![Basic Mini-Monolith Architecture](https://www.plantuml.com/plantuml/svg/VP0n3i8m34NtdC9YxnLG4x5swWbCQb5BRHmbBWlYxYGj22GAcVALzv-jj5anwJ9FHbad0eUPFNGSkEaaoCGwWar-P2MlIo9ZL2wa8oN063FS39JZPOuIA2WSR8mJUrIM0FO0c2jd_r7kHJbp_z1dIbVsj3FY93DoiKF_H5R18BFzGRelSXrL5uEcEMxLki1-SiOCg7Z6J4LPRj2h9DfS9PRdKjde6clbdKnBOIWV_000 "Basic Mini-Monolith Architecture")

### Of Plato, Forms and Models

> [Plato](https://docs.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design), that most famous student of Socrates, proposed that the concepts, people, places, and things we intuit and perceive with our senses are merely shadows of the truth. He dubbed this idea of a true thing a Form.
>
> To explain Forms, Plato used what's become known as the allegory of the cave. In this allegory, there exists a people that are bound inside a deep, dark cave. These cave people are chained in such a way that they can only ever see a blank wall of the cave that receives light from the opening. When an animal walks by the opening, a shadow is projected onto the interior wall that the cave dwellers see. To the cave dwellers, these shadows are the real thing. When a lion walks by, they point at the shadow of the lion and exclaim, "Run for cover!" But it is really only a shadow of the real Form, the lion itself.
>
>You can relate Plato's theory of Forms to DDD. Much of its guidance helps us get closer to the ideal model over time. The path to the Form you want to describe with your code is scattered about in the minds of domain experts, the desires of stakeholders, and the requirements of industries in which we're working. These are, in a very real sense, the shadows to Plato's imaginary cave dwellers.
>
>Furthermore, you are often constrained by programming languages and considerations of time and budget in trying to reach that Form. It's not much of a stretch to say these limitations are the equivalent of cave dwellers only ever being able to see the interior wall of shadows.
>
> Good models exhibit a number of attributes independent of their implementation. The fact of the matter is, the mismatch between the model that's in everyone's head and the model you're committing to code is the first thing an aspiring domain modeler should understand.
>
> ___The software you create is not the true model. It is only a manifestation—a shadow, if you will—of the application Form you set out to achieve. Even though it's an imitation of the perfect solution, you can seek to bring that code closer to the true Form over time.___

This last paragraph is prophetic for nearly every large project.  We gen an idea in our head of what the true model of our application looks like, only to find what gets built after the compromises made for pragmatics and other purposes does not 100% reflect our vision.

**And That's OK...** as long as the road leading there was honest.  Intentionally disrupting a project for any reason is never ok regardless of how much you disagree with methodology.

So all this talk of honesty seems out of place, doesn't it?  But what do you say when you are asked an opinion on an architecture during the design phase of the SDLC and you have a strong opinion?  Do you speak up and add your opinion?  Do you just wait for the architect to be done so you can just get to doing what you were going to do anyways?  By the time the second scenario gets to you, a lot of money has been spent, a lot more budgeted, people have been hired to fulfill specific jobs, often leading to relocations.  Contracts with vendors for services have been signed and so many more side effects arrive from architectural decisions.  It is _vitally_ important that all opposition to the design of an app be brought forth for discussion so that nobody is only looking at the shadows of lions on the back wall of the cave.

## Dividing an Application into Domains

First let's define Domain: According to Microsoft in [Best Practice - An Introduction To Domain-Driven Design](https://docs.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design):

> Domain-Driven Design(DDD) is a collection of principles and patterns that help developers craft elegant object systems. Properly applied it can lead to software abstractions called domain models. These models encapsulate complex business logic, closing the gap between business reality and code.

Continuing from Plato,

> The software you create is not the true model. It is only a manifestation—a shadow, if you will—of the application Form you set out to achieve. Even though it's an imitation of the perfect solution, you can seek to bring that code closer to the true Form over time.
>
> In DDD, this notion is called model-driven design. Your understanding of the model is evolved in your code. Domain-driven designers would rather not bother with reams of documentation or heavy diagramming tools. They seek, instead, to imbue their sense of domain understanding directly into their code.
>
> The idea of the code capturing the model is core to DDD. By keeping your software focused on the problem at hand and constrained to solving that problem, you end up with software receptive to new insights and moments of enlightenment. I like what Eric Evans calls it: crunching knowledge into models. When you learn something important about the domain, you'll know right where to go.

## Summary

1. Domain Driven Design is a living Architecture
1. The Code we Deliver is a Manifestation of the Understanding of the Domain at a point in time.
1. Keep the solution focused on the problem at hand (which is the Domain).

When you put these three things together, the Mini-Monolith makes more and more sense.

1. Models are always shared and up-to-date within the Domain.
1. The Logic of the Mini-Monolith is focused on on the Domain, but all of the Domain at the same time.
1. A single Mini-Monolith is much easier to reason about as the Living Architecture of the Domain.  All artifacts (code, requirements, etc.) stay together and move together like a living organism.

### What Mini-Monolith Is Not

1. Mini-monoliths do not hide public aspects of a domain.  All public aspects should be exposed via API.
1. Mini-Monoliths do not endeavor to solve performance issues surrounding communication with __other domains__.  This is solely a function of the technologies chosen to implement each domain's Mini-Monolith.
1. Mini-Monoliths do not discourage strong usage of patterns, such as the Strategy Pattern which allows Domains to be polymorphic while maintaining proper separation of Concerns.
1. Mini-Monoliths do not drive database design.  There is a correlation between business entities and data modeling, but only so far as the domain does not influence decisions that prevent the achievement of Forth Normal Form in the Database.
1. Mini-Monoliths are not intended to be transaction brokers for multiple services.  The need to share a transaction between services should be extraordinary, no commonplace.  If you find yourself constantly initiating transactions to other services that you mus build upon, then there are too many services involved with the scope of the use case and the identification of problem domains is incorrect.

### An Example

![Component](https://www.plantuml.com/plantuml/svg/TOyn2W8n44Nxd698xmKiP8tR23Qo2zRZxXJ1P6QTZ7fzim511CiFxptuNJ5KU-G4_Y1v4IOsxonQ8ZZcHMKXXLuoHeQWXBTPNkpSz66hLdqOI9zn8WzOO9Qy_mPwDFm5WdCh1fjTMx25KP4BJXQ5CS55er5bgdh5Gk27ywarI5kYt5ChXBLGnxz0HppNSsy0 "Component")

Here we have the most basic use case, saving the cart to the database.


#### Microservices Implementation

In the classic Microservices implementation we would have at least two services involved, the first being a REST endpoint to accept the cart as an object which would translate the cart to business entities, then send the business entities to the Database Service which would normalize the business entities to entities and push the entities to the database for persistence.  Along the way, the REST endpoint created a Transaction that allows the REST endpoint to timeout gracefully and cancel the write to the database to maintain data hygiene.

![Microservice Save Cart](https://www.plantuml.com/plantuml/svg/TOyn2W8n44Nxd698xmKiP8tR23Qo2zRZxXJ1P6QTZ7fzim511CiFxptuNJ5KU-G4_Y1v4IOsxonQ8ZZcHMKXXLuoHeQWXBTPNkpSz66hLdqOI9zn8WzOO9Qy_mPwDFm5WdCh1fjTMx25KP4BJXQ5CS55er5bgdh5Gk27ywarI5kYt5ChXBLGnxz0HppNSsy0 "Microservice Save Cart")

The most common method for implementing these transactions in microservices is using the [Saga Pattern](https://medium.com/swlh/microservices-architecture-what-is-saga-pattern-and-how-important-is-it-55f56cfedd6b#:~:text=Choreography%20is%20the%20simplest%20way%20to%20implement%20SAGA,local%20transactions%20then%20Choreography%20is%20very%20fit%20option.).  You can think of the Saga Pattern is being an implementation of British Bureaucracy which is always expanding to mee the needs of the expanding Bureaucracy.  Every new microservice gets its own state machine which gets duplicated every time the service joins a transaction.  In the end, all state machines get cascading vote, and if any state machine dissents (or doesn't answer), then the transaction fails.  Since microservices are intentionally part of the puzzle and practically always depend on other microservices, this process is repeated constantly on each write.

![Mini-Monolith Save Cart](http://www.plantuml.com/plantuml/svg/TOwn2i9044Jx_Ohb-lo0XIJ69c10ERjWiIPR7CGzt5tZxnjF41lRUVE6gSr9_N6RCVH9KjLdmREI68sUiWI0YPokP8mXdWuOMHVMW6Heznc6hzIIUg5fv0jMspV63JPjj_yTX66d-McifVD7Nxr82t_2vjW1r2pJUl85 "Mini-Monolith Save Cart")
