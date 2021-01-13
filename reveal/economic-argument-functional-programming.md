---
title: Economic Argument for Functional Programming
---

## Economic Argument for Functional Programming

* Michael Snoyman
* VP of Engineering, FP Complete
* LambdaConf 2020 Global Edition
* May 5, 2020

<div style="text-align:center;margin-top:1em">
<div>
<img src="/static/fpcomplete-logo.png" style="border:0;margin:0;margin-right:1em;background:inherit;box-shadow:none">
<img src="https://lambdaconf.us/assets/default/LC-Simple-Logo-LG.png" style="border:0;margin:0;height:94px;background:inherit;box-shadow:none">
</div>
</div>

<aside class="notes" data-markdown>

Good morning, afternoon, and evening to everyone. I'm honored to get the privilege of being the first speaker for LambdaConf's new global edition. I hope everyone has been staying safe and healthy in these interesting times. I know I look forward each year to LambdaConf, and the amazing community that it brings together. I'm very happy that, despite the current global situation, we'll still be able to live out some of the experience.

With that: I promise I will not be bringing up COVID-19 any more, unless it's actually relevant to this talk. Onward!

</aside>

---

## Let's talk about me

* A bit self indulgent
* Background and education is a bit different
* This talk is really based on that difference
* Context here will help

<aside class="notes" data-markdown>

This may seem a little self indulgent, but I want to start off this talk by talking about myself just a bit. My background and education is different enough from many people in the functional programming world that sometimes I will see things radically differently than others. So a little context of where I come from may help explain the prompt for this talk.

</aside>

---

## My background

* Self-taught programmer
* Studied to be an actuary
* Took some math, stats, and lots of econ (too much)
* Advantage: econ teaches you a different way to think
* I still think about the world using those lessons
* Discuss topics at work, or with my kids, using these concepts

<aside class="notes" data-markdown>
Like many people in our community, I learned programming from a book at a young age. I was doing some level of programming from the time I was 8 years old, and was working as a programmer on small jobs before entering university. I've always loved software development. However, it's not what I studied in university, and not what my professional credentials are actually focused in.

For various reasons that I won't get into now, I decided to pursue a career as an actuary. For those who don't know, actuaries focus on risk assessment. I personally worked in casualty insurance pricing, meaning I helped put together models for determining how to price automobile and homeowner's insurance. To skip to the end of the story: due to my programming background, I ended up working on the actuarial tooling team in my first and only actuarial job. We wrote most of our "code," and I mean that with the biggest scare quotes I can muster, in Excel, Access, Visual Basic for Applications, and believe it or not a bunch of Perl scripts. I never trusted these tools to stand up to time, and was constantly seeking something more reliable for writing analysis software. Ultimately, I discovered Haskell and functional programming, I fell in love with them, and decided to make a career shift.

But let's go back to the days before I'd found functional programming. My degree was in actuarial sciences. I don't think the degree was particularly well designed. I took a few applied mathematics courses. I took some really useful statistics and probability courses. But the degree I took included a huge number of economics courses. I say this wasn't well designed, because most of those courses had no bearing on my actuarial studies. I ended up taking six of the actuarial exams before dropping out and becoming a full time developer, and almost none of the information from economics courses appeared on those tests. And furthermore, very little of my day-to-day job involved economics knowledge.

At least, not directly. I think most people in this virtual room will agree that, as a software engineer, we're practiced at thinking differently than many other people. We learn ways to approach problems that involve debugging the issue, testing the limits of a theory, trying to isolate a problem down to its simplest form, and logically step through all pieces of a puzzle. It's a capability that certainly helps us write software, but has carry-over impact to everything else in life.

That's how I feel about economics. I may not regularly need to know the exact details of demand curves, or the difference between average and marginal supply. In fact, it's been so many years since I took those courses that I probably don't remember most of the details correctly. However, there's a way of approaching the world that I learned in studying economics which I continue to pursue today. I regularly use these methods when discussing topics with the rest of the engineering team at work. I'll have conversations with my children using economic concepts as a way of understanding whatever topic is on the table. In other words, I generally like to think of economics not as the science, but as a way of thinking.
</aside>

