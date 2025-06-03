---
layout: post
title:  "Catching the wagon on AI tooling"
date:   2024-07-05 22:15:00 -0500
categories: IDE, AI
---
![Dragon](/assets/images/wagon-catching.png)

# Why I am writing this
Over the last 12 months or so, I feel like there is a widening divide between AI believers and non-AI believers. Interestingly a lot of people have not changed their mind all this time even though a lot has changed. My goal is not to convince anyone. I mostly want to help folks that already feel it have a path towards not falling behind.


# What AI tooling was
First of all I have been eyeing the AI editors + models progress almost since its inception. I have tried to integrate them into my workflow mostly because I if I know something can be automated, there is no way in hell I am going to do that manually.

When editors like Cursor came out, they were pure hype ( not going to sugarcoat this ). I also despised the idea of someone forking VSCode and adding some fluff on top without any real value.

At the time it was okay enough to try to ask the editor something and you would get something other than junk 30% of the time. The usage was only in `ask` mode. It was basically having chatgpt window in your editor.

# What AI tooling is today
I think we have finally hit a point that AI can do very useful things with proper guidance. AI editors got iterated over and at the same time models got much much better.With the inception of MCP, for the first time, There is almost always a prompt path that you can give the model and it would be able to create something very accurate and very good.

The interesting thing about this process is that it didn't really happen overnight. Some folks are naturally better working with AI (so they saw it coming a few months ago) and some are better when they rely on themselves. 

Previously if you did a poor job of prompting Cursor to create a module or function for you, it would go about and create enough hassle that you would possibly opt to do it yourself. It would happen enough times that made the value of using it not that much.

Now you can pinpoint the editor + model to do exactly what you want. You can tell it to search the exact documentation you need and respect the exact rules you want it to follow. It won't get it right 100% of the time but it is actually quite close. It can automate a very large portion of your job description.

# Getting Started
It is finally a new era of being able to work smarter. AI tooling can help you perform so much better at your job by letting you focus on what matters the most.

Here is what I am urging you to do if you have not already:

- Install Cursor. Let it edit things that you already know how to do and watch it work. Don't cheap out on the models . Use the best ones (Claude and Gemini) as much as you can.
- Use agent mode exclusively. If you want to ask something, ask it to write it to an .md file
- Add an MCP server. Github is an easy one. Then add a few global rules on how to use it. For starters let it try addressing your colleague's PR comments.
- revisit the rules when it does something stupid you don't like. Maybe it tries editing comments when it was not asked to or it tried refactoring.

Here is some things I use it the most for:
- Smart grepping: if you are not sure where something is or how it is implemented -> just ask it . MCP servers are the best here since they give you ability to search across your org's codebase
- inline editing: If you want to change an implementation somewhere, just mark it and `CMD + K` . AI works best when there is a foundation already.
- I keep a `notes` repository and use it to reference my thoughts when I want it to do something. I basically create a `.md` file and put down my thoughts for a task and then reference it when I want to implement something
- If AI does a good job of explaining something to me that I didn't know, I keep that as an .md file as well and reference it when I want to explain it back to it. I will ask it to refine it to my liking first. Remember: AI tools don't have a good memory but you do.

# Final Notes
This is an important point in time for the history of software development. I don't think AI is still good enough to replace humans entirely. I also don't believe in vibe-coding. But AI tooling today is good enough to help you in your job in a very meaningful way and the goal of this article was to show you that. I hope I gave you enough reason to go and finally try using AI editors with proper models.