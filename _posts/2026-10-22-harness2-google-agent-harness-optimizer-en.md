---
layout: post
title: "Google's Harness²: Can It Fix Your Agent Harness for You? What's Verified and What Isn't"
lang: en
ref: harness2-google-agent-harness-optimizer
date: 2026-10-22
permalink: /en/harness2-google-agent-harness-optimizer/
---

Harness² is an open-source framework from Google Research. It leaves the model alone and edits the harness around it: the system prompt, memory, tools and skills. The headline gain of "up to 11.5 points" is a maximum from one setup, not what you should expect on your own agent. We have not installed or run it, so everything below comes from the paper, the repository and public discussion.

{% include stat.html value="11.5 points" label="Largest gain reported on WorkBuddy-Bench (GLM-5 with OpenCode, one improvement step). It is a maximum, not an average." source="Harness² paper, arXiv 2610.14224" url="https://arxiv.org/abs/2610.14224" date="Oct 22, 2026" %}

> **Verdict:** Worth a cheap look if you run an agent harness and can spare a small API budget. Do not plan around the 11.5. Start with the free demo, then one small run, and stop if the gain is within noise or the cost passes your cap.
{: .v-verdict}

## What is Harness², in one paragraph?

It is a research framework, released under Apache 2.0, for agents that meet tasks nobody designed the harness for. The README describes two loops. In the first, for each task, it proposes edits to the harness, probes what they change, and composes a better harness from the contrast. The paper calls this a Propose-Probe-Compose step. In the second, it keeps a persistent "improvement harness" and stores adopted harnesses and evidence-supported lessons from each task, so later tasks start smarter.

The README lists eight editable parts around the model: system prompt, guardrails, memory, tool guidance, subagents, skills, scripts and plugins. The repository (google-research/harness2) says it is "not an officially supported Google product." It was created on Oct 6, 2026, and its last push was Oct 14, 2026 (GitHub API, checked Oct 22, 2026).

