---
layout: post
title:  "Living in an Extrapolated World"
date:   2026-07-20 22:00:00 -0400
categories: AI, SRE, Infra, Development
---
![Where Reality Lives](/assets/images/extrapolation.png)

# The Extrapolated Reality
The programming world looks better.

We are all better at coding now. Pull requests rarely have typos. They are mostly structurally right. Stupid mistakes are rarely made (unless you lack some needed tooling to catch those).

Most code reviews are now about whether you even need a feature or whether the formulation you had in mind even makes sense.

We are all shipping code faster. Writing design docs faster. Documenting all incidents and failure modes and options and what can go wrong all very fast. 

Our AI tools are getting better and better. Our jobs on the other hand is getting harder and harder everyday. Not because implementations are hard (That was never an issue really). It's something more subtle.

Categorically speaking. Humans are all about "What is True". We care about whether ideas actually work in practice because at the end of the day we are the ones being held accountable for them. We and people around us and sometimes the people of world have to deal with the consequences. The stakes can really be high.

AI models are all about "What could be true". They will mingle the context we provide for them with baseline. They search the knowledge they can and they put it together and they draw conclusions out of them. They work based on those conclusions towards the targets we have decided for them. 

AI models fundamentally are not designed to produce something that is true. They are designed to produce things that "make sense" and there is a very important difference between the two for us humans. 

In a way AI models extrapolate reality to meet some end. Most of the time that extrapolation is good enough. Sometimes it is not but the effects of this is much larger than it initially looks.

# The Environment We All Live in 
Let's say you are diagnosing a niche production issue in an environment you don't know. Maybe it is a service you deployed for a customer and getting prod access is hard or simply you don't know enough about their stack or their code.

In the old world, Someone would describe the problem because they see the symptoms themselves and then they went ahead and did some observations. They drew some conclusions on what they think is happening and they gave it to you.

You would then go ahead and form some hypothesis and then run some experiments to try and find which one is true. You would find a result that would be convincing enough to point the exact problem. Going to the solution could be the easy part of the story sometimes.

But let's run the same scenario today. Someone sees a symptom somewhere. They ask their AI agent why that might happen. They form some opinions based on that and then they give the results back to the team. A lot of time that person doesn't bother with actual observations and those are replaced by extrapolation of the original problem. Now you have "Would could be wrong" instead of "What is wrong"

Then someone on your team runs their agent to run their procedures against those extrapolated issue. They will form some extrapolated solution based on that context and then they try to implement a solution on top of that. 

The results are basically very different. Either we hit the jackpot and the issue is resolved OR we are now working with people with their minds set on false primitives. You as a person that actually solves the problem would need to do extra work to bring back people to factory settings. To guide them through the actual observations (try to dig them out) and then guide them again through step by step analysis rooted in reality. That's a lot more work!


![Context Transformed](/assets/images/context-transformed.png)

# What we can do about our future
If you are lucky like me and have smart colleagues to work with, you can all rely on the shared due diligence to make progress. Basically hold each other accountable as much as possible.

I think the most important skill nowadays is being critical of everything in your head and a bit of paranoia. In the past you could rely on people's expertise and judgment and build on top of that but those lines are becoming more and more murky. People are getting their hands dirty in domains they never touched before. The horizon has expanded by a lot and so has our attention.

The best way to operate is just questioning everything. Go to start and start reasoning. Use AI for research but treat it like that friend that sometimes gets too excited with their stories in the parties.

Find out if that method of authentication actually works the way it is described. Find the exact documentation that talks about this. Cross-Check AI's research with another model. Go through it yourself and find out if it makes sense logically.

Hopefully that way we can tie the outcomes to the reality and we can all leverage all the speedups that LLMs bring for us. The good parts!
