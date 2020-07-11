---
layout: post
title: Software Rot Causes
categories: [blogs]
tags: [miscellaneous]
---

Software rot is Entropy, what the hell is it and what is the link with softwares development you say ? Entropy is the notion that on a long enough time scale everything gets messy and disorganized until it completely disappears. Software and software systems are not an exception, in fact, I would say they are pretty much proof.

![The symbol of entropy]({{ site.baseurl }}/images/entropy.jpg "the scientific symbol for entropy")

Anybody who’s worked within a poorly conceived and maintained codebase can attest to that, it’s a big ball of mud, an inscrutable system where any attempt at deciphering what it does and why and how it was implemented that way are the cause of soul-crushing insanity which have the potential to earn you a trip to the asylum.

A rotten codebase or system is often like a jenga tower where one small seemingly simple change can have a massive ripple effect where it causes bugs and defects on things that should have been separate. It can also be interlocked systems that should not be and have very opaque and indirect relationships like all Elon Musk’s romantic relationships.

So why does a codebase or a system rots? The causes are many and this post will delve into what causes software to decay.

<br/>

<hr/>
<br/>

#### Feature creep

![Too much features]({{ site.baseurl }}/images/swiss_army_knife.jpg "I'm confused")
More features is always a good thing right ? Well no, it can really be the opposite especially when the new features are poorly thought out and rushed to production without any good idea with how to measure its usage and success. It can often lead to over design and complication and start to confuse the users more than it can deliver values to them. It can also start to push the dev teams to rush the delivery of features and hack them all together which produces a cobbled together codebase over time. In fact, one of the purposes of the agile methodology was to quickly gather feedback about what brings value to the software users quickly in order to help the dev teams to know on what to put the real effort and quickly discard what does not bring enough value to users.

<br/>

<hr/>
<br/>

#### Lack of good developers with relevant experience

![Average tech recruiter job offering]({{ site.baseurl }}/images/fullstackdev.jpg "Average tech recruiter job offering")
There’s a big shortage of developers in the world right now. Experienced developers are rarer and can be expensive. So in order to save money big institutions and small startup tend to hire junior developer and put them in a role where more experience is required, for instance maintain mission critical legacy system that the experienced devs they have on board don’t want to touch because it’s already too old, so a junior dev comes in with this very hard task to do well and since he’s inexperienced he unwillingly contribute to the rot.

For a startup it can also be hiring junior devs to code and do the architecture for a whole system and app, which is a daunting task even of an experienced developer, so of course the code gets messy gradually and the craps just continue to pile up. Also because hiring practices for software developers can be a very hit and miss process, sometimes hr people hires devs with good experience in a given field and puts them in a completely different field thinking that the developer will be able to transition easily. Sometimes the developer has a big ego and underestimates the difficulty of transitioning from a field to another, like a frontend dev switching to backend or a mobile developer jumping into full-stack web development. So developers can transition from a field to another but usually the code they write during the transition time has the potential of not being very good and too often it will still be pushed to production because of the business deadline to meet.

<br/>

<hr/>
<br/>

#### No time planned and allowed for refactoring or addressing technical debt

![Average it project states after years in production]({{ site.baseurl }}/images/technicaldebt.png "Average it project states after years in production")
Everybody sucks when they start at something, it’s just how it is. Research shows it takes on average [10 000 hours of practices](https://medium.com/skilluped/will-10-000-hours-of-practice-make-you-world-class-152bbad64078){:target="\_blank"} before being really good at something. The technology is ever changing so developers are often starting from scratch on new frameworks, technologies or practices and as stated above everybody sucks when starting at something, so you can see the problem there. So codebases are rarely optimal, there's always ways to better it on top of constant technological updates.

But those ways to make the code better or more up to date, it never really brings new business values immediately so it’s often relegated to a vague and unplanned latter...which often comes when the rot has set in and is huge and discouraging to start to attack. It’s like when you push to later your visits to the dentist or maintenance or your house, it starts to pile up and form a debt that eventually must be paid. This phenomenon is known as the [broken window theory](https://medium.com/@matryer/broken-windows-theory-why-code-quality-and-simplistic-design-are-non-negotiable-e37f8ce23dab){:target="\_blank"}, i.e. things looking simple and well organized are easier to maintain in this state because there’s not the discouraging cost to spend effort to fix the mess in the first place.

<br/>

<hr/>
<br/>

#### Constantly changing and contradicting change request with impossible deadline aka dysfunctional business practices

You can have the best software development team in the world and still get mediocre results when a project is poorly managed. If the environnement is chaotic, the deadlines are pulled out of a hat and must absolutely be respected and the scope is ever changing then a lot of shortcuts will be taken to respect the deadline and it will be at the cost of quality. Then sometimes management will have the [false good idea](https://en.wikipedia.org/wiki/Brooks%27s_law){:target="\_blank"} to add people to a late project by thinking it will help the team to deliver more rapidly even though it has already been proven that it will have the adverse effect because the people have to ramp up and by doing solicits times from the other developer and add an overhead coast of thinking about dividing the work.

So people have less time and rush even more and so management starts to think about adding more people and the vicious cycle continues.
As you understand, rushed coding almost never results in easily maintainable code, it often results in a big ball of mud and the rot is already started. Useful documentation and specifications are discarded as well. So when in the future it’s time to make changes it’s opaque again how the software is working. Quality assurance can get neglected too so the software gets shipped with a lot of bugs and since the code was rushed and is not easy to understand there's a good change that fixes will introduce even more bugs.

<br/>

<hr/>
<br/>

To conclude, for the reasons I’ve stated above I think that a lot of codebase start with manageable issues and the problems start to pile up over time until it’s really hard to correct the situation or it starts poorly and goes down from there. In my next post I'll cover how to try to slow down entropy and reverse it even.