Sources: [repository](https://github.com/google-research/harness2), [paper](https://arxiv.org/abs/2610.14224), both checked Oct 22, 2026.

## What do "up to +11.5, +4.5, +11.8" actually mean?

They are three best cases, reported on three benchmarks, and they use different units. The abstract says a single step improved GLM-5 and Gemini 3.5 Flash over their base harnesses, "across three professional benchmarks and four model-harness configurations." Here is what we could confirm from the paper's text on Oct 22, 2026:

| Benchmark | Largest gain | Unit | Configuration |
|---|---|---|---|
| WorkBuddy-Bench | 11.5 | points | GLM-5 with OpenCode, one step (confirmed in the paper text) |
| JobBench | 4.5 | points | not confirmed by us |
| LAB | 11.8 | percentage points, partial pass rate | not confirmed by us |

Source: [arXiv 2610.14224](https://arxiv.org/abs/2610.14224), text read Oct 22, 2026. One sentence in the paper gives the JobBench and LAB figures together ("gains reach 4.5 points and 11.8 percentage points in Partial pass rate, respectively"). Our reads of the paper disagreed on which model and harness produced them. One explainer, [i-scoop](https://www.i-scoop.eu/harness2-google/), attributes 11.8 to GLM-5 with OpenCode. We treat that as a secondary claim. We also did not read the full result tables.

The paper also says more recursion helps. In its words, parallel task-level recursion at k=5 "adds a further 2.9 to 3.9 points on WorkBuddy-Bench." The main results use k=1.

Two things follow. Both are our reading, not the authors'.

**Our read:** the three numbers do not add up to "Harness² adds 11 points." Each is a best result in a different setup, and 11.5 and 11.8 use different units. A safe prior for your own harness is somewhere between zero and 11.5. The authors also tested only two executor models, GLM-5 and Gemini 3.5 Flash.

**Our read:** the model being improved is not the model doing the improving. According to the repository, the default editing model is Claude Opus 4.8. The setup docs say the tool "supports either Vertex Claude or Gemini as the improver." So you pay for a strong editor model on top of your executor model. That matters for cost.

## Is it a big deal or old news?

Both, depending on what you count. The attention is real. The repository had 17,179 stars and 1,593 forks on Oct 22, 2026 (GitHub API). The explainer site i-scoop listed 4,740 stars on Oct 18, 2026 ([i-scoop](https://www.i-scoop.eu/harness2-google/)). Those two numbers come from different sources, so treat the jump as rough, not an exact like-for-like count.

{% include stat.html value="17,179" label="GitHub stars for google-research/harness2 on the check date. A different site listed 4,740 on Oct 18, so the sources differ." source="GitHub API" url="https://github.com/google-research/harness2" date="Oct 22, 2026" %}

The engineering crowd was cooler. The Hacker News thread had 79 points and 19 comments on Oct 22, 2026 ([thread](https://news.ycombinator.com/item?id=50151059)). The complaints fall into three groups:

- No runnable example. One commenter wanted "a single end to end example you can actually run."
- Marketing feel. Another called the overview video "just an animated slideshow of benchmarks," and a couple of people objected to AI-generated images in the README.
- Not new. One commenter asked whether this is just "Learn from past runs to update your skills and system prompt etc?", which many agent builders already do by hand.

**Our read:** both sides are partly right. Feeding lessons back into prompts and skills is familiar to anyone who has hand-tuned a harness. What the paper adds is a structured, test-based way to do it, plus measured gains on benchmarks. Whether that beats your own hand edits is the open question, and nobody outside the authors has answered it yet.

## What does it cost to run?

The official answer is short: it costs whatever your model calls cost. The README says "Model-backed runs incur API costs; start with a small task selection." The experiments doc says the same about executor rollouts and improvement stages, and recommends reviewing model pricing before a full run.

We found no price list or rollout count in the official docs. One third-party post says the number of executor rollouts scales with k, with about 4 runs at k=1 and 20 at k=5. We could not find that in the repository docs, so treat it as a secondary-source claim ([wavect](https://wavect.io/blog/google-harness2-setup-cost-safety.md), also repeated by i-scoop, Oct 22, 2026). We are not converting anything to dollars, because the real price depends on your executor, your editor model and your task count.

What the docs do give you are two cost controls:

- `--dry-run` previews which tasks and domains would be selected, with no model calls.
- `--max-tasks` caps tasks per domain. The full LAB task stream is 1,143 tasks, so this flag matters.

**Our read:** if run counts grow with k as those posts say, going from k=1 to k=5 multiplies your bill by about five for a further gain the paper describes as a few points (2.9 to 3.9 on WorkBuddy-Bench). Start at k=1 and pay for more only if you see a gain.

## Is it safe to run?

Read the warnings before you point it at anything real. The README states: "Executor network access is unrestricted, and Codex runs with its sandbox disabled." It also lists Linux, Python 3.12 and uv as requirements.

The README adds a second warning about benchmarks: "Public benchmark rubrics may be accessible online. Before evaluation, configure network restrictions to prevent access to benchmark answers and grading criteria." In plain terms, an agent with open internet could look up the answers. The paper says its own pipeline never shows the rubric to the executor, the editor or the selector. That protects the authors' benchmark runs. It does not protect yours.

If you run it, use a throwaway machine or container with no credentials you care about, and no access to private repos. This is our advice, not the authors'. (README checked Oct 22, 2026.)

## How should a solo builder try it?

The demo is the first step. The README says `harness2-demo --output runs/demo --k 2` runs with "no model credentials." That answers the HN complaint about missing examples at no cost, though we have not run it ourselves, so we can't say what you will see.

A sequence we would follow:

1. Run the demo with no keys. Look at what an edited harness looks like.
2. Use `--dry-run` on your own tasks to see the scope.
3. Run one small batch at k=1 with `--max-tasks` set low. Write down the model spend.
4. Compare against your current harness on the same tasks.
5. Stop if the gain is within the run-to-run noise you already see, or if spend passes the cap you set before starting.

You choose the cap. Make it a number before you launch, not after.

The links: [repository](https://github.com/google-research/harness2), [paper](https://arxiv.org/abs/2610.14224). The repository you want is google-research/harness2. Other repositories with similar names, such as harness2-redteam, harness2-rs and harness2_tutorial, are separate projects.

We will fix anything here that turns out to be wrong and note the change. Star counts and discussion numbers move daily, so the figures above are accurate only as of the dates shown.
