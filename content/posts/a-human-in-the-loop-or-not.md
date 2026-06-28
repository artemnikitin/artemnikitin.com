---
layout: post
title: Do we need to be in the loop?
date: 2026-06-28 09:37:13.000000000 +02:00
---
In my [previous post]({{< relref "the-raise-of-microvms.md" >}}) I mentioned productivity gains from AI. I think this is one of the most interesting topics in our industry right now.

There is a lot of discussion about AI in software engineering nowadays, and it often goes to various extremes. I do not want to go into those extremes here, but I do have one thought that keeps coming back to me.

I think we are in an interesting state today. On one side, AI is clearly helping us move much quicker than before. I am speaking from my own experience, but there is plenty of other evidence around as well. On the other side, we can also see quality going down globally. Just look at the status pages of some services. They look like decorated Christmas trees, and that is not a compliment.

It is hard to argue that AI can produce code much faster than a human can review it. Of course, we can argue about the quality of that code and about many other parameters. But while we are having that discussion, even more code is already being written by AI.

Eventually, every software engineer will have to answer a simple question: **do I want to be in the loop?** For me, this is the key question.

And my opinion is blunt: there is no way to get the full productivity gains from AI while staying in the loop in its traditional sense. It is simply not possible. You cannot demand AI speed and still insist on checking all of its output.

So the only real option is to step outside that loop and let AI do its job. **But!** That does not mean there will be no work left for software engineers.

For me, it was never really about writing code. It was always about achieving something: building a new feature, creating a new piece of infrastructure, making a system work, etc. That part does not change. We are still responsible for delivering value. We are still responsible for making sure that _it actually works_. The difference is that we start abstracting away the act of writing code itself and focus more on engineering practices: making sure there is sufficient test coverage, proper validation, and strong gates on the way to production.

This is exactly how I'm approaching the work on https://github.com/artemnikitin/firework:

- I work together with AI on the design, making sure the major nuances are covered during the design and planning stage.
- AI is fully responsible for implementation. I look at the code sometimes, but I'm not reviewing it in a traditional sense.
- But I am responsible for ensuring that things actually work before changes are merged.

And in my view, this is the future we are moving toward. It's not really a question about being in the loop, but more of a question of which loop you want to be in.

Is it good or bad? We will see when we get there. But I do not think we can keep the old loop and still expect to get the benefits of AI...
