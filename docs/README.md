# Mini-Monolith Architecture

This repository contains documentation of the Mini-Monolith
application design pattern.

## What is a Mini-Monolith?

Mini-Monoliths are applications that encapsulate a single
Domain of servics where all possible transactions within
that Domain are contained within the Mini-Monolith except to
push data to ACID compliant data sources.

Typically a Mini-Monolith will be deployed and managed via
containers or through a hosted web server such as Azure App
Services which can leverage automatic or otherwise managed
deployments directly from sourc code repositories.

Mini-Monoliths shouls be hosted in services that can automatically
scale and spawn instances as necessary to meet demand or act
redundantly in the event of a failure of a mini-monolith.

## Tecnologies Involved

Mini-Monoliths are a refinement of the Microservices architure
to eliminate the complexity and pain of managing a deployed
Microservice platform.  Such pain points include:

* Cross-service Communication
* Cross-service Transactions
* Debugging Failures and Logic
* Versioning of Dependent Services
* Caching

Full monoliths typically don't have these difficulties due to
services being deloyed within a single application where there
is not any exposure to Cross-service Communication or
Cross-service Transaction issues.  Also, Logging for monoliths is
much easier and simpler as you don't need a log collector to
consolidate logged messages from multiple services.

Monoliths also eliminate the need to deploy Dependent Services
that may easily become out of sync with the deployment of
dependent microservice that become brittle.

Mini-Monoliths maintain all of these benefits by being built
on existing frameworks such ASP.Net WebAPI which provides a
robust environment for design, documenting, building and deploying
service architectures.  Mini-Monoliths refine these frameworks
by refining the scope of the encapsulated services exposed by
the framework.

![Basic Mini-Monolith Architecture](https://www.plantuml.com/plantuml/svg/VP0n3i8m34NtdC9YxnLG4x5swWbCQb5BRHmbBWlYxYGj22GAcVALzv-jj5anwJ9FHbad0eUPFNGSkEaaoCGwWar-P2MlIo9ZL2wa8oN063FS39JZPOuIA2WSR8mJUrIM0FO0c2jd_r7kHJbp_z1dIbVsj3FY93DoiKF_H5R18BFzGRelSXrL5uEcEMxLki1-SiOCg7Z6J4LPRj2h9DfS9PRdKjde6clbdKnBOIWV_000 "Basic Mini-Monolith Architecture")
