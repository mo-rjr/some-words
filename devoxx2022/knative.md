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

But obviously what we've lost when we do that is precisely those links between the modules/lambdas.
This a problem.
When you're trying to troubleshoot a system, you need to be able to see the flow through it.
In a monolith you can use an IDE to track down where something is called from,
not to mention that there might be a stack trace to help you out.
But in a distributed system it can be a massive hassle to work out where something got lost,
or how it got to the place where it failed.
You're probably going to have to rely on your memory about how things connect up, 
or on diagrams in docs which might now be out of date.
Correlation ids can help, but you'd better have good tooling to find those ids in different logs.
Splitting up monoliths shunts the complexity of how things are connected into configuration code 
which is almost certainly in a different language and possibly a different repo.

Step Functions are hugely useful because they let us link up our lambdas, 
together with basic flow control like "if output is empty, then skip to the end", etc.
They also give us a lovely UI for debugging.  I see them as a bit like the Actor model,
which is often credited with giving Erlang its reliability, where immutable messages
are passed between entirely distinct bits of code which are allowed to mutate state.

But we write tons and tons of config in AWS-bespoke yml.
All AWS things are better when they use Open-Source standards,
so even if we never take anything off AWS it would still be better to use OS definitions.
Plus it would be more comfortable if our infrastructure-as-code code 
was not so closely tailored to the platform on which it is deployed -- 
that doesn't feel like the best separation of concerns.
The business logic is all jumbled up with platform specifics.
Platform details ought to be abstracted away from business logic.

## Talks
## [Knative and Spring -- Bringing Back the func](https://www.devoxx.co.uk/talk/?id=5267)

[Video available here](https://www.youtube.com/watch?v=EKDYE_dStTI)

A talk about using Knative with the Spring framework.
(Since we swapped to doing serverless with Java we've not used the Spring framework,
and I have found this refreshing.
I accept that it's pretty standard for making web services,
but I think it's a bit heavyweight for a little lambda.)

### Their summary of Knative serving
* dev-friendly abstractions
* from code to "url" -- _I wanted to query what they meant by this_ -- _are they assuming all services are REST APIs?_
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
#### Their pros and cons
* event-based allows systems to be more reactive
* the message broker is abstracted
* CloudEvents has a standard structure
* monitoring is required for understanding data
* eventual consistency

### I asked the Knative speaker afterwards about Step Functions
He said to look at [https://serverlessworkflow.github.io/](https://serverlessworkflow.github.io/).

## Live-diagramming Knative
[Video available here](https://www.youtube.com/watch?v=a3rIuPatyvs)

She has some live-diagramming videos online too: [https://tanzu.vmware.com/developer/tv/enlightning/6/](https://tanzu.vmware.com/developer/tv/enlightning/6/)

This was a good talk explaining how Knative serving works on top of Kubernetes.

She said that the key benefits of Knative serving are:
* less yml
* auto TLS
* concurrency based on number of requests
  * good for FaaS aka serverless but not just for Faas
  * essentially anything that you might want to scale to zero
  * scaling from zero to 1 is hard but Knative has a thing in place to handle it

and she said to look for the knative.dev tutorials


## Comments
Edmund, 2022-05-30
*Really interesting set of notes Rebecca - thanks for putting together. Also IMO great way of sharing!*
> When you're trying to troubleshoot a system, you need to be able to see the flow through it.
In a monolith you can use an IDE to track down where something is called from

Tangential to kubernetes, but IMO relevant to your wider point: just to note that personally, seeing flow is *already* a pain point in monolith. Just one that some in Tech may not be quite so aware of, as Tech *have* the IDE fallback to see flow in monolith.

As a scientist, I'm sometimes called on to help debug issues in operational science models, as I have relevant subject matter expertise which colleagues in Tech don't. In debugging, I've often had to work through operational architecture layers around the models, in order to understand the call context (when model is being run, arguments going in, ...). These architecture layers are written by my Tech colleagues, and are in Javascript. 

The main tools at my disposal for tracking flow are using browser to inspect architecture layer repos, hosted in BitBucket/GitHub. I don't have Javascript experience, or knowledge of how to set up an IDE to see the flow between widely-separated repos. And the need here comes up *just* infrequently enough that it's hard to justify upskilling myself. Faster to just try to impute flow manually, via browser hammer: hunting through imports, and using these to look up other repositories. Occasionally with recourse to commit histories & ancient tickets, and using the sort of diagrams/memory cribs you mention.

Faster, but very painful: such a shame that the browser-based approach only seems to provide these cross-repo flow insights via this manual approach - that it doesn't seem possible to get flow insights automagically, e.g. via [code navigation on GitHub](https://docs.github.com/en/repositories/working-with-files/using-files/navigating-code-on-github), which makes in-repo tracking of flow much easier, like you'd have in an IDE.
* *All ears if I'm missing something on this!*

Our architecture layers are now moving over to AWS, and becoming more decoupled/microservice-y - sadly, I don't think this will help on this interpretability-of-flow painpoint, as think there are still boundaries between repos which code navigation tools will struggle with.
* *Again happy to be corrected if possible!*

On another approach to avoid this problem: in past we've also done Tech/Science collabs using pipelines, which in principle help separate concerns, letting me be agnostic to architecture layers, and focus on my science layer, debugging by injecting some input data (thought to trigger bug) at the interface to model. Quite powerful, and probably removes ~90% of my need to inspect flow in architecture layers.
But needs some effort to have this sort of pipeline around all models - we've only really done this for one operational one (albeit being done for a lot of incoming ones).