---

## The question

Question at a previous conference:

> Why is all software slow? Why is all software buggy? Isn't this exactly what functional programming solves? Why is our software today so much worse than software from 30-40 years ago?

<aside class="notes" data-markdown>
I think that's enough background information on me to continue, so thank you for indulging me. Now that you know that I tend to look at a problem differently than others, it's time for a story. I was at another conference a few months ago, and there was a roundtable discussion among the speakers. I wasn't able to participate, but I was able to watch. One of the questions that was brought up was something to the effect of:

> Why is all software slow? Why is all software buggy? Isn't this exactly what functional programming solves? Why is our software today so much worse than software from 30-40 years ago?

My mind immediately went to an economics-based answer to this category of questions. I'll get back to that. Instead, since I wasn't participating in the discussion, I got to see the answers of the other speakers. The answers went in the direction of things like:
</aside>

---

## Technical answers

* Our software today does more than software used to
* We have the wrong abstractions
* People build too many layers of abstraction because they don't understand the lower layers
* Functional programming is relatively recent and hasn't fixed the industry yet

<aside class="notes" data-markdown>
My mind immediately went to an economics-based answer to this category of questions. I'll get back to that. Instead, since I wasn't participating in the discussion, I got to see the answers of the other speakers. The answers went in the direction of things like:

* Our software today does more than software used to
* We have the wrong abstractions
* People build too many layers of abstraction because they don't understand the lower layers
* Functional programming is relatively recent and hasn't fixed the industry yet

It was a good discussion. I don't disagree with any of the points here. I'm sure many of you in the audience are nodding your heads in agreement with these points, and adding a few more.
</aside>

---

## My economics-based answer

> The people making budget decisions in software companies have determined that the marginal revenue to the company is less than the marginal cost of speeding up the software.

---

## Your likely response

* What do those words mean?
* That's stupid, you can't answer "why is software slow" without talking about software!

---

## Goal for today

* You'll understand what that statement means
* You'll agree it's a pretty good root cause analysis
* You'll be better able to advocate for better software going forward

And I hope you like birdhouses

---

## Marginal cost, marginal revenue

Type|Time|Cost|Price
--- | --- | --- | ---
Normal | 1 day | $10 | $75
Golden | 1 day | $100 | $150

Profit: $65 vs $50 _Or_

<table>
<tr>
<th>Marginal cost</th>
<td>$90</td>
</tr>
<tr>
<th>Marginal revenue</th>
<td>$75</td>
</tr>
</table>

```
$65 - $50 == $90 - $75 == $15
```

Yay math!

---

## No gold birdhouses?!?

* Always better to make normal birdhouses
* No one will ever make a gold birdhouse
* I don't want to live in such a world!

Three different cases to analyze

1. Buyer values it more
2. Pride of the maker
3. Neighbors like the birdhouse

What does this have to do with software? Soon

---

## Underpriced goods

* Open marketplace allthingsbirdhouse.com
* Gold birdhouses set at $150
* Alice is willing to spend $500
* Alice is "making" a $350 profit
* No one is selling!
* Bob is willing to make a birdhouse for $200
* Bob makes $100 in real profit, $35 marginal versus normal birdhouse
* Alice still makes $300, market price adjusts

---

## Underpriced software

* Use the "how much would I spend" approach
* Think about software you use daily
* Think about some limitation
* How much would you pay to see it improved?

---

## Pride of the maker

* Bob's birdhouses are a piece of his soul!
* Bob wants to leave a mark on the world
* Can't put a price tag on joy and pride


...Right?

---

## Everything has a price

* Bob makes a normal birdhouse
* Minimum price he'll sell for: $50

> Oh, I'm not putting it in my yard. I'm gonna blow it up!

* No longer willing to sell it for $50
* Soul searching...

---

![Best I can do is $55](/static/econarg/best-i-can-do.jpg)

`$55 - $50 == $5`

I guess Bob's pride and joy is worth $5

---

## How about gold?

* Bob is really proud of his gold birdhouses
* Gold birdhouse for front yard? $120
* Gold birdhouse for explosions? $145
* Pride in a gold birdhouse: $25

