# Why the fuss about serverless?

_Captured: 2017-04-19 at 08:43 from [hackernoon.com](https://hackernoon.com/why-the-fuss-about-serverless-4370b1596da0)_

To explain this, I'm going to have to recap on some old work with a particular focus on co-evolution.

#### **Co-evolution**

Let us take a hike back through time to the 80s/90s. Back in those days, computers were very much a product and the applications we built used architectural practices that were based upon the characteristics of a product, in particular mean time to recovery (MTTR)

When a computer failed, we had to replace or fix it and this would take time. The MTTR was high and architectural practices had emerged to cope with this. We built machines using N+1 (i.e. redundant components such as multiple power supplies). We ran disaster recovery tests to try and ensure our resilience worked. We cared a lot about capacity planning and scaling of single machines (scale up). We cared an awful lot about things that could introduce errors and we had change control procedures designed to prevent this. We usually built test environments to try things out before we were tempted to alter the all important production environment.

But these practices didn't just magically appear overnight, they evolved through trial and error. They started as novel practices, then more dominant but divergent forms emerged until we finally started to get some form of consensus. The techniques converged and good practice was born. Ultimately these were refined and best architectural practice developed. In such confident days, you'd be mocked for not having done proper capacity planning as this was an expected norm.

Our applications needed architectural practices that were based upon (needed) compute which was provided as a product. The architectural norms that became "best practice" were N+1, scale up, disaster recovery, change control and testing environments and these were ultimately derived from the high MTTR of a product. I've shown this evolution of practice in the map below. Normally with maps I just use the description of evolution for activities, it's exactly the same with practice but with slightly different terms e.g. novel, emerging, good and best rather than genesis, custom, product and commodity.

The thing is, compute evolved. As an activity then compute had started back in the 1940s in that uncharted space (the genesis of the act) where everything is uncertain. We then had custom built examples (divergent forms) and then products (convergence around certain characteristics with some differentiation between them). However, compute by the early 2000s had started to transform and become more commodity like with differentiation becoming far more constrained, the activity itself becoming far more defined. In this world a server was really about processor speed, memory, hard disk size, power consumption and how many you could cram in a rack. In this world we built banks of compute and created virtual machines as we needed them. Then we got public utility forms with the arrival of AWS EC2 in 2006.

The more industrialised forms of any activity have different characteristics to early evolving versions. With computing infrastructure then utility forms had similar processing, memory and storage capabilities but they had very low MTTR. When a virtual server went bang, we didn't bother to try and fix it, we didn't order another, we just called an API and within minutes or seconds we had a new one. Long gone were the days that we lovingly named our servers, these were cattle not pets.

This change of characteristics enabled the emergence of a new set of architectural principles based upon a low MTTR. We no longer cared about N+1 and resilience of single machines, as we could recreate them quickly if failure was discovered. We instead designed for failure. We solved scaling by distributing the workload, calling up more machines as we needed them -- we had moved from scale up to scale out. We even reserved that knowing chortle for those who did "capacity planning" in this world of abundance.

_Map -- Emergence of a new practice_

We started testing failure by the constant introduction of error -- we created various forms of chaos monkeys or masters of disasters that introduced random failure into our environments. One off disaster recovery tests were for the weak, we constantly adapted to failure. With a much more flexible environment, we learned to roll back changes more quickly, we became more confident in our approaches and started to use continuous deployment. We frowned at those that held on to the sacred production and less hallowed testing environments. We started to mock them.

These novel practices -- scale out, design for failure, chaos engines and continuous deployment among others -- were derived from an increasingly low MTTR environment and such practices were simply accelerated by utility compute environments. Our applications were built with this in mind. The novel practices spread becoming emergent (different forms of the same principles) and have slowly started to converge with a consensus around good practice. We even gave it a name, DevOps. It is still evolving and it will in turn become best architectural practice.

What happened is known as co-evolution i.e. a practice co-evolves with the activity itself. This is perfectly normal and happens throughout history. Though steel making itself industrialised, we can still produce swords (if we wish) but we have in most part lost the early practice of forging swords. One set of practices has been replaced with another.

I've shown the current state of co-evolution in compute in the map below. The former best architectural practice we now call "legacy" whilst the good (and still evolving) architectural practice is called "devops".

_Map -- Co-evolution of DevOps_

This transformation of practice is also associated with inertia i.e. we become used to the "old" and trusted best practice (which is based upon one set of characteristics) and the "new" practice (based upon a more evolved underlying activity) is less certain, requires learning and investment. Hence we often have inertia to the underlying change due to governance. This was one of the principle causes of inertia to cloud computing.

Furthermore any application we had which were based upon the "old" best practice lacks the benefits of this new more evolved world. These benefits of industrialisation always include efficiency, speed of agility and speed of development in building new things. Our existing applications became our legacy to our past way of doing things. They needed re-architecting but that involves cost and so, we try to magic up ways of having the new world but just like the past. We want all the benefits of volume operations and commodity components but using customised hardware designed just for us! It doesn't work, the Red Queen eventually forces us to adapt. We often fight it for too long though.

This sort of co-evolution and the inevitable dominance of a more evolved practice is highly predictable. We can use it to anticipate new forms of organisations that emerge as well as anticipate the changes in practice before they hit us. It's how back in Canonical in 2008, we knew we had to focus on the emerging DevOps world and to make sure everyone (or as many as possible) that were building in that space were working on Ubuntu. We exploited this change for our own benefits. As one CIO recently told me, one day everyone was talking about RedHat and the next it was all Cloud plus Ubuntu. That didn't happen by accident.

### **Complicating the picture a bit more**

Of course, the map itself doesn't show you the whole picture because I've deliberately simplified it to explain co-evolution. Between the application and the architectural practice we used for computing infrastructure layer is another layer -- the platform.

Now platform itself is evolving. At some point in the past there was the genesis of the first platforms. These then evolved to various divergent but still uncommon custom built forms. Then we had convergence to more product forms. We had things like the LAMP stack (Linux, Apache, MySql and Perl or Python -- pick your poison).

Along with architectural practice around computing infrastructure, there was also architectural practices around the platform. These were based upon the characteristics of the platform itself. From coding standards (i.e. nomenclature) to testing suites to performance testing to object orientated design within monolithic program structures. The key characteristic of the platform was how it provided a common environment to code in and abstracted away many of the underpinnings. But it did so at a cost, that same shared platform.

A program is nothing more than a high level function which often calls many other functions. However, in general we encoded these functions altogether as some monolithic structure. We might separate out a few layers in some form of n-layer design -- a web layer, a back end, a storage system -- but each of these layers tended to have relatively large programs. To cope with load, we often replicated the monoliths across several physical machines.

Within these large program we would break them into smaller functions for manageability but we would less frequently separate these functions onto a different platform stack because of the overhead of all those different platform stacks. You wouldn't want to have machine sitting there with an entire platform stack to run one function which was rarely called. It was a waste! In the map below I've added the platform and the best practice above the platform layer.

_Map -- Evolution of Architectural Practice (platform)_

In 2005, the company I ran was already using utility like infrastructure. We had evolved early DevOps practices -- distributed systems, continuous deployment, design for failure -- and this was just the norm for us. However, we had also produced a utility coding platform, which happened to allow developers to write entire applications, front and back end in a single language -- JavaScript.

As a developer you just wrote code, you were abstracted away from the platform itself, you certainly had no concept of servers. That every function you wrote within your program could be running in a different platform stack was something you didn't need to know. From a developer point of view you just wrote and ran your program and it called other functions. However, this environment (known as Zimki) enabled some remarkable new capabilities from distribution of functions to billing by function. The change of platform from product to utility created new characteristics that enabled new architectural practices to emerge at this level. This is co-evolution. This is normal.

These new practices, I've nicknamed FinDev for the time. The "old" best architectural practices, well, that's legacy. I've drawn a map to show this change.

_Map -- Co-Evolution of Architectural Practice (platform)_

The more mundane of these architectural changes is it encourages componentisation, the breaking down of complex systems into reusable discrete components provided as services to others. In Zimki, every function could be exposed as a web service through a simple "publish" parameter added to the function. Today, we use the term micro services to describe this separation of functions and provision as web services. We're moving away from the monolith program containing all the functions to a world of separated and discrete functions. A utility platform just enables this and abstracts the whole underlying process from the developer.

The next mundane point is it encourages far greater levels of re-use. One of the problems with the old object orientated world was there was no effective communication mechanism to expose what had been built. You'd often find duplication of objects and functions within a single company let alone between companies. Again, exposing as web services encourages this to change. That assumes someone has the sense to build a discovery mechanism such as a service register.

Another, again rather trivial point is it abstracts the developer further away from the issues of underlying infrastructure. It's not really "serverless" but more "I don't care what a server is". As with any process of industrialisation (a shift from product to commodity and utility forms), the benefits are not only efficiency in the underlying components but acceleration in the speed at which I can develop new things. As with any other industrialisation there will be endless rounds of inertia caused by past practice. Expect lots of nashing of teeth over the benefits of customising your infrastructure to your platform and … just roll the clock back to infrastructure as a service in 2007 and you'll hear the same arguments in a slightly different context.

Anyway, back to Old Street (where the company was) and the days of 2005. Using Zimki, I built a small trading platform in a day or so because I was able to re-use so many functions created by others. I didn't have to worry about building a platform and the concept of a server, capacity planning and all that "yak shaving" was far from my mind. The efficiency, speed of agility and speed of development are just a given. However, these changes are not really the exciting parts. The killer, the gotcha is the billing by the function.

Billing by function fundamentally changes how you do monitoring. When I provided a service to the world, users of my program could follow very different paths through it. These we call flows. Depending upon their flow in our system then some functions can be called more frequently. Billing by the function not only enables me to see what is being used but also to quickly identify costly areas of my program. I would often find that one function was causing the majority of the cost because of the way I had coded it. My way of retrieving trades in my program was literally killing me with cost. I could see it, I could quickly direct investment into improving that one costly function and reduce the overall cost. Monitoring by cost of function changes the way we work -- well, it changed me and I'm pretty sure this will impact all of you.

However, this pales into a shadow compared to the next change. This we will call worth based development and to explain it, I need to give you an example and we need to go further back in time.

### **Worth based development**

In 2003, the company that I ran built and operated small sized systems for others. There were no big systems, these were more of the £100k -- £2M scale covering a few million users. Our clients usually wanted to write a detailed specification of exactly what they needed to ensure we delivered. That doesn't sound too bad but even at this small scale then some of the components in these projects would be in the uncharted space requiring exploration and experimentation and hence no-one knew exactly what was wanted. Unfortunately, back then, I didn't have the language to explain this. Hence we built and operated the systems and inevitably we had some tension over change control and arguments over what was in or out of a particular contract.

During one of these discussions, I pointed out to the client that we were sitting around a table arguing over what was in or out of a piece of paper but not one of us was talking about what the users of the system needed. The contract wasn't really the customer here; the client's end users were. We needed to change this discussion and focus on the end user. I suggested that we should create a metric of value based upon the end user, something we could both work towards. The idea fell on deaf ears as the client was pre-occupied with the contract but at least the seed was planted. It wasn't long after this that another project provided an opportunity to test this idea. The client gave me a specification and asked how much would it cost to build a system to do this? I replied -- "How does free sound?"

They were a bit shocked but then I added "However, we will have to be paid to operate the system. We can determine a measure of value or worth and I'll get paid on that". There was a bit of um and ah but eventually we agreed to try out a method of worth based development.

In this case, the goal of the system was to provide leads for an expensive range of large format printers (LFPs). The client wanted more leads. Their potential end users wanted a way of finding out more on these printers along with a way of testing them. I would build something which would marry the two different set of needs. But rather than the client paying up front and taking all the risk, I would build it for free and take a fee on every new lead created. We (as in the client and my company) were no longer focused on what was in or out of a contract but on a single task of creating more leads. We both had an incentive for this. I also had a new incentive for cost effectiveness because the more efficient I made system then the more profit I retained.

With a worth based approach, I have a strong incentive to: -

  * reduce the operational cost of the project because the cheaper it is then the more profit I make.
  * provide reliability because if the system went down, I wasn't making any money.
  * ensure the system maximises the value metric because the more it did, the more money I made.

So, let us map this out

_Map -- the system_

The map begins with our client who has a need for more leads which hopefully leads to other companies buying their product. The conversion from lead to actually purchasing a printer is beyond the scope of this project as that was within the client's sales organisation. We're focused solely on generating leads. The other type of user in this map is the consumer who hopefully will buy one of these expensive printers. They have different needs, they want to find out about the right sort of printer for their commercial operations and to test it before buying something they will use. In this project, we're aiming to provide an online mechanism for the consumer to find out about the printer (a microsite) along with a method to test it (the testing application).

The test is a high resolution image that the potential customer uploads and which is then printed out using the printer of their choice. Their poster (this is large format) would then be distributed to the potential consumer along with a standard graphical poster (showing the full capabilities), relevant marketing brochures and a sales call arranged. Each of the components on the map can expand into more detail if we wish.

From the map, we hope to have visitors to our microsite which will extol the virtue of owning a large format printer and this hopefully persuades some of these visitors to go and test it out. The act of turning a visitor into an actual lead requires the user to test a printer. So we have multiple conversion rates e.g. from microsite to testing application and from visitor to lead. At the start these will be unknown but we can guess.

Normally, operating a microsite requires all those hard to calculate costs of how much compute resource I'm using. Originally, the platform space was a source of headaches due to my inability to provide a variable operational cost for application use. This was 2003 and I had to worry about capacity planning and all that other "yak shaving". However let us revisit this in a modern setting. The platform has evolved towards more of a utility service especially with systems like AWS Lambda. In such a utility platform world, your application is simply a function running on the platform and I'm charged for use. The operational cost of my microsite is basically the number of visitors x the average cost of the microsite function. Remember, an application consists of many functions and users can navigate around it which means some "wandering" users turn out to be more expensive than others. But we can cope with that by taking an average for our microsite.

The same will apply to my "test the printer" (testing) application but in this case the users will include converted visitors from the microsite along with those who directly visit. Every use of the testing application (a function) will incur a cost. But as with the microsite, this is a variable. Of course, the actual functional cost of the testing application could be wildly different from the microsite depending upon what the applications did and how well the code was written but at least we would have a granular price for every call.

When you look at map, there can be many forms of flow within it whether financial or otherwise. It could be flows of users or revenue or flows of risk. For example, if the utility platform dies due to some catastrophic event then it'll impact my microsite and my testing application which will impact the consumer needs and stop any lead generation. This would incur a financial penalty for me in terms of lost revenue. Equally, a user has many paths they could travel, for example they could go to the microsite and never bother to go to the testing application thereby incurring cost but no revenue. Nevertheless, I can take these flows and create a business model from it.

_From a map to the business model_

This is like manna from heaven for someone trying to build a business. Certainly I have the investment in developing the code but with application being a variable operational cost then I can make a money printing machine which grows with users. It also changes my focus on investment -- do I want to invest in increasing marketing for more users, or the conversion rate, or maybe the testing application is so badly written (or a function within it) that investing in coding improvement will bring me better returns? Suddenly, the whole way I build a business and invest is changed.

Let me be clear here. A decade ago, when I looked at a system built on Zimki, I could take a single function and know how much it cost every time it ran. You can now do the same thing using AWS Lambda. Using a map, I could know where that same function (if I wanted that level of granularity) sat in the value chain and how it influenced my revenue. You can also do the same thing, mapping is all creative commons. You can know the influence on revenue and cost of a single function.

Most companies today, when they look at a function see a set of characters for which they have no idea what it costs to run, let alone how it can impact a bottom line. To be brutal, most companies are still struggling with user needs. Most don't think this stuff matters and that'll continue until they face off against a company that thinks it does.

For a bit of comparison, back in the 1990s I used to work in FMCG -- think P&L by crisp packet. Everyone talks about "algorithmic management" these days (well, everyone in certain circles I walk in) but if you don't know the cost of something, its impact on revenue and how it is changing then no algorithm is going to help you magic up the answer to the investment decisions you need to make. Now admittedly, most of my work these days is at industry and even nation state level with the occasional dalliance with companies. But you can, if you wish, analyse a business right down to the function.

The co-evolution of practice around platform from componentisation to code sharing to financial monitoring to increases in agility and efficiency is a pretty big deal as we enter this serverless world. But the new business models around worth based development and the collision of finance and development will literally knock your socks off. Which is why the moniker "FinDev". Beyond the initial investment in coding, I can create an almost variable cost business model and redirect investment to maximise returns in ways that most of you have never experienced. I know, I've been there.

These emerging practices will spread despite the inertia. The path of adoption will be a punctuated equilibrium as with all points of industrialisation. This means the growth is exponential and you won't barely notice it until it gets to a few percent of the market and then in the next few years it will take over. On average the timescale for this process is 10-15 years, so expect to see the whole world being overtaken by serverless by 2025. Yes, we will go through the "[no" -> "oh no" -> "oh f#@k"](https://medium.com/@drew.firment/serverless-and-the-enterprise-69aca8e552cb) phases of adoption. Try not to get disrupted by such highly predictable change claiming no-one saw this coming. We've known for ages. The only plausible excuse is you're too close to retirement and don't want to rock the boat which might be good for you but not for those who come after.

If it helps, serverless is roughly where Infrastructure as a Service (e.g. cloud) was in late 2007. Look around you and how much everything now is "cloud, cloud, cloud" and how difficult it is to hire people with the right skills. Think back to 2007 and how much it was all "this is a toy", "no serious enterprise would use this" and "our data centre is better". Think about all those big name strategy consultants who told you that it wasn't for the enterprise. If you currently have regrets about not moving fast enough back then, just know you're about to make the same mistake again.

These "FinDev" architectural practices will rapidly become good and then best practice but what their exact form will be, we don't know yet. We're not near the stage of reaching consensus and they still have to evolve and refine. But the exact form should become clear in the next five years (by which time the game is almost over, the winners will be emerging etc)

Serverless will fundamentally change how we build business around technology and how you code. Your future looks more like this (simply take the _Co-Evolution of Architectural Practice (platform)_ map and remove the legacy lines).

_Map -- future of development_

You thought devops was big but it's chicken feed compared to this. This is where the action will be, it'll be with you quicker than you realise and yes, you'll have inertia. Now is not the time for building a DevOps team and heading towards IaaS, you've missed that boat. You should be catching this wave as fast as you can.

### A couple of final words.

**Containers** -- they are important but ultimately invisible subsystems and this is not where you should be focused.

**Cloud Foundry** -- it's really important they move up the stack and create that marketplace otherwise AWS Lambda et al will own this space.

**DevOps** -- a lot of what people are trying to build in this space will itself become invisible and if you're building internally then possibly legacy. It's below the line of where you need to be.

One final note, for those using a pioneer -- settler -- town planner structure. If you're providing a platform then your town planners should have taken over this space from the settlers (from platform through devops to infrastructure). Unless you've got scale, you should at the very least be planning to push most of this outside of the organisation with the company focused on building above the platform. I'd hope if you're a regular reader you will be well advanced along the path towards data centre zero.

Your pioneers should be all over the new practices around utility platforms (FaaS, Serverless or whatever you wish to call them). They should be building apps around this space, working out how to combine finance and development into new models, how to build service repositories, monitoring etc. Experiments in this space should be going wild.

Your settlers along with helping the town planners take over any existing efforts from IaaS to PaaS, now need to start hunting through all the novel and emerging practices both internally and externally that will be developing around utility platform efforts. They need to be looking for re-occurring patterns for things that might have some legs and be useful. They need to be looking for those spaces with potential and finding the MVP for your new line of products. Miss this boat and you'll be kicking yourself come 2025.

_Map -- PST_

P.S. For everyone's sake, someone please come up with a better name than serverless. The original Zimki service was described as FaaS (Framework as a service) back in 2006. Unfortunately a bunch of hapless consultants morphed the terminology into PaaS (Platform as a Service) which in many areas has become next to meaningless. This has now has morphed into FaaS (Function as a Service). It's all the same thing, unless you're a consultant or vendor trying to flog your new term as having meaning. It's all about utility platforms where you just code, where billing is as granular as possible (e.g. down to the function) and you don't give two hoots about "yak shaving" (pointless tasks like capacity planning or racking servers etc).

If you want to keep tabs on the development of the field, follow [adrian cockcroft](https://medium.com/@adrianco) also [read his post](https://medium.com/@adrianco/cloud-trends-where-have-we-come-from-and-where-are-we-headed-3d7e5e756d16) along with [Drew Firment](https://medium.com/@drew.firment) ([posts here](https://medium.com/@drew.firment/serverless-and-the-enterprise-69aca8e552cb)) and [Paul Johnston](https://medium.com/@PaulDJohnston) ([here](https://medium.com/@PaulDJohnston/disruptive-serverless-ddb417ebdd15)) et al.

Be warned! The people above are friendly whereas I tend to growl at people especially if they don't have a map of their business … grrr, grrr, big gnashing teeth. Oh, and before someone drools "But McKinsey says", I still haven't stopped laughing from "[Clearing the Air on Cloud Computing"](http://www.isaca.org/Groups/Professional-English/cloud-computing/GroupDocuments/McKinsey_Cloud%20matters.pdf) and that was 2009.

If you don't know what a map is -- [start with chapter 1](https://medium.com/wardleymaps) and can [I suggest reading some basics of strategy](https://medium.com/@swardley/how-to-master-strategy-as-simply-as-i-can-d15627f00326).
