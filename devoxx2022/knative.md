# Knative from the perspective of a Step-Function user (i.e. me)

[skip to the stuff about the talks](#talks)

I went to two talks about Knative, and several other talks mentioned it.
Knative provides serving and eventing for Kubernetes.
It is often talked about as allowing serverless on Kubernetes,
but as several people mentioned out, it does more than that.

My interest is particularly in whether there could be an Open Source alternative to AWS Step Functions.
Step Functions work really well for us as a way of composing our lambdas into a flow.

If you consider an old-school monolith, like Prodgen on Ripple, then each lambda would represent a module in the application.
By separating those modules out into separate lambdas we have really enforced the separations between them.
(Good programmers keep those separations in a monolith anyway but there's not the same enforcement.)

But obviously what we've lost when we do that is those links between the modules/lambdas.
This a problem.
When you're trying to troubleshoot a system, you need to be able to see the flow through it.
In a monolith you can use an IDE to track down where something is called from,
not to mention that there might be a stack trace to help you out.
But in a distributed system it can be a massive hassle to work out where something got lost,
or how it got to the place where it failed.
You're probably going to have to rely on your memory about how things connect up, 
or on diagrams in docs which might now be out of date.
Correlation ids can help but you'd better have good tooling to find those ids in different logs.
Splitting up monoliths shunts the complexity of how things are connected into configuration code 
which is almost certainly in a different language and possibly a different repo.

Step Functions are hugely useful because they let us link up our lambdas, 
together with basic flow control like "if output is empty, then skip to the end", etc.
They also give us a lovely UI for debugging.  I see them as a bit like the Actor model,
which is often credited with giving Erlang its reliability, where immutable messages
are passed between entirely distinct bits of code which are allowed to mutate state.

But we write tons and tons of config in AWS-bespoke yml.
All AWS things are better when they use Open-Source standards,
so even if we never take anything off AWS it would still be better to use OS tooling.
Plus it would be more comfortable if our infrastructure-as-code code 
was not so closely tailored to the platform on which it is deployed -- 
that doesn't feel like the best separation of concerns.
The business logic is all jumbled up with platform specifics.
Platform details ought to be abstracted away from business logic.

## Talks
## [Knative and Spring -- Bringing Back the func](https://www.devoxx.co.uk/talk/?id=5267)

A talk about using Knative with the Spring framework.
(Since we swapped to doing serverless with Java we've not used the Spring framework,
and I have found this refreshing.
I accept that it's pretty standard for making web services,
but I think it's a bit heavyweight for a little lambda.)

### Their summary of Knative serving
* dev-friendly abstractions
* from code to "url" -- I wanted to query what they meant by this -- are they assuming all services are REST APIs?
* autoscaling, scaling to zero -- scaling from zero to one is hard
* progressive rollouts
* things can be request-driven or event-driven
* cloud agnostic
* not only about functions -- about extra capabilities for Kubernetes

### The Spring parts
* Spring Native is going to bring graalvm native to Spring (this will be nice if they can get it up to the required reliability)
* Spring Cloud Function allows the composition of functions within a codebase as one unit of deployment
  * but it seems to require horrible yml to chain things together -- why not just write a Java class?
  * apparently it does "transparent type conversion" -- this is probably excellent but they didn't explain what it means so it made me anxious
  * the example they made was a bit Enterprise Fizz Buzz -- admittedly it was a short demo and it's hard to come up with something for those that both demonstrates capabilities and makes it look like the capabilities are worth the trouble

### Their summary of Knative eventing
* event routing and triggers
* developer-friendly abstractions
* event-driven architectures
* event routing
* polyglot support with CloudEvents
* pluggable
* cloud agnostic
#### their pros and cons
* event-based allows systems to be more reactive
* the message broker is abstracted
* CloudEvents has a standard structure
* monitoring is required for understanding data
* eventual consistency

### I asked the Knative speaker afterwards about Step Functions
He said to look at [https://serverlessworkflow.github.io/](https://serverlessworkflow.github.io/).

## Live-diagramming Knative
This was a good talk explaining how Knative serving works on top of Kubernetes.
I think it's essentially online here [https://tanzu.vmware.com/developer/tv/enlightning/6/](https://tanzu.vmware.com/developer/tv/enlightning/6/)

She said that the key benefits of Knative serving are:
* less yml
* auto TLS
* concurrency based on number of requests
  * good for FaaS aka serverless but not just for Faas
  * essentially anything that you might want to scale to zero
  * scaling from zero to 1 is hard but Knative has a thing in place to handle it

and she said to look for the knative.dev tutorials







