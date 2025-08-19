_(Courtney Nash’s [excellent post](http://programming.oreilly.com/2013/08/automation-myths.html "Automation Myths") on this topic inadvertently pushed me to finally finish this – give it a read)_

In the [last post](http://www.kitchensoap.com/2012/09/21/a-mature-role-for-automation-part-i/ "A Mature Role for Automation Part I") on this topic, I hoped to lay the foundation for what a mature role for automation might look like in web operations, and bring considerations to the decision-making process involved with considering automation as part of a design. Like Richard mentioned in his excellent [comment](http://www.kitchensoap.com/2012/09/21/a-mature-role-for-automation-part-i/#comment-8887 "comment") to that post, this is essentially a very high level overview about the past 30 years of research into the effects, benefits, and ironies of automation.

I also hoped in that post to challenge people to investigate their assumptions about automation.

Namely:

*   _when_ will automation be appropriate,
*   _what_ problems could it help solve, and
*   _how_ should it be designed in order to **augment and compliment** (not simply replace) human adaptive and processing capacities.

The last point is what I’d like to explore further here. Dr. Cook also pointed out that I had skipped over entirely the concept of _task allocation_ as an approach that didn’t end up as intended. I’m planning on exploring that a bit in this post.

But first: what is responsible for the impulse to automate that can grab us so strongly as engineers?

Is it simply the disgust we feel when we find (often in hindsight) a human-driven process that made a mistake (maybe one that contributed to an outage) that is presumed impossible for a machine to make?

It turns out that there are a number of automation ‘philosophies’, some of which you might recognize as familiar.

Philosophies and Approaches
---------------------------

### One: The Left-Over Principle

One common way to think of automation is to gather up all of the tasks, and sort them into things that can be automated, and things that can’t be. Even the godfather of Human Factors, [Alphonse Chapanis](http://www-personal.umich.edu/~danhorn/chapanis.html "Alphonse Chapanis") said that it was reasonable to “mechanize everything that can be mechanized” ([here](http://www.amazon.com/Human-Factors-Systems-Engineering-Management/dp/0471137820 "Human Factors in Systems Engineering")). The main idea here is efficiency. Functions that cannot be assigned to machines are left for humans to carry out. This is known as the _‘Left-Over’ Principle_.

David Woods and Erik Hollnagel has a response to this early incarnation of the “automate all the things!” approach, in [Joint Cognitive Systems: Foundations of Cognitive Systems Engineering](http://books.google.com/books/about/Joint_Cognitive_Systems.html?id=CzaG96osYSMC "Joint Cognitive Systems: Foundations of Cognitive Systems Engineering"), which is (emphasis mine):

> “The proviso of this argument is, however, that we should mechanise everything that can be mechanised, only in the sense that it can be _guaranteed_ that the automation or mechanisation always will work correctly and not suddenly require operator intervention or support. Full automation should therefore be attempted only when it is possible to anticipate every possible condition and contingency. Such cases are unfortunately few and far between, and the available empirical evidence may lead to doubts whether they exist at all.
> 
> Without the proviso, the left-over principle implies a rather cavalier view of humans since it fails to include any explicit assumptions about their capabilities or limitations — other than the sanguine hope that the humans in the system are capable of doing what must be done. Implicitly this means that humans are treated as extremely flexible and powerful machines, which at any time far _surpass_ what technological artefacts can do. Since the determination of what is left over reflects what **technology cannot do** rather than what **people can do**, the inevitable result is that humans are faced with two sets of tasks. One set comprises tasks that are either too infrequent or too expensive to automate. This will often include trivial tasks such as loading material onto a conveyor belt, sweeping the floor, or assembling products in small batches, i.e., tasks where the cost of automation is higher than the benefit. The other set comprises tasks that are too complex, too rare or too irregular to automate. This may include tasks that designers are unable to analyse or even imagine. Needless to say that may easily leave the human operator in an unenviable position.”

So to reiterate, the Left-Over Principle basically says that the things that are “left over” after automating as much as you can are either:

1.  Too “simple” to automate (economically, the benefit of automating isn’t worth the expense of automating it) because the operation is too infrequent, OR
2.  Too “difficult” to automate; the operation is too rare or irregular, and too complex to automate.

One critique of the Left-Over Principle is what Bainbridge points to in her second irony that I mentioned in the last post. The tasks that are “left over” after trying to automate all the things that can are the ones that you _can’t figure out how to automate effectively_ (because they are too complicated or infrequent therefore not worth it) you then give back to the human to deal with.

So hold on: I thought we were trying to make humans lives _easier_, not more difficult?

Giving all of the easy bits to the machine and the difficult bits to the human also has a side affect of amplifying the workload on humans in terms of cognitive load and vigilance. (It turns out that it’s relatively trivial to write code that can do a boatload of complex things quite fast.) There’s usually little consideration given to whether or not the human could effectively perform these remaining non-automated tasks in a way that will benefit the overall system, _including_ the automated tasks.

This approach also assumes that the tasks that are now automated can be done in isolation of the tasks that can’t be, which is almost never the case. When only humans are working on tasks, even with other humans, they can stride at their own rate individually or as a group. When humans and computers work together, the pace is set by the automated part, so the human needs to keep up with the computer. This underscores the importance automation in the context of humans and computers working _jointly_. Together. As a team, if you will.

We’ll revisit this idea later, but the idea that automation should place high priority and focus on the human-machine collaboration instead of their individual capacities is a main theme in the area of Joint Cognitive Systems, and one that I personally agree with.

[![The Left-Over Principle](https://github.com/jallspaw/ironies/blob/main/LeftOverPrinciple-Hollnagel.png?raw=true "The Left-Over Principle")](http://www.kitchensoap.com/2013/08/20/a-mature-role-for-automation-part-ii/leftoverprinciple-hollnagel-2/)

[Parasuraman, Sheridan, and Wickens (2000)](http://archlab.gmu.edu/people/rparasur/Documents/ParasSherWick2000.pdf "A Model for Types and Levels of Human Interaction with Automation") had this to say about the Left-Over Principle (emphasis mine):

> “This approach therefore defines the human operator’s roles and responsibilities in terms of the automation. Designers automate every subsystem that leads to an economic benefit for that subsystem and leave the operator to manage the rest. Technical capability or low cost are valid reasons for automation, **given that there is no detrimental impact on human performance in the resulting whole system**, but this is not always the case. The sum of subsystem optimizations does not typically lead to whole system optimization.”

### Two: The “Compensatory” Principle

Another familiar approach (or justification) for automating processes rests on the idea that you should exploit the strengths of both humans and machines differently. The basic premise is: give the machines the tasks that they are good at, and the humans the things that they are good at.

This is called the _Compensatory Principle,_ based on the idea that humans and machines can compensate for each others’ weaknesses. It’s also known as _functional allocation, task allocation, comparison allocation_, or the MABA-MABA (“Men Are Better At-Machines Are Better At”) approach.

Historically, functional allocation has been most embodied by “Fitts’ List”, which comes from a report in 1951, “[Human Engineering For An Effective Air Navigation and Traffic-Control System](http://oai.dtic.mil/oai/oai?verb=getRecord&metadataPrefix=html&identifier=ADB815893 "\" Human engineering for an effective air navigation and traffic-control system\"")” written by Paul Fitts and others.

Fitts’ List, which is essentially the original MABA-MABA list, juxtaposes human with machine capabilities to be used as a guide in automation design to help decided _who_ (humans or machine) does _what_.

Here is Fitts’ List:

> **Humans** appear to surpass present-day machines with respect to the following:
> 
> *   Ability to detect small amounts of visual or acoustic energy.
> *   Ability to perceive patterns of light or sound.
> *   Ability to improvise and use flexible procedures.
> *   Ability to store very large amounts of information for long periods and to recall relevant facts at the appropriate time.
> *   Ability to reason _inductively_.
> *   Ability to exercise judgment.
> 
> Modern-day **machines** (_then, in the 1950s)_ appear to surpass humans with respect to the following:

> *   Ability to respond quickly to control signals and to apply great forces smoothly and precisely.
> *   Ability to perform repetitive, routine tasks
> *   Ability to store information briefly and then to erase it completely
> *   Ability to reason _deductively_, including computational ability
> *   Ability to handle highly complex operations, i.e., to do many different things at once

This approach is intuitive for a number of reasons. It at least recognizes that when it comes to a certain category of tasks, humans are much superior to computers and software.

Erik Hollnagel summarized the Fitts’ List in _[Human Factors for Engineers:](http://www.amazon.com/Human-Factors-Engineers-Control-Sandom/dp/0863413293 "Human factors for engineers")_

[![Summary of the Fitts List](https://github.com/jallspaw/ironies/blob/main/FittsListPrinciples.png?raw=true)](https://github.com/jallspaw/ironies/blob/main/FittsListPrinciples.png?raw=true)

It does a good job of looking like a _guide_; it’s essentially an IF-THEN conditional on **where** to use automation.

So what’s not to like about this approach?

While this is a reasonable way to look at the situation, it does have some difficulties that have been explored which makes it basically impossible as a practical rationale.

### Criticisms of the Compensatory Principle

There are a number of strong criticisms to this approach or argument for putting in place automation. One argument that I agree with most is that the work we do in engineering are never as decomposable as list would imply. You can’t simply say “I have a lot of data analysis to do over huge amounts of data, so I’ll let the computer do that part, because that’s what it’s good at. Then it can present me the results and I can make judgements over them.” for many (if not all) of the work we do.

The systems we build have enough complexity in them that we can’t simply put tasks into these boxes or categories, because then the cost of moving between them becomes extremely high. So high that the MABA-MABA approach, as it stands, is pretty useless as a design guide. The world we’ve built around ourselves simply doesn’t exist neatly into these buckets; we move dynamically between judging and processing and calculating and reasoning and filtering and improvising.

Hollnagel unpacks it more eloquently in [Joint Cognitive Systems: Foundations of Cognitive Systems Engineering](http://books.google.com/books/about/Joint_Cognitive_Systems.html?id=V-mcFVvrgwYC "Joint Cognitive Systems: Foundations in Cognitive Systems Engineering"):

> “The compensatory approach requires that the situation characteristics can be described adequately a priori, and that the variability of human (and technological) capabilities will be minimal and perfectly predictable.”
> 
> “Yet function allocation cannot be achieved simply by substituting human functions by technology, nor vice versa, because of fundamental differences between how humans and machines function and because functions depend on each other in ways that are more complex than a mechanical decomposition can account for. Since humans and machines do not merely interact but act together, automation design should be based on principles of coagency.”

David Woods refers to Norbert’s Contrast (from Norbert Weiner’s 1950 _[The Human Use of Human Beings](https://en.wikipedia.org/wiki/The_Human_Use_of_Human_Beings "The Human Use of Human Beings"))_

> _**Norbert’s Contrast**_
> 
> _Artificial agents are literal minded and disconnected from the world, while human agents are context sensitive and have a stake in outcomes._

With this perspective, we can see how computers and humans aren’t necessarily decomposable into the work simply based on what they do well.

Maybe, just maybe: there’s hope in a third approach? If we were to imagine humans and machines as _partners?_ How might we view the relationship between humans and computers through a different lens of cooperation?

That’s for the next post. 🙂