Marginal pride in gold: `$25 - $5 == $20`

```
Normal birdhouse:
$75 revenue - $10 material + $5 pride = $70 profit

Gold birdhouse:
$150 revenue - $100 material + $25 pride = $75 profit
```

* Non-monetary compensation

---

## Non-monetary in dev

* You love FP
* How much of a paycut would you take to use it?
* That's how much you value FP
* Not advocating paycuts for FP!
* Want you to think about:
    * How much you like FP
    * Why you value it that much

---

## Externalities

* Alice is willing to spend $25 more for a gold birdhouse
* Actually costs $75 more
* Alice buys a normal birdhouse, done
* 10 neighbors, each prefer gold by $10
* $100 of _positive externality_
* Global decision: buy the gold!
* Actual decision: buy normal
* Alice doesn't take all benefits into account

---

## Tragedy of the commons

* Charlie is making OSS
* 10 companies each benefit $1,000/month
* They _should_ pay $10,000/month
* Game theory: they won't put the money in, get the work for free
* Charlie willing to work for $6,000/month
* Charlie ultimately gets a "real job"
* $4,000 in potential profit is lost

---

## Enough birdhouses!

* Define all value in some standard, measurable unit
* Can compare "ounce of gold" and "pride"
* How much would you spend to solve that problem?
* How much would it take to get you to give up something you like?
* Compare alternatives at the margins
* Maximize `delta benefit - delta cost`
* Accounts for tangible and non-tangible
* Hard to measure these things accurately
* Doesn't account for externalities

<aside class="notes" data-markdown>
There are _many_ big holes in this breakdown. One of them is the fact that measuring the value of everything is all but impossible to do correctly. We do the best we can, but we're going to go into this flaw in a more detail in a bit. The other big flaw we've mentioned is externalities. The person making the decisions only pays attention to benefits and costs that apply to him or her. This is going to be absolutely crucial to understanding how we make functional programming successful in industry, and how we generally try to improve software. Hold onto that thought though, because I want to build up a few other ideas.
</aside>

---

### Bananas

* Let's buy bananas
* Two markets, equal distance, gonna drive
* Look up price, choose cheaper store
* Market A closer than market B
    * Price of gas
    * Value of my time
* Buy apples bananas and pears, more complicated analysis
    * Go only to A
    * Go only to B
    * Go to both, buy cheaper at each

<aside class="notes" data-markdown>
I'm sure everyone's tired of birdhouses. Let's talk about going out to buy groceries instead. For those of you who don't remember: before COVID-19, it was common for people to leave their houses on a fairly regular basis to buy food from things called supermarkets, instead of hoping that delivery trucks would drop food out in front of their houses.

But now, let's say that supermarket A will take 10 minutes to drive to, and supermarket B will take 20 minutes. The bananas will cost $10 at supermarket A, and $5 at supermarket B. Now it's time to look up the going cost of gas. And figure out: how much is 10 minutes of your time worth? OK, that's not too terribly difficult, and you can come to a conclusion fairly quickly.
</aside>

---

## Perfect knowledge

* We don't always have access to all information
* Acquiring information is itself expensive
* Most people _don't_ analyze cost of gas when going to the market
* Gut feeling, which place is cheaper
* It's inefficient...
* But it's logical: making a perfect decision more expensive than an imperfect one
* Adjust analysis behavior for larger shopping trips

---

## Perfect knowledge in software

* Estimates, predictions, risk analysis: all expensive
* Modulate between:
    * Never looking into a language besides PHP
    * Line-by-line analysis of every code dependency
* Engineering skill: how deep do I need to investigate this first?

---

## Software maintenance

* "Functional Programming for the Long Haul"
* We care more about benchmarks and productivity than maintenance
* One reason: gaining knowledge on maintenance is expensive
* We lie to ourselves: then it isn't important!
* Better: be honest
* Acknowledge the unknowns
* Quantify cost of investigation
* Decide if it's worth it

---

## Decisions with imperfect knowledge

