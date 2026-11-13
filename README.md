# Awesome Dreaming

A curated list of research and implementations on AI dreaming, sleep-time compute, and offline memory consolidation for language models and agents.

Dreaming can mean revisiting experience between sessions, consolidating context into model state before cache eviction, or simulating future actions. These sections distinguish those mechanisms from precomputing work for a later query.

## Contents

- [Start here](#start-here)
- [Agent memory consolidation](#agent-memory-consolidation)
- [Model-level sleep](#model-level-sleep)
- [Query precomputation and speculation](#query-precomputation-and-speculation)
- [Imagination and replay](#imagination-and-replay)
- [Evaluation](#evaluation)
- [Contributing](#contributing)

## Start here

- [The components of agent memory](https://www.anthropic.com/research/components-of-agent-memory) (Anthropic research post, 2026) — Introduces Claude's between-session dreaming process. It rereads transcripts to correct memory notes, build representations such as wikis, and choose what to load into future sessions.
- [Dreaming with a dynamic workflow](https://platform.claude.com/cookbook/managed-agents-cma-dreaming-with-a-dynamic-workflow) (Anthropic cookbook) — A worked example of a dreaming workflow with Claude Managed Agents. [Dreams API documentation](https://platform.claude.com/docs/en/managed-agents/dreams)
- [Sleep-time Compute: Beyond Inference Scaling at Test-time](https://arxiv.org/abs/2504.13171) (Lin et al., arXiv preprint, 2025) — Processes shared context before questions arrive and reuses intermediate reasoning across queries. [Letta write-up](https://www.letta.com/blog/sleep-time-compute/) · [Code](https://github.com/letta-ai/sleep-time-compute)

## Agent memory consolidation

- [Auto-Dreamer: Learning Offline Memory Consolidation for Language Agents](https://arxiv.org/abs/2605.20616) (Ye et al., NeurIPS 2026) — A learned consolidator periodically rewrites parts of a memory bank using evidence from multiple sessions. A counterfactual reward favors memories that help later tasks. [Acceptance record](https://cseweb.ucsd.edu/~jmcauley/reviews/neurips26c.pdf#page=2)
- [EVOCHAMBER: Test-Time Co-evolution of Multi-Agent System at Individual, Team, and Population Scales](https://arxiv.org/abs/2605.11136) (Zhang et al., NeurIPS 2026) — Collaborative Dreaming runs between tasks after team failures or disagreements, distilling and routing lessons to agents that need them. [Code](https://github.com/Mercury7353/EvoChamber)
- [LightMem: Lightweight and Efficient Memory-Augmented Generation](https://proceedings.iclr.cc/paper_files/paper/2026/hash/a05b72653ec5b473732129829ae04195-Abstract-Conference.html) (Fang et al., ICLR 2026) — Defers long-term memory updates to a sleep-time phase so related entries can be consolidated off the online inference path. [Code](https://github.com/zjunlp/LightMem)
- [MemCode: Discrete Semantic Representations for Long-Term Agent Memory](https://arxiv.org/abs/2610.19472) (Li et al., NeurIPS 2026) — Separates online writing of atomic facts from asynchronous clustering, consolidation, and archiving.
- [HeLa-Mem: Hebbian Learning and Associative Memory for LLM Agents](https://aclanthology.org/2026.acl-long.625/) (Zhu et al., ACL 2026) — Uses sleep-inspired, threshold-triggered reflection to distill clusters of episodic memories into traceable semantic records. [Code](https://github.com/ReinerBRO/HeLa-Mem)
- [Lightweight LLM Agent Memory with Small Language Models](https://aclanthology.org/2026.acl-long.588/) (Zhang et al., ACL 2026) — Uses small models for online memory operations and a separate offline model to consolidate episodic evidence into long-term semantic memory. This paper also calls its system LightMem.
- [In Prospect and Retrospect: Reflective Memory Management for Long-term Personalized Dialogue Agents](https://aclanthology.org/2025.acl-long.413/) (Tan et al., ACL 2025) — Reflects at the end of each dialogue session to extract and merge memories for future sessions.

## Model-level sleep

- [Do Language Models Need Sleep? Offline Recurrence for Improved Online Inference](https://arxiv.org/abs/2605.26099) (Lee et al., NeurIPS 2026) — Runs multiple recurrent forward passes over each context chunk before cache eviction, carries its fixed-size SSM fast weights to the next chunk, and predicts each answer token in a single pass. [Method and Figure 1](https://arxiv.org/html/2605.26099v3#S5) · [Rule 110 code](https://github.com/sangyun884/llm-sleep/tree/main/rule110)
- [Language Models Need Sleep: Learning to Self-Modify and Consolidate Memories](https://arxiv.org/abs/2606.03979) (Behrouz et al., arXiv preprint, 2026) — Studies continual learning through a separate sleep phase that distills short-term knowledge into long-term parameters and rehearses with self-generated examples.

## Query precomputation and speculation

- [Panini: Continual Learning in Token Space via Structured Memory](https://proceedings.mlr.press/v306/rajesh26a.html) (Rajesh et al., ICML 2026) — Builds an entity-linked question-answer network at write time. Incoming queries traverse the network to assemble relevant reasoning chains. [Code](https://github.com/roychowdhuryresearch/gsw-memory)
- [EverMemOS: A Self-Organizing Memory Operating System for Structured Long-Horizon Reasoning](https://aclanthology.org/2026.acl-long.2125/) (Hu et al., ACL 2026) — Extracts time-bounded foresight signals from dialogue episodes for future retrieval as part of incremental online memory construction.
- [SpecHop: Continuous Speculation for Accelerating Multi-Hop Retrieval Agents](https://arxiv.org/abs/2605.21965) (Saberi et al., NeurIPS 2026) — Speculates on tool observations while requests are in flight, then verifies branches as actual results arrive.
- [Don't Wait to Reply: Towards Responsive yet Thoughtful Dialogue through Proactive Thinking](https://aclanthology.org/2026.findings-emnlp.709/) (Wang et al., EMNLP Findings 2026) — Predicts possible next user replies and precomputes reasoning during gaps between turns.
- [IdleSpec: Exploiting Idle Time via Speculative Planning for LLM Agents](https://arxiv.org/abs/2605.22154) (Choi et al., arXiv preprint, 2026) — Uses tool-wait time to draft plans for both expected outcomes and recovery, then uses the observed result to guide the next step.
- [Anticipate and Learn: Unleashing Idle-Time Compute in Proactive Agents](https://arxiv.org/abs/2605.25971) (Hu et al., arXiv preprint, 2026) — Uses idle time between interactions to anticipate likely needs, gather evidence, and prepare artifacts for future tasks.

## Imagination and replay

- [DreamPhase: Offline Imagination and Uncertainty-Guided Planning for Large-Language-Model Agents](https://iclr.cc/virtual/2026/poster/10011238) (Hamidi et al., ICLR 2026) — Simulates multiple futures in a latent world model before each real action and turns the chosen trajectory into a short reflection for the policy LLM.
- [Modelling the control of offline processing with reinforcement learning](https://proceedings.nips.cc/paper_files/paper/2025/hash/d7e5870810331da5a8ac8bd16d42e074-Abstract-Conference.html) (Spens et al., NeurIPS 2025) — Learns to schedule episodic replay, world-model abstraction, and generative replay during sleep to improve awake performance.
- [Dream to Control: Learning Behaviors by Latent Imagination](https://openreview.net/pdf?id=S1lOTC4tDS) (Hafner et al., ICLR 2020) — Dreamer learns a policy from imagined trajectories generated by a latent dynamics model.
- [Recurrent World Models Facilitate Policy Evolution](https://papers.nips.cc/paper_files/paper/2018/hash/2de5d16682c3c35007e4e92982f1a2ba-Abstract.html) (Ha and Schmidhuber, NeurIPS 2018) — Trains a controller inside a learned world model and transfers it to the original environment.

## Evaluation

- [LoCoMo: Evaluating Very Long-Term Conversational Memory of LLM Agents](https://aclanthology.org/2024.acl-long.747/) (Maharana et al., ACL 2024) — Tests question answering and event recall over long, multi-session dialogues.
- [LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory](https://github.com/xiaowu0162/LongMemEval) (Wu et al., ICLR 2025) — Evaluates information extraction, cross-session reasoning, temporal reasoning, knowledge updates, and abstention.
- [Useful Memories Become Faulty When Continuously Updated by LLMs](https://arxiv.org/abs/2605.12978) (Dylan Zhang, NeurIPS 2026) — Compares batch and streaming memory consolidation and documents how repeated rewrites can erase useful evidence.

## Contributing

Pull requests are welcome. Add the original source, a confirmed venue or publication status, and a one-sentence description of when the extra computation runs and what it produces. Link author-maintained code when available.

List format inspired by [Awesome](https://github.com/sindresorhus/awesome) and [Awesome Memory for Agents](https://github.com/TsinghuaC3I/Awesome-Memory-for-Agents).
