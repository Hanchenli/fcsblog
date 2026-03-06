---
layout: distill
title: Evaluating Your Evolving Agent Systems at Scale on Frontier-CS
description: "Modern LLMs claim superhuman algorithmic abilities, but what happens when there is no strict verifier? We analyze how multi-turn 'optimization' in Frontier-CS exposes the cognitive ceiling and catastrophic failures of AI in open-ended problem solving."

date: 2026-03-06
date_display: "Mar 6, 2026"
htmlwidgets: true

authors:
  - name: Qiuyang Mang
    url: "https://joyemang33.github.io/"
    affiliations:
      name: University of California, Berkeley
  - name: Qizheng Zhang
    url: "https://alex-q-z.github.io/"
    affiliations:
      name: Stanford University
  - name: Frontier-CS team
    url: "https://frontier-cs.org"

toc:
  - name: The Real-World Evaluation Gap
  - name: Case Study - The Hedgehog Graph
  - name: The Anatomy of the Trap
  - name: The Post-Training Flaw
  - name: Real-World Implications

_styles: >
  d-article img {
    height: auto;
    display: block;
    margin: 1.5rem auto;
    border-radius: 6px;
  }
  d-article p img {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
---
### Evolving Agents Are the Next Frontier for LLMs

Evolving agent systems—including methods based on **continual learning**, **memory evolution**, and **context refinement**—are emerging as a promising path toward agents that improve through experience rather than relying on a fixed policy. This matters especially in discovery-style settings, where the agent must learn from prior failures, accumulate useful knowledge, and adapt its future behavior over long horizons. Recent work such as [GEPA](https://arxiv.org/abs/2507.19457) and [ACE (Agentic Context Evolution)](https://arxiv.org/abs/2601.08747) reflects this trend.

### A Promising Direction, Bottlenecked by Evaluation
However, evaluation has not kept up. Most prior work demonstrates gains on **only ~10 tasks**, often selected case studies or small benchmark subsets. That is a weak test for evolving systems: improvement on three or four tasks does not tell us whether a method can generalize across a broad task distribution, remain stable over many iterations, or handle the kinds of long-horizon, high-difficulty reasoning that make evolution necessary in the first place.

Worse still, many tasks used in prior evolving-agent papers are not expert-crafted and saturate far too quickly. As a result, they fail to measure continued progress in the domain. Circle packing is a telling example: [ThetaEvolve](https://arxiv.org/abs/2511.23473), [TTT-Discover](https://arxiv.org/abs/2601.16175), [AdaEvolve](https://arxiv.org/abs/2602.20133), and [EvoX](https://arxiv.org/abs/2602.23413) all converge to essentially the same value, **2.635983**. Once multiple methods collapse to the same endpoint, the benchmark no longer measures open-ended improvement—it only measures how fast a system reaches saturation.

<div style="text-align: center;">
  <figure>
    <img src="{{ 'assets/img/2026-03-06-agent-evaluation/circle-packing.png' | relative_url }}" style="width: 30%; border-radius: 6px;" alt="Circle Packing" data-zoomable>
    <figcaption style="margin-top: 0.5rem; font-size: 0.9em; font-weight: bold;">Existing LLM evolving work converges to the same best for the circle-packing task.</figcaption>
  </figure>
</div>
