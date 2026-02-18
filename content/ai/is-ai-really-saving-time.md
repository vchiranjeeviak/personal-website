---
title: Are We Really Saving Time with AI?
---

The whole premise of AI is that it saves us a lot of time, leading to better productivity, which in turn leads to more savings or more revenue. Every product pitch, every demo, every LinkedIn post about AI tools carries this underlying promise — do more with less, do it faster, do it better. But is that what's really happening?

As long as we can't completely rely on AI, maybe we aren't saving as much time as we think. Let me elaborate.

## AI in Existing Workflows

One way we can utilise AI in its current state is by incorporating it into our existing flows — writing code, reviewing it, generating architectures, writing boilerplates, and so on. This is probably the most common way developers interact with AI today, whether it's through copilots in their IDE, chat-based assistants, or CLI tools.

But is it really saving time here? If you're making a small code change, or you already know exactly what to change, I don't see the point of using AI — unless you just want to test its capabilities. If you know where the change is required and the change is small, just go there and update it manually. Typing out a prompt, waiting for a response, and then verifying that the output is correct often takes more time than just making the change yourself. There's a certain overhead to using AI that people conveniently ignore.

Where AI starts to make sense is when you're not sure what needs to change, where it needs to change, or when the change is large. Exploring unfamiliar codebases, scaffolding out new features, or figuring out how an API works — these are areas where AI can genuinely help. But even here, there are two problems.

First, when AI makes a change spanning hundreds of lines of code across dozens of files — which is not rare at all, it's pretty common — someone still needs to verify all of it. Are the changes valid? Are they safe to push? Are they introducing new bugs? Are there edge cases the AI didn't think about? That review process takes far more time than people assume. You can't just glance at a diff and approve it. You have to understand the intent behind every change, trace through the logic, and make sure nothing is silently broken. That's real work.

One solution is to lean on CI/CD pipelines with robust test suites that can catch issues in AI-generated code before it reaches production. Have your linters, unit tests, integration tests, and security scans act as automated gatekeepers. On paper, this sounds like the right approach. But if we start relying too heavily on that safety net, we end up increasing both pipeline run times and infrastructure costs. More AI-generated code means more tests to validate it, which means longer feedback loops and higher compute bills. You're trading one problem for another.

And as long as AI tools keep showing disclaimers that their output can't be fully trusted, this verification step isn't optional. It's necessary. The disclaimer is there for a reason — the tool itself is telling you not to blindly trust it.

Second, and this is the more dangerous problem — if the person using AI doesn't have the ability to judge whether what AI is doing is right or wrong, the product is at serious risk. AI doesn't tell you when it's confidently wrong. It presents everything with the same level of certainty whether it's a perfect solution or a subtly broken one. If the person reviewing the output lacks the experience to tell the difference, bad code ships. This is especially true in the dangerous middle ground: someone junior enough to miss subtle mistakes, but senior enough to be trusted with pushing to production. That's where real damage happens — not from obvious failures, but from things that look right and pass a surface-level review.

## AI Agents and Bots

The other way we can incorporate AI is through agents and bots, which have been getting a lot of hype recently. The idea is compelling — instead of just assisting you in a conversation, AI takes actions on your behalf. It reads your codebase, makes decisions, calls tools, and executes tasks end to end. You may think they're awesome, and I can't take away from the fact that they are cool.

But think about it from this perspective. We use Infrastructure as Code tools like Terraform for infrastructure management. Why? Is it because it's fast? No. Managing infrastructure manually through a cloud console is faster, easier, and more intuitive. You can click around, find what you need, and make changes in minutes. Then why do we use tools like Terraform? It is for predictability, reliability, and reproducibility. We want to know that the same configuration applied today will produce the same result tomorrow. We want to version control our infrastructure, review changes before they're applied, and roll back when something goes wrong. We chose a slower, more deliberate tool because those properties matter more than speed.

Now apply that lens to AI agents. We can't just create one agent for one application and another for a different application and hope they work predictably and reliably while talking to each other. There is no guarantee that an agent will behave the same way twice given the same input. The non-deterministic nature of LLMs means that today's perfect execution could be tomorrow's production incident.

If you want AI to behave predictably, you still need well-defined APIs for them to interact with — and even then, reliability depends on the LLM's ability to call the right API, with the right parameters, correctly, every single time. One hallucinated parameter, one misunderstood context, and you have a problem that's much harder to debug than a bug you wrote yourself — because at least with your own bugs, you understand the thought process that led to them.

## So, Are We Saving Time?

I'm not saying AI is useless. It's a powerful tool when used in the right context and by the right people. But the narrative that it's a universal time-saver is misleading. For small, well-understood tasks, it adds overhead. For large tasks, it shifts the work from writing to reviewing — which is better, but not the dramatic improvement that's being sold. And for agents, we're nowhere near the predictability and reliability we need to trust them with anything critical.

The real question isn't whether AI can do the work. It's whether the time we spend verifying, correcting, and babysitting AI is actually less than the time we'd spend just doing it ourselves.