* Most important metric: how difficult to maintain software
* All but impossible to assess without writing a real life application
* Therefore, we have to take some guesses at this
* Going to base guesses on less reliable data sources:
    * Marketing material
    * Proof-by-authority claims from leaders
    * Popularity

---

![Extrapolate](/static/econarg/extrapolate.jpg)

---

## FP's flaw

* We're not helping the situation
* We don't write marketing material
* We don't talk about success stories
* We talk about
    * Elegant code
    * More advanced solutions
* For those outside the bubble
    * Limited time to assess FP
    * Compare to Go and Rust
* We need to signal better

<aside class="notes" data-markdown>
Try to put yourself in the shoes of a developer or a manager who isn't a Haskell or Scala aficionado. They have limited time to gather knowledge on "this FP thing." They pull up some articles on Go, and see what a success it is in the DevOps space. They look at Rust's subreddit and see a page full of "look at this weekend project I threw together." They come to the Haskell mailing list and read about effect systems, and dependently typed coding, or to make fun of myself: a bunch of criticisms of monad transformer stacks and async exception caveats.

We believe that functional programming solves real world problems better than the alternatives. But we're not effectively signaling that. And the highly rational breadth-first search most companies and developers will follow to find a language will probably not select FP based on this information.
</aside>

---

## Who's still awake?

* Almost done with the econ lesson
* Three easier topics
* Recap, then bring it home

![Just to keep you awake](/static/econarg/economies-of-scale.png)

<aside class="notes" data-markdown>
If anyone's wondering about the relevance of the comic: there isn't one really, I just like it, and wanted to keep you awake.
</aside>

---

## Risk mitigation

* Pay to play!
* I'll flip a coin
* You get:
    * $2 on heads
    * $0 on tails
* How much will you pay?
* Most people: $1 is fair

---

## Bigger stakes

* Your whole life savings is $10,000
* $20,000 on heads, $0 on tails
* Will you pay $10,000 to play?
* Upside: really nice
* Downside: absolutely catastrophic
* Most people are _risk averse_
* Most companies (especially older ones) are risk averse

---

## Rewrite it in Haskell

* Invest 5 months of dev
* Rewrite entire codebase from PHP to Haskell
* 37% reduction in hardware costs
* 33% reduction in maintenance costs
* 63% improvement in user satisfaction

Easy to weigh cost of 5 months of dev against benefits

Except...

---

## Risk!

* Will it really take 5 months?
* Will the new version actually work?
* Will hardware cost go down 37%?
* Is Haskell more maintainable than PHP?
* Will user satisfaction really go up 63%?
* Getting better idea of risk requires knowledge acquisition

Without knowing Haskell, would you take this risk? I wouldn't

<aside class="notes" data-markdown>
</aside>

---

## Fixed and sunk costs

* COBOL is almost dead, Python is very popular
* Should I spend 5 years learning COBOL for one contract?
* Should I spend 5 years learning Python for 50 contracts?
* Fixed costs need to be amortized (spread out)
* If I already know COBOL, should I be willing to take a contract?
* Yes, it's a _sunk cost_
* Should I _avoid_ learning Python? Absolutely not!

<aside class="notes" data-markdown>
</aside>

---

## Sunk cost fallacy

* Focus on the already-spent sunk costs
* Include them in the analysis, even though you shouldn't
* One reason: humans are emotional, make bad decisions
* Another: justify a decision you made previously to your boss

---

## Decisions with sunk costs

1. Use the language we know, will take 18 months
2. Learn a new language for 6 months, then spend 6 months implementing?

<br>

* Use the new language, obviously!
* But do you believe those estimates?
* And is there institutional objection to ditching a sunk cost?

<aside class="notes" data-markdown>
The point of this is that there is a logical way of approaching these decisions involving fixed costs. But there will be both confounding factors, like emotional involvement or preexisting biases, that will make it difficult to approach this all rationally. And the interaction with other legitimate concerns, like perfect knowledge and risk, makes this even more complicated.
</aside>

---

## Needs versus wants

* There are no needs in economics
* "But I need oxygen!"
* Nah, only if you _want_ to live
* Morbid and uncaring? Yep
* Highly useful
    * All options are on the table
    * All options have a value

