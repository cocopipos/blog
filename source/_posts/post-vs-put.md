title: What is the difference between the HTTP methods POST and PUT?
date: 2016-01-03 21:02:20
tags: [http, put, post, rest]
---

On his [article](http://martinfowler.com/articles/richardsonMaturityModel.html) about Richardson's REST Maturity Model Martin Fowler says:

> The trade-offs between using POST and PUT here are more than I want to go into here, maybe I'll do a separate article on them some day. But I do want to point out that some people incorrectly make a correspondence between POST/PUT and create/update. The choice between them is rather different to that.

It seems that the day in which Martin is going to explain us what is involved in the choice between POST and PUT did not arrive yet, so I will try to explain it myself.

In our way to enlightenment, let's take a look on what says [HTTP's RFC](http://tools.ietf.org/html/rfc2616#section-9.6) about the difference between POST and PUT:

> The fundamental difference between the POST and PUT requests is reflected in the different meaning of the Request-URI. *The URI in a POST request identifies the resource that will handle the enclosed entity.* That resource might be a data-accepting process, a gateway to some other protocol, or a separate entity that accepts annotations. In contrast, *the URI in a PUT request identifies the entity enclosed with the request* -- the user agent knows what URI is intended and the server MUST NOT attempt to apply the request to some other resource.

So, the difference between POST and PUT has nothing to do with create/update. Actually, both methods can create or update a resource. The difference is in what resource is going to be created/updated by the request.

In the case of PUT, the resource being created or modified is the resource pointed by the Request-URI. As stated in HTTP's RFC: "The PUT method requests that the enclosed entity be stored under the supplied Request-URI".

For the POST method, the Request-URI does not indicate a resource to be created or updated, but a resource capable of handling the entity enclosed in the request. As the result of the request handling a new resource may or may not be created. If a new resource is created, the server must respond with 201 (Created) and set the Location header with the URI of the new resource.

Another difference between these two methods is that PUT is supposed to be idempotent, while POST is not. This means that if a PUT request is made N times, the result must be the same for all them. POST method does not have this guarantee.
