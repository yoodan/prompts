
Best things you can do to improve agentic coding:
- Have a couple "pointer" files, reference files of how to ideally do a thing in the codebase.


# Prompting 101

> Why get good at prompting? 

Prompt engineering is a valued skill now and will only increase to become so. Being able to extract the most out of the LLM in an accurate manner can increase productivity.

> How to test prompts?

Create a test prompt against cases and refine the prompt against the test prompt that you already know the answer to.

> How can I make the AI less confident in its answer so I can be aware of any gaps that might be missing?

Within the response output, mention "you should be able to state whether or not you can fully confidently determine about X or if the human adjuster needs to follow up for more information."

> How to organize information in your prompts?

**Disorganized prompts are hard for Claude to comprehend.**

You should use delimiters like XML tags to organize information or section titles and headers.

XML is preferable as it's clear and token efficient.

> Why do you have to tell Claude to be a certain role?

Based on what you ask, it will assume a certain role. Instead of leaving some information to assumptions, just straight up tell it what its job is for a certain task.

> How do you prevent hallucinations?

- Have Claude say "I don't know" if it doesn't know or if it doesn't have a high confidence score.
- Tell Claude to answer only if it is very confident in its response.
- Have Claude *think* before answering.
	- This forces it to check its output and verify its own work.
- Ask Claude to find relevant quotes from long documents then answer using the exact quotes

> When prompting normally, how can you get it in the exact form that you want?

Use prefilled responses. 
So prefill a response, then write in text for the "assistant" field / role. This will have it continue where it left off.

So if you add "itenerary"<> tag asking it for an itenerary, it knows to fill that in the output.

---

### Prompting for Agents

> What are the skills of prompt engineering?

- Clear, unambiguous, precise writing.
- Creating evals with scientific mindset, testing constantly.
- Product thinking, what is the ideal model behavior for your product?
- Understanding the LLMs, their tendencies, and limitations.
- Aggregating and analyzing failure modes + thinking of ways to fix it 
- Thinking of edge cases and ways to make the prompt robust to a wide range of inputs


> It's hard to make meaningful progress on a prompt without an eval. How can you test your system to know if it's improving?

First, start with a small eval. If you have a large agent or a large task, you actually don't need many tests to verify that it's better than before.

The more specific the agent or task gets, the more eval you need as the changes become more meaningful and impact is higher.

Just get started with evals first, keep it small. 

Use realistic tasks. Don't just give a coding agent competitive programming problems. Give it real world problems in the context of where it's used in.

Use rubrics. LLM-as-judge with a rubric is very powerful. LLMs are strong enough to be judges of outputs **only if they are given a clear rubric** aligned with human judgements.

**Nothing is a perfect replacement for human evals.** Nothing will beat vibe checking the system with real users.

> What are examples of evals?

1. Answer accuracy.
Given a prompt, check the answer of the agent against a rubric.

e.g. How many employees started in 2023 and are still active?
Agent: 47 started in 2023 and are still active.
Eval LLM Judge: Evaluation - CORRECT. Accurately reported the total count.

2. Tool use accuracy.
e.g. Book a flight to Paris tomorrow morning
Agent: search_flights(destination=Paris, date=tomorrow)
{errors out and fails}
Agent: Let me try that again. search_flights(destination=Paris, date=2024-05-19...)
{succeeds}

Eval LLM Judge: Pass. Recovered from its own parameter error.

3. T-bench (evaluates whether agent reaches correct final state)
User: Change Flight
Agent: Gives response that cannot be changed, but it can be cancelled. 
User: okay just cancel it.
Agent: Cancels reservation.

LLM Judge: Pass. It ended with the cancellation. Cancel Status = true.

> Last Notes

Ordering matters in LLM prompts. They prioritize information at the beginning and information at the end. They place less emphasis on stuff in the middle.