<aside class="notes" data-markdown>
I think this was actually the first lesson I ever received in an economics class. I almost forgot to include it in this talk, because it's so fundamental to how I think about things.
</aside>

---

## Uptime

> Our software must have high uptime, at least 99%

* Is that always true?
* What about Proof of Concept to close a $5m deal?
* Everything is a trade-off, everything has a value
* The value is context dependent
* Can be a big disconnect between management and engineering

---

## Final recap

* Compare cost and benefit at margin vs alternatives
* Quantify both tangible and non-tangible items
* Decision maker does not consider externalities
* Acquiring knowledge is expensive
    * It's logical to make imperfect decisions
* Risk aversion: downside more weighty than upside
* Ignore sunk costs!
    * Except people usually don't
* No needs, all wants, can be evaluated

<aside class="notes" data-markdown>
I appreciate all of you humoring me and letting me live out my fantasy of being a stuffy economics professor. Let's do one final recap of the key points before bringing it home.
</aside>

---

## From the top!

Why is software slow?

> The people making budget decisions in software companies have determined that the marginal revenue to the company is less than the marginal cost of speeding up the software.

---

## The CEO's perspective

* I don't use the software, I don't talk to customers
* How much am I spending? How much am I making?
* "I'm so annoyed about slow software!" "So what?"
* Need to talk in real, measurable terms

---

## Measuring slowness

* QA team is slowed down, speeding up will make them 20% more efficient
    * 20% more efficient == $$$ to the CEO
* Sales team estimates 7% of potential customers didn't buy because it's too slow
* Engineers are frustrated, I'm worried about losing good people
    * 3-4 month process to train a new engineer
    * Will delay deliverables
    * Will have both HR and engineering cost to replace

---

## Half the story

* Established concrete benefits
    * Increasing sales
    * Decreasing costs
* What will it cost to speed up the software?
* Be judicious in your recommendations!
* Start with cheapest, least risky, highest benefit items
* Aka highest leverage moves
* Don't throw in the kitchen sink

---

## Example: bump the machines

* Don't say "rewrite the codebase"
    * Raises appropriate warning bells with management
    * It's probably not the best short term solution!
    * Carries massive risk
* Start with: increase size of servers
* Estimate hardware costs, engineering time
* Quantify risks
* Estimate improvements, measure afterwards
* Establish credibility, rinse and repeat

---

## How to fix it?

* Convince decision makers to take speed into account
* Same thing applies to buggy software
* Convince review sites to analyze software quality
    * Unlikely, expensive to get that knowledge
* Convince companies to stop using broken software
    * Unlikely, vendor lock-in
* Legal responsibility for bugs? Maybe

---

## Benefits of FP

* More declarative code
* Immutable data by default
* Explicit effects
* Higher order functions
* Purity
* Combinators
* Mathematical abstractions
* Static type checking
* More fun to write

Can we say that better?

<aside class="notes" data-markdown>
I'm not sure if you've all noticed, but I've done something pretty impressive. I've spoken for however long I've spoken so far without really getting into any concrete benefits of functional programming. There's a reason for that: the concrete benefits aren't important to the higher level economic analysis. A CEO isn't going to care too much about _why_ functional programming saves him or her money. They'll care much more about how much money you're saving them in costs, or making them in revenue. And how much it's going to cost them to get those benefits. And how much risk there is inherent to your plans.
</aside>

---

## More declarative

* Less time spent in code review
* Easier to maintain code

---

## Immutable data by default

* Reduce risk of race conditions
* Reduce risk of business logic errors

---

## Explicit effects/Higher order functions/Purity

* We _think_ it makes code easier to maintain
* Really hard to make those kinds of arguments directly
* Probably not something I'd lead with

---

## Combinators/Mathematical abstractions

* Reusable concepts
* Less time spent learning new concepts for each library
* More consistent interface == reduced bug count

---

## Static type checking

* Remove classes of bugs entirely
    * Don't claim no bugs!
* Reduce overall testing burden
* QA can focus on higher impact bugs
* More maintainable codebases
    * Would really love concrete data to back up that claim!
    * Actually, applies to all the points here

