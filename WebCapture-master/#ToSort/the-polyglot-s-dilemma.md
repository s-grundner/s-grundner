# The Polyglot's Dilemma

_Captured: 2017-04-14 at 16:42 from [dzone.com](https://dzone.com/articles/the-polyglots-dilemma-daedtech)_

[See how three solutions work together](https://dzone.com/go?i=204124&u=https%3A%2F%2Fad.doubleclick.net%2Fddm%2Ftrackclk%2FN6040.130331DZONE%2FB11226848.150123399%3Bdc_trk_aid%3D321096583%3Bdc_trk_cid%3D81552442%3Bdc_lat%3D%3Bdc_rdid%3D%3Btag_for_child_directed_treatment%3D) to help your teams have the tools they need to [deliver quality software quickly](https://dzone.com/go?i=204124&u=https%3A%2F%2Fad.doubleclick.net%2Fddm%2Ftrackclk%2FN6040.130331DZONE%2FB11226848.150123399%3Bdc_trk_aid%3D321096583%3Bdc_trk_cid%3D81552442%3Bdc_lat%3D%3Bdc_rdid%3D%3Btag_for_child_directed_treatment%3D). Brought to you in partnership with [CA Technologies](https://dzone.com/go?i=204124&u=https%3A%2F%2Fad.doubleclick.net%2Fddm%2Ftrackclk%2FN6040.130331DZONE%2FB11226848.150123399%3Bdc_trk_aid%3D321096583%3Bdc_trk_cid%3D81552442%3Bdc_lat%3D%3Bdc_rdid%3D%3Btag_for_child_directed_treatment%3D).

Few things seem as institutional to the programming world as [what I call the experience tuple.](http://www.daedtech.com/avoiding-the-dreaded-experience-tuples/) A company needs to hire someone to automate something, so, naturally, it asks the software development group to make alphabet soup for [dice.com](http://www.dice.com/). "We need someone with (C#, XML, HTML, JS, ASP, MVC, REST, Angular, AJAX) with (React, MSTest, Moq, CSS) as a plus." Presumably, then, [polyglot](https://blog.lelonek.me/be-a-polyglot-programmer-6e7423916ed8) applicants stand a better chance. But I'd argue that they also face something I'll call the polyglot's dilemma.

Hold on to your hats, programmers, because this will get counter-intuitive before it makes sense. With that in mind, where to start?

## Problem Solvers and Problem Transformers

Well, perhaps categorizing hired software developers as problems makes for a good start. I don't mean problems in a negative sense, but rather in the same vein as puzzles. A business hires software developers for some broader purpose. Maybe they work on internal automation that reduces operating expenses. Or perhaps they produce software sold as a good or service and add to top line revenue.

In either case, the business implicitly says, "I need help increasing our profitability." And you show up saying the following:

> I have (8, 10, 10, 4, 6, 3, 1, 1, 0) years of (C#, XML, HTML, JS, ASP, MVC, REST, Angular, AJAX). Now while the rest of you figure out how to make use of me, I'll be over here sharpening the saw with some code katas.

Whenever I've had management responsibility, I've subconsciously put people into two buckets. Problem solvers take a problem I have and make it go away. Problem transformers take a problem I have and solve it by bringing me the next problem (I'm omitting non-performers who don't solve problems at all as beyond the scope of this post).

For instance, take the problem of a malfunctioning production server. A problem solver would go off and come back with a functioning production server, somehow. A problem transformer would come back, report that the problem was caused by a faulty power supply and ask what I wanted to do about that new problem.

As programmers, we behave as problem transformers. We present ourselves and our skill sets as problems in need of management solutions.

## Solving the Programmer Problem (Surface Version)

Alright, so let's say that a programmer dutifully applies to an open position with a resume full of experience tuples. And let's also say that this results in a hire and an accepted offer. That programmer can't simply wander in and become useful by starting to write logging libraries. Something else has to happen.

In corporate parlance, this programmer enters as a non-capitalized resource. And, yes, I use the term _resource_ deliberately here, in spite of the dehumanizing connotation. In fact, that's kinda the point. Like a file cabinet or a data entry contractor, that's the role we play when we enter an enterprise without any pretense of participating in said enterprise's strategy.

Entering this way, we require two flavors of management in order to do anything useful. Someone has to understand the intersection of tech and business strategy, and someone has to understand the intersection of tech and the organization's domain. Usually, some combination of management flavors handles this: program managers, product managers, line managers, project managers, etc. Sometimes an architect enters the fray as well.

Thus the enterprise divides itself. Programmers bring the experience tuples. Others bring a strategic understanding of why those experience tuples matter to anyone. And those others then solve the programmer problem.

## Solving the Programmer Problem (Realpolitik Version)

Let's take a different look now. Recall [my definition of the corporate hierarchy](http://www.daedtech.com/defining-the-corporate-hierarchy/) and also [my definition of the journeyman idealist](http://www.daedtech.com/journeyman-idealist-architect-programmer-paycuts/). I elaborate extensively on these concepts in _[Developer Hegemony](http://developerhegemony.com), _but the definitions in the posts should suffice.

Inbound developers generally enter as pragmatists or journeyman idealists. Both archetypes occupy the bottom of the corporate pyramid and both report to (mostly) idealists in management. The actual stack ranking among the line level folks matters only to the line level folks. They play stack ranking games with no actual organizational stakes in the grand scheme of things.

The idealists report to upper management, which consists entirely of opportunists. The opportunists, the organization's real strategic players, manage everyone. Since they have relatively few direct reports, they manage the organization indirectly, using narrative and culture. And so, in the context of zero-sum pyramid organizations, they create a culture that feeds a narrative advantageous to the organization.

To put it more bluntly and tangibly, they get idealists (journeyman and regular) to believe that the company's interests mirror their own. And they get them to force that culture on pragmatists who don't buy it but don't fight it. The opportunists thus solve the programmer problem by creating a culture of maximizing the programmer's value to the organization while caring not at all for the programmer's market value or external prospects (an entirely rational thing to do, I might add).

## Solving the Programmer Problem (Applied Version)

For the sake of simplicity, picture a custom app dev shop. You see these either operating as so-called "consultancies" that build custom websites or else you see them within extremely large organizations, acting as internal agencies. In either case, these organizations tend toward relatively flat pyramids and they sell margin on human labor. This makes their political currents relatively straightforward.

Let's say that I start just such a shop. I take a business plan and some letters of intent to a bank, secure a business loan and get some web developers on the payroll. We do .NET, PHP, Ruby, or Java. Bob's your uncle. Then I go and sell accordingly to organizations in need of web apps.

If I hire you to have you on the payroll indefinitely, I have a vested interest in you having skills a mile wide and an inch deep. I can gloss over the lack of depth during sales, but I can't work with the lack of breadth. If clients want us to augment their Ruby development organization's staff, I can't send them the foremost experts in a specific set of .NET technologies. But I can send them relatively mediocre Ruby folks and collect margin without getting sued.

So what do I do? Well, I seek to create a culture that places a high degree of value on generalizing. I create a culture that values polyglots with experience tuples. And I capitalize on hired programmers by deploying them interchangeably to as wide a client base as possible. These programmers serve the company well, and I reward them with standard corporate COLAs and the occasional raise and "senior" added to their previous titles.

## The Journeyman Idealist Culture Conduit

As a mechanism for creating this culture, I rely heavily on journeyman idealists, specifically. In the programming world, programmers tend to look up to them, be they pragmatist or journeyman idealist. So the key to manufacturing favorable culture lies in aligning journeyman idealist values with the company's values. This can prove harder than it sounds since journeyman idealists tend to value "the craft" more than the company.

But in the case of generalizing and experience tuples, these interests align nicely. You see, learning many programming languages and techs fluently -- becoming a polyglot -- _makes you a better programmer_. And the journeyman idealist values this first and foremost. So, if I run an agency, I enlist the journeyman idealists to sell experience tuple breadth as a virtue to all of the organization's programmers. Don't learn a new language or two because I can sell your labor more easily. Do it because it's really in your own best interests!

Now, in our line of work, I actually don't need to sell this particularly hard. Journeyman idealists flow freely among organizations and cross-pollinate these concepts. As a result, we have an entire industry that operates under the wrongheaded assumptions that programming skill translates directly to profit and that breadth across domain and tech makes for a good career strategy. Or, I should say, we have an industry of pragmatists and journeyman idealists that operate under this assumption. Opportunists know better.

## Generalist Culture in Action

Watch [this video by John Sonmez](https://simpleprogrammer.com/2015/04/23/im-not-sure-i-want-to-be-a-specialist/). I went out looking for other voices to add to my own about the career merits of specialization. John certainly agrees. But I stumbled on this video, and it presents an absolutely perfect concretion of what I've talked about so far.

In it, a reader writes to John saying, in effect, "I like to generalize." He then cites his company's apparent motto as the motivation for his own take: "we specialize in not specializing." That represents _exactly_ the sort of thing that an opportunist translates from "this makes it easier to sell your labor" to "we have high-minded cultural principles that we ask all of our highly esteemed software engineers to live up to."

That slogan practically drips with opportunist indirect management. In our industry, we've been perversely encouraged to hold in the highest esteem the very approach that makes our labor and ourselves fungible commodities. To put that in plainer terms, if we identify ourselves by the languages we use and we all strive to learn all of those languages, we become completely interchangeable. And nothing suits my agency better than an army of interchangeable coders. I can easily mix and match them, and I can also easily replace them.

When we aspire to generalizing as a key plank of professionalism, we maximize how a company can deploy us. In other words, we make ourselves a textbook problem for strategic opportunists to solve.

## The Polyglot's Dilemma

So let me now come full circle to talk about the polyglot's dilemma. In the current world of software development, learning multiple languages and notching more and more techs makes for good business. But it makes for good business in a perpetual subordinate, journeyman idealist context. Generalizing, for the individual programmer, is a locally maximizing activity (and, I would argue, a [tragedy of the commons situation](https://en.wikipedia.org/wiki/Tragedy_of_the_commons) for the industry, but that's a topic for another day).

As you examine your own career prospects, you face the polyglot's dilemma. On the one hand, broadening and deepening your experience tuples means more interviews, more offers, and marginally better job situations. It ensures that you remain relevant, sharp, and gainfully employed. In our industry, it ensures high demand for your services.

But on the other hand, it ensures high demand for your services as a low-level resource and bit organizational player. It ensures a permanent spot as a pawn and not a player in every game you enter. And that's because generalizing over the years and across the technologies isn't _strategic_. You've never figured out how to solve anyone's actual business problems -- you've only figured out how to make yourself a perpetually sharp saw for others to use.

## The Case for Specialization, but Only if You Do it Right

I understand Xander from John's video when it comes to specialization. His thinking (I assume) goes something like, "I can get jobs if I introduce myself as a C# programmer, but not if I introduce myself as a C# programmer specializing in C# 6.0, specializing in Linq extension methods. I want to remain a generalist."

I see this misalignment of "specialist" definition a lot. Forget about languages and frameworks. Seriously. C# or some subset thereof is not a specialty. Recall my differentiation between problem solvers and problem transformers. Specializing in technologies makes you a problem transformer. You need to _solve_ problems.

For Developer Hegemony, I interviewed a woman named [Sally Lehman](https://twitter.com/SllyLhmn). She caught my eye as an interesting person both due to an ability to secure work at non-traditional organizations and also as someone who managed to carve out a niche entirely within a corporate context. She had three different full-time roles that oriented around a specialization in email delivery, including one with Github.

Sally understood how to _solve _problems rather than transform them. She has a legitimate specialty. "I help organizations with email." Whether she chooses to maintain that, augment it, or even abandon it at some point, she nevertheless has it.

If someone from a company for which Sally very much wants to work bumps into her in an elevator, she can explain in a sentence or two how she could make a real impact. Could you? Or would you just start talking about how many "years of XML" you have?

## Getting off of the Treadmill

Why does this matter? Why does it prove advantageous?

If you've been at this a while, what I say here will really resonate. You can easily think of your programming career as one of adding more and more language/framework/methodology/etc. gunk to your resume, the way you collect Stack Overflow points and badges. But, unlike Stack Overflow, the stuff you've done before expires. For instance, I have a good bit of VB6, VBA, and some Perl under my belt. But those techs increase my current marketability not a whit.

You can't model our language learning as a walk forward. You have to think of it as walking in the wrong direction against a treadmill as the landscape changes and makes our old knowledge archaic. And if you measure your marketability and value to a company in terms of the techs you currently know, you'll spend a career running the wrong way on a treadmill to keep up. If you get stuck somewhere doing a Pascal project for 4 years, you might come up for air at the end only to find yourself unemployable.

But now imagine that you, like Sally, acquire a specific expertise. Now you can sell yourself on the sorts of problems that you can solve for organizations instead of selling yourself on how easily they can deploy you as a fungible resource. Of course, you need to learn new things to keep up with your specialty. But _you_ control that learning and position yourself as an expert, instead of trying in exasperation to explain to some HR employee that you'll have no problem picking up C# since you've spent a lot of years in Java and C++.

## What's the Takeaway

I always seem to generate the longest posts when I talk about office politics and techie careers. Today presents no exception, and I feel acutely aware that I should wrap it up. But I want to do so with a tangible takeaway.

I'm not disparaging companies or opportunists for encouraging a culture that makes developers swappable. That's just good business sense, and it mainly happens subconsciously. I'm also not disparaging developers for complicity in this scheme. It's just the way business is done, so it wouldn't occur to most people to contemplate an alternative.

But now that you see an alternative (I hope), start to contemplate it. I encourage you to stop notching languages and frameworks as part of a Sisyphean spring against the motion of the treadmill. Instead, take a critical look at what your company has you doing, and start trying to think in terms of the business problems you solve for them instead of the languages that you know.

From there, extrapolate to defining a career narrative wherein you're the expert in solving some specific problem, like Sally. This won't pigeonhole you because you need not always lead with it. But it will make you expert in an area and give you a framework for solving, rather than transforming problems. Experts have an easier time getting both contract and full-time gigs, and they can also move fluidly into consultative or managerial roles. Do this, and you'll create many more career options for yourself, and you will escape the polyglot's dilemma.

Discover how TDM Is Essential To [Achieving Quality At Speed For Agile, DevOps, And Continuous Delivery](https://dzone.com/go?i=204125&u=https%3A%2F%2Fad.doubleclick.net%2Fddm%2Ftrackclk%2FN6040.130331DZONE%2FB11226848.150413345%3Bdc_trk_aid%3D321095198%3Bdc_trk_cid%3D81552443%3Bdc_lat%3D%3Bdc_rdid%3D%3Btag_for_child_directed_treatment%3D). Brought to you in partnership with [CA Technologies](https://dzone.com/go?i=204125&u=https%3A%2F%2Fad.doubleclick.net%2Fddm%2Ftrackclk%2FN6040.130331DZONE%2FB11226848.150413345%3Bdc_trk_aid%3D321095198%3Bdc_trk_cid%3D81552443%3Bdc_lat%3D%3Bdc_rdid%3D%3Btag_for_child_directed_treatment%3D).