---

## More fun to write

* Probably don't lead with that one either
* But can point out: better staff retention, easier recruiting
    * Some concerns around recruiting pool
    * Highly motivated people in FP
    * Hire remotely!

---

## Acknowledge downsides

* Don't be a zealot (I've been guilty)
* Your audience knows they have imperfect knowledge
* If you hide all defects: they'll know you're lying
* Establish credibility by acknowledging flaws
    * See the book "Presuasion"
* Don't manipulate, be honest!
* Ethical issue
* But also practical: you'll get caught

---

## Example downsides

* Haskell is worse than Kotlin for an Android app
* Many better options than Haskell for front end web
* Nothing garbage collected for real time guarantees
* Many, many more, based on context

---

## Choose your battles

* I believe FP is the best choice for most software
* But we need to acknowledge the downsides
* Save your ammo for solid wins

---

## max(benefit), min(cost)

* Highest benefits, lowest costs, lowest risks
* Don't pitch "Rewrite it in Haskell"
* Small side projects
* Play to strengths of the language
* Minimize impact on the rest of the project/company
* Wait till normal approach has major costs

---

## Example: Haskell microservice

* Not a big fan of microservices...
* But it isolates the risk
* Complicated business logic case
* Easy to test well in Haskell
* Haskell well proven for network services
* Worst case scenario: scrap the whole project
    * As opposed to bring down the company
* Set up measurable objectives
* May have to compare apples to oranges

<aside class="notes" data-markdown>
If you do get the go-ahead to move forward, try to set up some measurable objectives. It's too easy for a successful project to be written off. I remember one case we had at FP Complete where we helped a company do a pilot project in Haskell, to test the waters for moving from C# to Haskell. At the end, they had their two top C# experts review the results to determine if it was something they should consider. The ultimate answer was "nah, we like C#." We had produced results in less time, less lines of code, with less bugs. But the company had set a completely subjective measure of "do our C# developers like it?" It undermined the entire process.
</aside>

---

## Hidden benefits &amp; costs

* Management doesn't ignore these things
* They are _unaware_
* Your job: make them aware
* Put it in terms they will understand and care about
* Communicate clearly
* Clear communication _unlocks the value_ of your analysis
* The truth doesn't speak for itself
* Well structured email, pretty graph, Powerpoint
* Be honest, be accurate, be clear, be persuasive

<aside class="notes" data-markdown>
The founder of FP Complete, and my boss for 7 years, Aaron Contorer, taught me a lot. One of these items is that you can have a feature that unlocks the value of all the other features. Clear communications is one of these things. You can perform all the analysis in the world, and have an absolutely perfect recommendation which will absolutely be golden for your company.
</aside>

---

## Examples of hidden costs &amp; benefits

Do these apply at your company? Can you make the argument for them?

* Request handling latency
* Engineer morale
* Bug rate
* Time to market
* Hardware costs
* Maintainability

---

## Proof by authority

Do you agree with this?

> Java is obviously a great language, because so much software is written in it

* I don't, but there's a grain of truth
* Inferior languages win because of non-technical reasons
* But software shipping in Java is a good proof point

---

## How to be effective

* We don't talk about our successes enough
* Management will want concrete examples of success
* Explaining why it's theoretically better isn't enough
* Need more success blog posts
* Need more articles in popular publications
* Gotten good traction with examples from Fintec
* Facebook's articles have made waves

<aside class="notes" data-markdown>
My request: everyone in this virtual room should start talking more, in public, about the successes they've had with functional programming.
</aside>

---

## Conclusion

* I hope this talk:
    * gave you a fresh look on decision making processes
    * helps you communicate more effectively
    * opens up new ways of thinking

Final word: __empathy__. As you discuss topics of FP, or anything else, be empathetic to the listener. Attune your message to what they care about and will understand.

---

## Thank you

* Thanks to this great audience
* Thanks to the LambdaConf team for restructuring the entire conference
* Thanks to my wife, Miriam, for all the help preparing this talk
* Looking forward to great interactions throughout the year!

---

## Questions?

Oh, shoot, did I lose my connection?
