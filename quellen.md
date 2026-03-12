# Literature Sources: Workflows vs. Agents / Node-Level Hybrid Design

> Updated: 2026-03-09 | v3 focus: node-level orchestration, hybrid systems, NADF | Session 2: Q01/Q02/Q03/Q05/Q06/Q07/Q08/Q09/Q13/Q27/Q28/Q29/Q30/Q31/Q32/Q33/Q35/Q36/Q37/Q42/Q43/Q44/Q47/Q52 enriched with verified test setups, key numbers, explicit "does NOT do" notes | All exposé-cited papers verified ✅; author corrections: Q31, Q43; Q49/Q50/Q51/Q52 new entries added | Q52 Webster & Watson (2002) added as IS literature review methodology reference
> Original: 2026-03-04 | Search queries: LLM agents workflows, agentic AI systems, autonomous AI agents benchmark, AI workflow automation LLM

---

## NEW IN V3

### [Q47] Zheng, L. et al. (2023). Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena.
- **Authors:** Lianmin Zheng, Wei-Lin Chiang, Ying Sheng et al. (UC Berkeley / LMSYS)
- **Year:** 2023
- **Type:** P (NeurIPS 2023)
- **URL:** https://arxiv.org/abs/2306.05685
- **Relevance:** 5/5
- **Verification status:** ✅ Key numbers verified (2026-03-09)
- **What was tested:** Two evaluation frameworks: (1) MT-Bench — 80 challenging multi-turn questions across 8 categories (writing, roleplay, extraction, reasoning, math, coding, knowledge, STEM), judged pairwise by GPT-4. (2) Chatbot Arena — crowdsourced blind pairwise comparison platform with 30,000+ human votes across multiple LLMs.
- **How it was tested:** Human expert annotators vs. GPT-4 judge on the same pairwise comparisons. Agreement rate measured by counting matches between human verdict and GPT-4 verdict. Ties excluded from agreement rate calculation (important nuance).
- **Key Findings (verified):**
  - GPT-4 as judge achieves >80% agreement with human raters overall (abstract summary)
  - Pairwise MT-Bench comparisons: 85% agreement when ties are excluded
  - Three identified judge biases: (1) position bias (favors first response), (2) verbosity bias (favors longer responses), (3) self-enhancement bias (favors outputs from same model family)
  - Mitigation: randomize response order, use reference answers, multiple independent judge calls
  - Fleiss' kappa used to quantify inter-rater reliability between human raters themselves (~0.45 on average — moderate)
- **Precise citation note:** "over 80% agreement" is the abstract-level summary. The precise figure on pairwise MT-Bench is 85% (ties excluded). Do not cite as "85% agreement" without the caveat.
- **Core Thesis Relevance:** Methodological foundation for the OQS evaluation protocol (Phase 4 and Phase 6). The >80% threshold is the calibration target. Thesis requires Fleiss' κ ≥ 0.70 between the LLM judge and human raters on 30% of outputs before deploying the judge for the remaining 70%. Mitigations from this paper (order randomization, reference anchors) should be implemented in the evaluation protocol.

### [Q48] OMG (2013). Business Process Model and Notation (BPMN) Version 2.0.2. *(REMOVED FROM V3 — BPMN framing dropped)*
- **Authors:** Object Management Group
- **Year:** 2013 (current standard)
- **Type:** B (Industry Standard)
- **URL:** https://www.omg.org/spec/BPMN/2.0.2/
- **Relevance:** 4/5
- **Abstract:** The formal specification of BPMN, the dominant standard for process modeling in enterprise contexts. Defines task types (service task, user task, business rule task, script task, manual task), gateway types, and event types with precise execution semantics.
- **Key Contributions:**
  - Formal taxonomy of process task types with execution semantics
  - Standard vocabulary connecting practitioner process design to this thesis's node archetypes
  - Grounds the node archetype taxonomy in an established, practitioner-recognized framework
- **Core Thesis Relevance:** Theoretical grounding for the node archetype taxonomy (Table 2). Enables practitioners to apply the NADF directly to existing BPMN process models.

---

## Legend
- **Relevance Score**: 1 (low) – 5 (high) for the thesis topic "Workflows vs. Agents"
- **Type**: P = Peer-reviewed Paper, B = Blog/Technical Report, F = Framework/Software, S = Survey

---

## TIER 1 – Core Papers (Relevance: 5/5)

---

### [Q01] Schluntz, E. & Zhang, B. (2024). Building Effective Agents.
- **Authors:** Erik Schluntz, Barry Zhang (Anthropic)
- **Year:** December 19, 2024
- **Type:** B (Anthropic Technical Blog / Research Report — NOT peer-reviewed, no empirical data)
- **URL:** https://www.anthropic.com/research/building-effective-agents
- **Relevance:** 5/5
- **Verification status:** ✅ Content verified (2026-03-09)
- **What this is:** Practitioner-authored engineering blog post by Anthropic engineers. Not peer-reviewed. No experiments, no benchmarks, no quantitative validation. Pure definitional and design-principle content.
- **Core Definitions (cite-ready):**
  - Workflow: "systems where LLMs and tools are orchestrated through predefined code paths"
  - Agent: systems where "LLMs dynamically direct their own processes and tool usage"
  - Augmented LLM: base building block combining an LLM with retrieval, tools, and memory
- **Five Workflow Patterns (named, with use-case guidance):**
  1. Prompt chaining — linear multi-step pipelines with defined handoffs
  2. Routing — classifies input, dispatches to specialized subflows
  3. Parallelization — concurrent execution of independent subtasks, result aggregation
  4. Orchestrator-workers — dynamic task decomposition by a coordinator LLM
  5. Evaluator-optimizer — generation loop with explicit quality feedback and revision
- **Design Principles stated (qualitative):**
  - Start simple; add agentic complexity only where demonstrably necessary
  - Prefer workflows for well-defined, repeatable tasks
  - Prefer agents for tasks requiring judgment, exception handling, or open-ended search
  - Tool documentation quality matters more than model size for tool-use accuracy
- **What the paper does NOT do:** No empirical comparison between paradigms. No quantitative performance data. All recommendations are heuristic, based on engineering experience at Anthropic.
- **Core Thesis Relevance:** Primary definitional source for the workflow/agent distinction (cite for definitions). The five workflow patterns map directly to the SDT and OIG archetypes. Use only for definitions and qualitative design principles, never for quantitative claims.

---

### [Q02] Wang, L., Ma, C., Feng, X., et al. (2023). A Survey on Large Language Model based Autonomous Agents.
- **Authors:** Lei Wang, Chen Ma, Xueyang Feng, Zeyu Zhang, Hao Yang, Jingsen Zhang, Zhiyuan Chen, Jiakai Tang, Xu Chen, Yankai Lin, Wayne Xin Zhao, Zhewei Wei, Ji-Rong Wen (Gaoling School of Artificial Intelligence, Renmin University of China)
- **Year:** 2023 (arXiv August 2023; published Frontiers of Computer Science, 2025)
- **Type:** S (Survey — peer-reviewed journal publication, Frontiers of Computer Science, Springer)
- **arXiv:** 2308.11432
- **DOI:** https://doi.org/10.1007/s11704-024-40231-1
- **Citations:** ~1,200+
- **Relevance:** 5/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What this is:** 42-page comprehensive survey covering LLM-based autonomous agent construction, applications, and evaluation. Not an empirical study — reviews and synthesizes existing literature. Proposes a unified 4-module architectural framework.
- **Unified agent architecture framework (4 modules, cite-ready):**
  1. **Profiling module** — defines the agent's role and persona; three profile generation strategies: handcrafting (manual prompts), LLM-generation (automatic from seed profiles), dataset alignment (from real-world data)
  2. **Memory module** — stores and retrieves environmental observations; two structures: *unified memory* (short-term only, in-context window) and *hybrid memory* (short-term + long-term external vector storage); operations: reading, writing, reflection
  3. **Planning module** — decomposes tasks and sequences actions; two modes: *planning without feedback* (single-path or multi-path reasoning, e.g. CoT, ToT) and *planning with feedback* (environment feedback, human feedback, model feedback, e.g. Reflexion, ReAct)
  4. **Action module** — translates decisions into outputs; covers action targets (task completion, exploration, communication), action production (memory recollection, plan following), action space (tools, self-knowledge), and action impact (environments, internal states)
- **Applications surveyed:** Social science (opinion dynamics, social simulation), natural science (drug discovery, climate), engineering (software development, web agents, embodied agents)
- **Evaluation strategies:** Subjective (human evaluation, LLM-as-judge) and objective (task completion metrics, benchmark-specific measures)
- **What the paper does NOT do:** No empirical experiments. No comparison of workflow vs. agent paradigms. No quantitative thresholds for when to use which paradigm. Does not address cost, latency, or governance.
- **Precise citation note:** Both Q02 citations in the exposé are valid: (1) general claim that LLM systems process unstructured inputs and reason across multi-step tasks — confirmed by paper scope and framing; (2) "survey agent architectures comprehensively, covering profiling, memory, planning, and action" — matches the 4-module framework exactly.
- **Core Thesis Relevance:** Theoretical foundation for the agent paradigm side of the thesis (Section 2.1). The 4-module framework (Profiling/Memory/Planning/Action) maps to the six NADF archetypes: OIG → Planning; SDT → Action; AC → Action+Memory; OQE → Planning+Feedback; HET → Profiling+Planning; MSS → Memory+Planning. Co-cite with CoALA [Q08] for the agent architecture grounding — both surveys converge on the same core components.

---

### [Q03] Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing Reasoning and Acting in Language Models.
- **Authors:** Shunyu Yao, Jeffrey Zhao, Dian Yu, Nan Du, Izhak Shafran, Karthik Narasimhan, Yuan Cao
- **Year:** 2022 (submitted October 6, 2022; ICLR 2023)
- **Type:** P (Conference Paper, ICLR 2023)
- **arXiv:** 2210.03629
- **URL:** https://arxiv.org/abs/2210.03629
- **Citations:** ~2,000+
- **Relevance:** 5/5
- **Verification status:** ✅ Key numbers verified (2026-03-09)
- **Core mechanism:** Interleaves reasoning traces (Think) and actions (Act) in a single output stream. The loop is: Think → Act → Observe → Think → Act → Observe → ... The reasoning trace is not executed — it is a scratchpad guiding the next action. This is the defining characteristic of agent nodes (OIG, AC, OQE, MSS, HET archetypes in the thesis).
- **What was tested (4 benchmarks across 2 domains):**
  - Knowledge-intensive QA: HotpotQA (multi-hop reasoning), Fever (fact verification)
  - Sequential decision-making: ALFWorld (household navigation tasks), WebShop (e-commerce product search)
- **Baselines compared:** Standard LLM (no tools), Chain-of-Thought only (CoT), Act-only (no reasoning traces), Imitation Learning (IL), Reinforcement Learning (RL)
- **Key Findings (verified):**
  - ALFWorld: 34 percentage point absolute improvement over best non-ReAct baseline (RL/IL)
  - WebShop: 10 percentage point improvement over Act-only baseline
  - HotpotQA / Fever: Outperforms CoT-only (fewer hallucinations due to grounding via observations)
  - Interpretability: reasoning traces make failure diagnosis straightforward
- **Precise citation note:** The 34pp improvement on ALFWorld is vs. RL/IL baselines — not vs. a static workflow. The comparison is ReAct vs. pure-LLM methods, not agent vs. deterministic workflow.
- **What ReAct does NOT show:** No comparison to deterministic workflow execution. Does not measure cost or latency. Does not address failure rate on structured schema-output tasks.
- **Core Thesis Relevance:** Defines the Think-Act-Observe loop that underpins all autonomous agent archetypes (OIG, AC, OQE, MSS, HET). The 34pp ALFWorld result grounds H1 (agent superiority on unstructured retrieval). Cite as architectural foundation for agent nodes, not as evidence of agent superiority over workflows.

---

### [Q04] Xi, Z., Chen, W., Guo, X., et al. (2023). The Rise and Potential of Large Language Model Based Agents: A Survey.
- **Authors:** Zhiheng Xi, Wenxiang Chen, Xin Guo, Wei He, Yiwen Ding, Boyang Hong, Ming Zhang, et al. (Fudan University)
- **Year:** 2023 (submitted September 14, 2023)
- **Type:** S (Survey, 86 pages)
- **arXiv:** 2309.07864
- **URL:** https://arxiv.org/abs/2309.07864
- **Citations:** ~900+
- **Relevance:** 5/5
- **Abstract:** Proposes a three-component framework for LLM-based agents: Brain (LLM core), Perception (multimodal input), Action (output modalities). Covers single-agent systems, multi-agent interactions, and human-agent collaboration. Explores emergent behaviors within LLM agent societies.
- **Key Contributions:**
  - Brain-Perception-Action architecture framework
  - Multi-scenario coverage (single-agent, multi-agent, human-agent)
  - Analysis of emergent social phenomena in agent communities
  - Future challenges and open problems
- **Core Thesis Relevance:** Complementary major survey to [Q02]; different architectural framing useful for theoretical grounding.

---

### [Q05] Liu, X., Yu, H., Zhang, H., et al. (2023). AgentBench: Evaluating LLMs as Agents.
- **Authors:** Xiao Liu, Hao Yu, Hanchen Zhang, Yifan Xu, Xuanyu Lei, Hanyu Lai, Yu Gu, et al. (Tsinghua University, Ohio State, UC Berkeley)
- **Year:** 2023 (ICLR 2024)
- **Type:** P (Conference Paper, ICLR 2024)
- **arXiv:** 2308.03688
- **URL:** https://arxiv.org/abs/2308.03688
- **Citations:** ~500+
- **Relevance:** 5/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What was tested:** 29 LLMs across 8 interactive environments in 3 groups:
  - Code-grounded: OS interaction (Bash shell), Database queries (SQL), Knowledge Graph (multi-hop SPARQL)
  - Game-grounded: Digital Card Game (Dou Di Zhu), Lateral Thinking Puzzles (question-asking), House Holding (ALFWorld-style)
  - Web-grounded: Web Shopping (e-commerce navigation), Web Browsing (task completion on live web)
- **How it was tested:** Overall weighted score on a 0–10 scale across all environments. Commercial API models (GPT-4, ChatGPT, Claude, Bard, Gemini) compared against open-source models up to 70B parameters (LLaMA, Vicuna, CodeLlama, WizardLM, etc.). 5 failure type labels coded per trajectory.
- **Key Findings (verified):**
  - GPT-4 overall score: 4.01; average OSS model <70B: 0.51 — approximately 8× gap
  - 5 failure types: CLE (confused loop escape — stuck in repetitive actions), IF (instruction following failure — ignores task constraints), IA (invalid action — malformed output/API call), TLE (timeout — exceeded step limit without completion), Complete (reached end but produced wrong answer)
  - Main failure drivers: poor long-term reasoning across many steps, decision-making under ambiguity, instruction following on structured tasks
  - Code training: ambivalent impact — improves web-grounded tasks but hurts some game-grounded tasks
  - Cross-environment correlation: strong (r > 0.7) — models that perform well in one environment tend to perform well across others
- **What the paper does NOT do (important for citations):** No comparison of workflow execution paradigm vs. autonomous agent paradigm. No cost or latency data. No structured-output / schema-enforcement tasks. All 8 environments are interactive and sequential — not batch or stateless.
- **Precise citation note:** The 4.01 / 0.51 scores are on the normalized AgentBench scale, not accuracy percentages. Do not cite as "GPT-4 achieves 40% accuracy."
- **Core Thesis Relevance:** Primary empirical source for the commercial/OSS agent capability gap. The 5-type failure taxonomy (CLE, IF, IA, TLE, Complete) maps directly to the UEF error rate dimension (ER). GPT-4's 4.01/10 score grounds the calibrated expectation that even top models fail on approximately 60% of complex agent tasks, directly motivating the NADF's deterministic fallback nodes. Co-cited with Kapoor et al. [Q13] and Zhu et al. [Q37] for APS weight derivation.

---

### [Q06] Xiao, R., Ma, W., Wang, K., et al. (2024). FlowBench: Revisiting and Benchmarking Workflow-Grounded Planning for LLMs.
- **Authors:** Ruixuan Xiao, Wentao Ma, Ke Wang, Yuchuan Wu, Junbo Zhao, Haobo Wang, Fei Huang, Yongbin Li
- **Year:** 2024
- **Type:** P (Research Paper)
- **Relevance:** 5/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What was tested:** LLMs instructed to follow predefined workflow graphs (process diagrams with conditional branches and tool calls). Three workflow domains: (1) customer service (multi-turn dialogue with decision trees), (2) knowledge QA (retrieval + structured answering), (3) tool-use workflows (multi-step API sequences). Models evaluated include GPT-4, GPT-3.5-Turbo, Claude, and several open-source LLMs.
- **How it was tested:** Sessions scored as success/failure at the full session level (not step level). A session succeeds only if the LLM completes all required steps in the correct order without critical errors. Step-level errors are categorized into the 5-type taxonomy. Two evaluation modes: with full workflow graph provided in context; with only natural language workflow description.
- **Key Findings (verified):**
  - 43.2% average session success rate across all models and workflow types
  - Performance drops ~15pp when the workflow graph is described in natural language vs. provided as structured input
  - 5-type failure taxonomy: (1) step omission, (2) hallucinated steps, (3) wrong branching at conditionals, (4) tool misuse (wrong arguments/API), (5) premature termination
  - GPT-4 achieves the highest performance but still fails on ~40% of sessions
  - Tool-use workflow type has the lowest success rate; knowledge QA has the highest
- **What the paper does NOT do (important for citations):** Does NOT compare workflow execution paradigm vs. autonomous agent paradigm. All systems follow workflow instructions — this is not a workflow vs. agent study. Does not provide "distinct failure profiles for structured vs. unstructured tasks across paradigms."
- **Core Thesis Relevance:** The 43.2% session success rate grounds reliability arguments for LLM systems on structured tasks. The 5-type failure taxonomy provides vocabulary for the UEF error rate dimension (ER). The tool-use failure mode directly motivates the SDT archetype (deterministic schema-based tool calls). Cite for failure taxonomy and reliability evidence, NOT as paradigm-comparison.

---

### [Q07] Fan, S., Cong, X., Fu, Y., et al. (2024). WorkflowLLM: Enhancing Workflow Orchestration Capability of Large Language Models.
- **Authors:** Shengda Fan, Xin Cong, Yuepeng Fu, Zhong Zhang, Shen Gao, Jiajie Zhang, Yankai Lin, Zhiyuan Liu, Maosong Sun
- **Year:** 2024
- **Type:** P (Research Paper)
- **Citations:** ~80
- **Relevance:** 5/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What was tested:** Fine-tuning LLMs on workflow orchestration tasks in the Apple Shortcuts domain. Task: given a natural language description of a desired automation workflow, generate the corresponding Apple Shortcuts program (a sequence of app actions chained into a shortcut). This is static code generation — not runtime agent execution.
- **How it was tested:** Curated WorkflowBench (106,763 samples, 1,503 APIs, 83 apps, 28 categories). Fine-tuned LLaMA-based 8B model (WorkflowLlama) on this dataset. Evaluated on held-out test set using execution accuracy (does the generated shortcut run correctly?) and step-level accuracy.
- **Key Findings (verified):**
  - WorkflowLlama (8B fine-tuned) beats GPT-4o by 9.1pp on workflow code generation accuracy
  - Dataset scale: 106,763 samples covering 1,503 APIs across 83 apps in 28 categories
  - Domain-specific fine-tuning outperforms general-purpose models (even much larger ones)
  - The 9.1pp advantage is on Apple Shortcuts — generalizability to other workflow domains not tested
- **What the paper does NOT do (important for citations):**
  - Does NOT compare workflow paradigm vs. autonomous agent runtime paradigm
  - The Apple Shortcuts domain is static code generation — no runtime decision-making, no tool-call loop
  - "Fundamentally different training paradigms" interpretation is incorrect — the paper shows domain-specific fine-tuning helps, not that workflow and agent systems require different architectures
  - No real-world deployment or SME context
- **Core Thesis Relevance:** Demonstrates that structured workflow execution can be improved through specialized training data. The 106K-sample dataset scale and 9.1pp improvement show the value of domain-specific optimization for structured output tasks (relevant to SDT and OQE archetypes). Limited scope (Apple Shortcuts) means this cannot be cited as evidence for general workflow vs. agent comparisons.

---

## TIER 2 – Highly Relevant Supporting Papers (Relevance: 4/5)

---

### [Q08] Sumers, T.R., Yao, S., Narasimhan, K., & Griffiths, T.L. (2023). Cognitive Architectures for Language Agents.
- **Authors:** Theodore R. Sumers, Shunyu Yao, Karthik Narasimhan, Thomas L. Griffiths
- **Year:** 2023 (submitted September 5, 2023; final March 2024)
- **Type:** P
- **arXiv:** 2309.02427
- **URL:** https://arxiv.org/abs/2309.02427
- **Citations:** ~600+
- **Relevance:** 4/5
- **Verification status:** ✅ Content verified (2026-03-09)
- **What this is:** Theoretical framework paper (CoALA). No empirical experiments. Synthesizes cognitive science and AI literature to produce a unified design framework for language agents. Not a benchmark, not a system paper.
- **Core Framework — Three Dimensions:**
  1. **Memory modules (4 types):**
     - In-context (working memory): current prompt window, temporary reasoning
     - External (retrieved memory): vector stores, databases, retrieved at runtime
     - Episodic (past experiences): stored interaction histories, few-shot examples
     - Semantic (world knowledge): parametric LLM knowledge, fine-tuned representations
  2. **Action spaces (2 categories):**
     - External actions: world-altering actions — tool calls, API requests, file writes, environment interaction
     - Internal actions: reasoning (chain-of-thought), memory retrieval, learning, model parameter updates
  3. **Decision procedure (2-stage):**
     - Observe: ground the agent in current context (memory retrieval + environment state)
     - Orient-Decide-Act: generate reasoning trace, select action, execute
- **What CoALA does NOT contain (important for citations):**
  - No "planning horizon" dimension — this term does not appear as a named framework component
  - No empirical comparison of architectures — purely theoretical synthesis
  - No claims about workflow vs. agent performance tradeoffs
- **Core Thesis Relevance:** Section 2.3 and Definition 7.4. The action space taxonomy (external vs. internal) grounds the node archetype taxonomy — OIG/AC/OQE/MSS/HET use the full internal reasoning action space; SDT uses only external tool calls without internal reasoning. The 4 memory types inform the memory architecture design for the ALIC use case. Cite for theoretical framework, not for empirical claims.

---

### [Q09] Shinn, N., Cassano, F., Berman, E., Gopinath, A., Narasimhan, K., & Yao, S. (2023). Reflexion: Language Agents with Verbal Reinforcement Learning.
- **Authors:** Noah Shinn, Federico Cassano, Edward Berman, Ashwin Gopinath, Karthik Narasimhan, Shunyu Yao (Northeastern University, MIT, Princeton)
- **Year:** 2023 (NeurIPS 2023)
- **Type:** P (Conference Paper, NeurIPS 2023)
- **arXiv:** 2303.11366
- **URL:** https://arxiv.org/abs/2303.11366
- **Citations:** ~800+
- **Relevance:** 4/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What was tested:** Reflexion — a verbal reinforcement learning framework. No weight updates; instead, agents generate textual self-reflections after each failed trial and store them in an episodic long-term memory buffer. Tested across three task types: (1) sequential decision-making (ALFWorld), (2) knowledge-intensive reasoning (HotPotQA), (3) code generation (HumanEval + LeetcodeHardGym).
- **How it was tested:** Iterative multi-trial setup. Each trial: agent acts → evaluator scores trajectory (binary reward, heuristic, or LLM self-evaluation / self-written unit tests) → Reflexion generates verbal summary of failure → appended to long-term memory → agent retries. Baseline: ReAct + CoT agents without reflection loop.
- **Key Findings (verified):**
  - ALFWorld (decision-making): +22 percentage points absolute over strong baseline in 12 iterative learning steps
  - HotPotQA (reasoning): +20% improvement over baseline
  - HumanEval (coding): 91% pass@1 — exceeds GPT-4's 80% at time of publication (+11pp)
  - Feedback types ranked: self-generated unit tests > pre-defined heuristics > binary environment reward
  - Short-term memory (trajectory history) + long-term memory (verbal reflections) work in tandem
- **What the paper does NOT do:** No comparison to deterministic workflows. No cost or latency analysis. No formal convergence guarantee ("relies on the power of the LLM's self-evaluation capabilities"). Improvements saturate after ~12 trials — not unbounded improvement. LeetcodeHard results show limits on truly novel algorithmic problems.
- **Precise citation note:** The 91% HumanEval figure is pass@1 for the Reflexion agent — not a baseline GPT-4 number. The +22pp ALFWorld gain is vs. ReAct/CoT baselines, not vs. static workflows. Do not cite as evidence that agents outperform workflows on structured tasks.
- **Core Thesis Relevance:** Architectural foundation for the OQE (Output Quality Evaluator) and MSS (Multi-Step Solver) archetypes — both use iterative feedback loops analogous to the Reflexion retry mechanism. The verbal reflection pattern is the basis for the OQE's quality gate and retry trigger in the NADF. Grounds H3 (agent adaptability via self-correction) when paired with Zhu et al. [Q37] failure taxonomy. Cite for the episodic memory + self-correction mechanism, not as evidence of general agent superiority.

---

### [Q10] Wu, Q., Bansal, G., Zhang, J., et al. (2023). AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation.
- **Authors:** Qingyun Wu, Gagan Bansal, Jieyu Zhang, Yiran Wu, Beibin Li, et al. (Microsoft Research)
- **Year:** 2023
- **Type:** P/F
- **Citations:** ~1,000+
- **Relevance:** 4/5
- **Abstract:** AutoGen framework enabling LLM applications via multi-agent conversations. Agents are customizable, conversable, can operate via LLMs, human inputs, and tools. Contrasts rigid single-pass pipelines with flexible multi-agent conversational architectures.
- **Key Contribution:** Multi-agent hybrid framework; demonstrates how workflow and agent paradigms can be combined.

---

### [Q11] Hong, S., Zhuge, M., Chen, J., et al. (2023). MetaGPT: Meta Programming for A Multi-Agent Collaborative Framework.
- **Authors:** Sirui Hong, Mingchen Zhuge, Jonathan Chen, Xiawu Zheng, Yuheng Cheng, Ceyao Zhang, et al.
- **Year:** 2023
- **Type:** P (ICLR 2024)
- **Citations:** ~700+
- **Relevance:** 4/5
- **Abstract:** Encodes Standardized Operating Procedures (SOPs) into prompt sequences enabling reliable workflows within a collaborative multi-agent framework. Assigns different roles to GPT models, coordinating them in a structured pipeline. Represents a hybrid between rigid workflows and fully autonomous agents.
- **Key Contribution:** Hybrid SOP-workflow + multi-agent architecture; directly relevant to hybrid paradigm discussion.

---

### [Q12] Schick, T., Dwivedi-Yu, J., Dessì, R., et al. (2023). Toolformer: Language Models Can Teach Themselves to Use Tools.
- **Authors:** Timo Schick, Jane Dwivedi-Yu, Roberto Dessì, Roberta Raileanu, Maria Lomeli, Luke Zettlemoyer, Nicola Cancedda, Thomas Scialom
- **Year:** 2023 (NeurIPS 2023)
- **Type:** P
- **arXiv:** 2302.04761
- **URL:** https://arxiv.org/abs/2302.04761
- **Citations:** ~1,500+
- **Relevance:** 4/5
- **Abstract:** Introduces Toolformer – model trained via self-supervision to decide which APIs to call, when, with what arguments. Tools: calculator, calendar, Wikipedia search, translation, Q&A. 6.7B Toolformer outperforms 175B GPT-3 on several benchmarks.
- **Key Contribution:** Demonstrates that tool use can be learned; precursor to function-calling in GPT-4/Claude; bridges workflow-tool-use and agent autonomy.

---

### [Q13] Kapoor, S., Stroebl, B., Siegel, Z.S., Nadgir, N., & Narayanan, A. (2024). AI Agents That Matter.
- **Authors:** Sayash Kapoor, Benedikt Stroebl, Zachary S. Siegel, Nitya Nadgir, Arvind Narayanan (Princeton)
- **Year:** 2024 (submitted July 1, 2024)
- **Type:** P
- **arXiv:** 2407.01502
- **URL:** https://arxiv.org/abs/2407.01502
- **Relevance:** 4/5
- **Verification status:** ✅ Key arguments verified (2026-03-09)
- **What was analyzed:** Meta-analysis of AI agent benchmarks (primarily SWE-bench and similar coding/task-completion benchmarks). Re-analyzes published results with added cost accounting. Does not run new experiments — reinterprets existing published data with economic lens.
- **Core Critique (3 arguments):**
  1. **Benchmark gaming:** Published SOTA agents optimize for benchmark accuracy while ignoring API cost. A 5pp accuracy gain often requires 10× the API calls. Cost is never reported alongside accuracy.
  2. **Cost-accuracy Pareto frontier:** When cost is plotted against accuracy, most "state-of-the-art" agents are not on the Pareto frontier — simpler, cheaper systems achieve comparable accuracy.
  3. **Break-even analysis:** At ~1,350 tasks processed per month, automated agent cost equals human labor cost (at US minimum wage). Below this threshold, human execution is economically competitive or superior.
- **Key Findings (verified):**
  - Cost is never reported in 96% of agent benchmark papers (as of mid-2024)
  - The 1,350 task/month break-even applies to a specific cost model — actual threshold varies by API pricing and task complexity
  - Proposed metric: tasks per dollar (rather than pure accuracy)
- **What this paper does NOT do:** Does not compare workflow paradigm vs. agent paradigm. Does not provide per-archetype cost data. Break-even figure is indicative, not universal.
- **Core Thesis Relevance:** Grounds the TC (Token Cost) and ER (Error Rate) dimensions of the UEF. Justifies including cost as first-class metric (APS weight: 0.20). The 1,350 break-even figure provides SME-relevant cost context for Discussion section 6.3. Co-cited with Liu et al. [Q05] and Zhu et al. [Q37] for APS weight derivation.

---

### [Q14] Park, J.S., O'Brien, J.C., Cai, C.J., Morris, M.R., Liang, P., & Bernstein, M.S. (2023). Generative Agents: Interactive Simulacra of Human Behavior.
- **Authors:** Joon Sung Park, Joseph C. O'Brien, Carrie J. Cai, Meredith Ringel Morris, Percy Liang, Michael S. Bernstein (Stanford/Google)
- **Year:** 2023 (ACM UIST 2023)
- **arXiv:** 2304.03442
- **Citations:** ~2,000+
- **Relevance:** 4/5
- **Abstract:** 25 LLM-powered agents in Smallville sandbox; agents demonstrate daily routines, form relationships, organize social events (emergent Valentine's Day party). Architecture: memory streams, reflection, retrieval.
- **Key Contribution:** Demonstrates emergent behavior in autonomous agents impossible with static workflows; highlights agent superiority for open-ended, social simulation tasks.

---

### [Q15] Shen, Y., Song, K., Tan, X., et al. (2023). HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face.
- **Authors:** Yongliang Shen, Kaitao Song, Xu Tan, Dongsheng Li, Weiming Lu, Yueting Zhuang
- **Year:** 2023 (NeurIPS 2023)
- **arXiv:** 2303.17580
- **Citations:** ~800+
- **Relevance:** 4/5
- **Abstract:** LLM (ChatGPT) as orchestrator selecting and coordinating specialized AI models from Hugging Face. Covers language, vision, speech. Demonstrates LLM-orchestrated workflow as path toward AGI.
- **Key Contribution:** Exemplifies LLM-as-workflow-orchestrator; hybrid between pure workflow and pure agent.

---

## TIER 3 – Relevant Context Papers (Relevance: 3/5)

---

### [Q16] Wei, J., Wang, X., Schuurmans, D., et al. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models.
- **Authors:** Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Brian Ichter, Fei Xia, Ed Chi, Quoc Le, Denny Zhou (Google Brain)
- **Year:** 2022 (NeurIPS 2022)
- **arXiv:** 2201.11903
- **Citations:** ~10,000+
- **Relevance:** 3/5
- **Abstract:** Intermediate reasoning steps significantly improve LLM performance on complex tasks. Emergent ability in models >~100B parameters. State-of-the-art on GSM8K with 540B model + 8 examples.
- **Key Contribution:** Foundation for agent planning; CoT is the reasoning backbone of most agent architectures.

---

### [Q17] Yao, S., Yu, D., Zhao, J., et al. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models.
- **Authors:** Shunyu Yao, Dian Yu, Jeffrey Zhao, Izhak Shafran, Thomas L. Griffiths, Yuan Cao, Karthik Narasimhan
- **Year:** 2023
- **arXiv:** 2305.10601
- **Citations:** ~3,000+
- **Relevance:** 3/5
- **Abstract:** Generalizes CoT to explore multiple reasoning pathways (tree search). Enables deliberate decision-making with self-evaluation and backtracking. GPT-4 with ToT: 74% on Game of 24 vs. 4% with CoT.
- **Key Contribution:** Advanced planning strategy for agents; relevant to agent planning superiority in complex tasks.

---

### [Q18] Hong, S., Lin, Y., Liu, B., et al. (2024). Data Interpreter: An LLM Agent For Data Science.
- **Authors:** Sirui Hong, Yizhang Lin, Bang Liu, et al. (MetaGPT team)
- **Year:** 2024
- **arXiv:** 2402.18679
- **Citations:** ~200
- **Relevance:** 3/5
- **Abstract:** LLM agent for end-to-end data science tasks. Hierarchical graph modeling; 25% boost on InfiAgent-DABench (75.9%→94.9%), 37% improvement on open-ended tasks.
- **Key Contribution:** Concrete domain-specific agent outperforming workflows in data science context.

---

### [Q19] Feng, P., He, Y., Huang, G., et al. (2024). AGILE: A Novel Reinforcement Learning Framework of LLM Agents.
- **Authors:** Peiyuan Feng, Yichen He, Guanhua Huang, Yuan Lin, Hanchong Zhang, Yuchen Zhang, Hang Li
- **Year:** 2024 (NeurIPS 2024)
- **arXiv:** 2405.14751
- **Relevance:** 3/5
- **Abstract:** RL framework for LLM agents with memory, tools, expert consultation, and reflection. Fine-tuned via PPO. 7B/13B models outperform GPT-4 agents on multiple QA benchmarks.
- **Key Contribution:** Demonstrates that training paradigm (RL vs. prompting) matters for agent performance; relevant to methodology discussion.

---

### [Q20] Li, G., Hammoud, H.A., Itani, H., Khizbullin, D., & Ghanem, B. (2023). CAMEL: Communicative Agents for 'Mind' Exploration of Large Scale Language Model Society.
- **Authors:** Guohao Li, Hasan Anil Hammoud, Hani Itani, Dmitrii Khizbullin, Bernard Ghanem
- **Year:** 2023
- **Citations:** ~600+
- **Relevance:** 3/5
- **Abstract:** Role-playing multi-agent framework. Agents negotiate autonomously via "inception prompting" without pre-specified workflow steps. Solves 89.7% of tasks through dynamic negotiation.
- **Key Contribution:** Demonstrates multi-agent autonomy without workflow scaffolding.

---

### [Q21] Wang, G., Xie, Y., Jiang, Y., et al. (2023). Voyager: An Open-Ended Embodied Agent with Large Language Models.
- **Authors:** Guanzhi Wang, Yuqi Xie, Yunfan Jiang, et al. (NVIDIA)
- **Year:** 2023
- **Citations:** ~700+
- **Relevance:** 3/5
- **Abstract:** First LLM-powered embodied lifelong learning agent in Minecraft. Three components: automatic curriculum (maximizes exploration), ever-growing skill library (executable code), iterative prompting mechanism. No human intervention.
- **Key Contribution:** Demonstrates agent superiority in open-ended environments where workflows cannot be predefined.

---

### [Q22] Patil, S.G., Zhang, T., Wang, X., & Gonzalez, J.E. (2023). Gorilla: Large Language Model Connected with Massive APIs.
- **Authors:** Shishir G. Patil, Tianjun Zhang, Xin Wang, Joseph E. Gonzalez (UC Berkeley)
- **Year:** 2023
- **arXiv:** 2305.15334
- **Citations:** ~600+
- **Relevance:** 3/5
- **Abstract:** Fine-tuned LLaMA model surpassing GPT-4 in writing API calls. Introduces APIBench (16,000+ APIs). Robust to API documentation changes via document retriever.
- **Key Contribution:** Tool-use precision as key metric; relevant to comparing agent tool-use accuracy vs. workflow hardcoded API calls.

---

### [Q23] Sun, C., Huang, S., & Pompili, D. (2024). LLM-Based Multi-Agent Reinforcement Learning: Current and Future Directions.
- **Authors:** Chuanneng Sun, Songjun Huang, Dario Pompili
- **Year:** 2024
- **Citations:** ~150
- **Relevance:** 3/5
- **Abstract:** Survey of LLM integration with MARL. Taxonomy: (1) LLM agents with full autonomy, (2) hybrid workflow-agent systems, (3) LLM-orchestrated fixed workflow pipelines.
- **Key Contribution:** Provides a three-tier taxonomy directly mapping the paradigm spectrum from workflows to agents.

---

## TIER 4 – Background/Contextual (Relevance: 2/5)

---

### [Q24] Richards, T.B. (2023). AutoGPT: An Autonomous GPT-4 Experiment.
- **Authors:** Toran Bruce Richards (Significant Gravitas)
- **Year:** 2023 (open-source, April 2023; no formal paper)
- **URL:** https://github.com/Significant-Gravitas/AutoGPT
- **Relevance:** 2/5
- **Abstract:** First widely-known autonomous LLM agent. Uses GPT-4 with goal → plan → act → observe → re-plan loop. Demonstrated both promise and limitations of fully autonomous agents.

---

### [Q25] Lu, P., Peng, B., Cheng, H., et al. (2023). Chameleon: Plug-and-Play Compositional Reasoning with Large Language Models.
- **Authors:** Pan Lu, Baolin Peng, Hao Cheng, Michel Galley, et al. (UCLA/Microsoft)
- **Year:** 2023
- **arXiv:** 2305.00955
- **Citations:** ~400+
- **Relevance:** 2/5
- **Abstract:** Compositional reasoning framework augmenting LLMs with diverse tools (vision models, web search, Python, rule-based modules). Sits between fixed workflows and fully autonomous agents.

---

### [Q26] Qin, Y., Liang, S., Ye, Y., et al. (2023). ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs.
- **Authors:** Yujia Qin, Shihao Liang, Yining Ye, et al.
- **Year:** 2023
- **Citations:** ~600+
- **Relevance:** 2/5
- **Abstract:** ToolBench dataset (16,464 REST APIs). ToolLlama achieves tool-use performance comparable to ChatGPT. Bridges workflow automation and dynamic agent behavior.

---

---

## TIER 1 – Core Papers (Relevance: 5/5) — Continued

---

### [Q27] Li, X. (2026). When Single-Agent with Skills Replace Multi-Agent Systems and When They Fail.
- **Authors:** Xiaoxiao Li (University of British Columbia, Vector Institute, CIFAR AI Chair)
- **Year:** January 2026
- **Type:** P (Preprint, arXiv v2)
- **arXiv:** 2601.04748
- **URL:** https://doi.org/10.48550/arXiv.2601.04748
- **Relevance:** 4/5 (revised down from 5/5 — paper is SAS vs MAS within agent paradigm, NOT workflow vs. agent)
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this paper is:** Investigates whether a single LLM agent equipped with a library of "skills" can replace a multi-agent system (MAS). Skills = schema-bounded operations with semantic descriptors + execution policies (not deterministic workflow nodes). Introduces the MAS-to-SAS Compilation paradigm and the Skill Scaling Hypothesis.
- **Compilability Conditions (Proposition 3.1):** A MAS is compilable to SAS if and only if:
  1. Serializable communication (no true parallelism required)
  2. Shared history (no private state between agents)
  3. Homogeneous backbone (all agents use same model)
  - Compilable: Pipeline, Router-Workers, Iterative Refinement
  - NOT compilable: Debate/Adversarial, Parallel Sampling, Private-state agents
- **Compilation Efficiency Results (verified, GPT-4o-mini backbone):**
  - Task accuracy: SAS achieves -2.0% to +4.0% of MAS (average +0.7%)
  - Token reduction: 53.7% average (56.2% GSM8K, 46.5% HumanEval, 58.4% HotpotQA)
  - Latency reduction: 49.5% average (28.7% GSM8K, 58.9% HumanEval, 60.9% HotpotQA)
  - API calls: 3–4 calls → 1 call (75% reduction for HotpotQA)
- **Skill Scaling Hypothesis (key finding):** Skill selection accuracy degrades non-linearly as library grows. Phase transition: accuracy stable below a critical threshold, then drops sharply. Semantic confusability (similar skills interfering) drives degradation more than raw library size alone.
- **Hierarchical Routing:** Decomposing skill selection into coarse-to-fine stages mitigates the phase transition, restoring reliable selection at scale.
- **What the paper does NOT do (important for citations):**
  - Does NOT compare deterministic workflows vs. LLM agents — SAS and MAS are both LLM-agent paradigms
  - "Skills" ≠ deterministic workflow nodes (skills still involve LLM reasoning for selection)
  - Does not address the paradigm choice at node level
- **Core Thesis Relevance:** Related work positioning (Section 2.1/2.2). The 53.7% token reduction and 49.5% latency reduction provide efficiency context for the thesis cost arguments. The compilability conditions partially mirror the NADF's paradigm selection logic. The Skill Scaling Hypothesis is thematically similar to the thesis's archetype taxonomy design (avoiding overlapping archetypes). Cite for efficiency evidence and as a conceptual parallel in the related work discussion — not as direct support for the workflow/agent distinction.

---

### [Q28] Gao, M., Li, Y., Liu, B., Yu, Y., Wang, P., Lin, C.-Y., & Lai, F. (2025). Single-agent or Multi-agent Systems? Why Not Both?
- **Authors:** Meng Gao, Yifan Li, Boyuan Liu, et al.
- **Year:** 2025
- **Type:** P (Research Paper)
- **arXiv:** 2505.18286
- **URL:** https://doi.org/10.48550/arXiv.2505.18286
- **Relevance:** 5/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **Abstract:** Compares single-agent systems (SAS) vs. multi-agent systems (MAS) for complex task decomposition. The comparison is SAS vs. MAS — both are fully agent-based paradigms. Proposes request cascading as a routing mechanism: simple tasks stay in SAS, complex tasks escalate to MAS. Evaluated on academic agent benchmarks only.
- **Key Findings (verified):**
  - SAS vs. MAS comparison (NOT workflow vs. agent — this is the critical point)
  - Request cascading mechanism routes tasks by complexity between SAS and MAS
  - Academic benchmark evaluation only — no production/enterprise validation
  - Self-identified limitation: "lacks transparent guidelines distinguishing when each paradigm excels"
- **What the paper does NOT do (important for citations):** Does NOT compare deterministic workflows vs. autonomous agents. Does NOT propose hybrid workflow+agent architectures. The "hybrid" in this paper means SAS+MAS, not workflow+agent.
- **Core Thesis Relevance:** Closest related work because they identify the paradigm-selection gap that the thesis fills — but at system level (SAS/MAS), not node level (deterministic/agent). Their stated limitation ("lacks transparent paradigm-selection guidelines") is exactly what the NADF addresses, at a finer granularity and with empirical node-level evidence. Use to sharpen positioning.

---

## TIER 2 – Highly Relevant Supporting Papers (Relevance: 4/5) — Continued

---

### [Q29] Bogavelli, T., Sharma, R., & Subramani, H. (2025). AgentArch: A Comprehensive Benchmark to Evaluate Agent Architectures in Enterprise.
- **Authors:** Teja Bogavelli, Rohit Sharma, Harish Subramani
- **Year:** 2025
- **Type:** P (Research Paper)
- **arXiv:** 2509.10769 (Version 2)
- **URL:** https://doi.org/10.48550/ARXIV.2509.10769
- **Relevance:** 4/5
- **Local copy:** `inputs/2509.10769v2.pdf`
- **Verification status:** ✅ Key numbers verified (2026-03-09)
- **Abstract:** Introduces AgentArch, a benchmark for evaluating agent architectures in enterprise deployment contexts. Focuses on realistic enterprise tasks spanning varying complexity levels. Key finding: enterprise agents show strong task-complexity sensitivity — max 35.3% success on complex tasks, 70.8% on simpler tasks.
- **Key Findings (verified):**
  - Maximum 35.3% task success rate on complex enterprise tasks
  - 70.8% success on simpler enterprise tasks
  - Strong task-complexity sensitivity — performance halves as task complexity increases
  - Enterprise deployment context (not academic benchmarks)
- **Core Thesis Relevance:** H2 grounding — demonstrates enterprise agents struggle with structured complex tasks. The 35.3%/70.8% split quantifies the reliability gap that motivates deterministic workflow nodes for structured archetypes (SDT, HET). Use these specific numbers in H2 citation.

---

### [Q30] Kim, Y., Gu, K., Park, C., et al. (2025). Towards a Science of Scaling Agent Systems.
- **Authors:** Yejin Kim, Kyuyong Gu, Changhoon Park, et al. (multiple institutions including CMU, Stanford)
- **Year:** 2025
- **Type:** P (Research Paper)
- **arXiv:** 2512.08296 (Version 2)
- **URL:** https://doi.org/10.48550/ARXIV.2512.08296
- **Local copy:** `inputs/2512.08296v2.pdf`
- **Relevance:** 4/5
- **Verification status:** ✅ Key content verified (2026-03-09)
- **What was tested:** Five agent architecture variants evaluated on a task suite spanning simple to complex scenarios. All five architectures are fully LLM-agent-based — no deterministic workflow systems are included in the comparison. The paper studies how adding more agents (scaling) affects performance, cost, and coordination overhead.
- **Key Findings (verified):**
  - Below 45% task success threshold: MAS outperforms SAS (multi-agent coordination helps on complex tasks)
  - Above 45% threshold: MAS does not reliably outperform SAS (coordination overhead dominates)
  - Increasing agent count without task decomposition strategy yields diminishing returns
  - Reliability decreases non-linearly as agent count increases (coordination failures compound)
- **What this paper does NOT do (important for citations):**
  - Does NOT compare deterministic workflows vs. LLM agents — all architectures are agent-based
  - Does NOT provide paradigm-selection criteria at the node level
  - The "45% threshold" applies to SAS vs. MAS within the agent paradigm only
- **Core Thesis Relevance:** H3 grounding (agent reasoning advantage on edge cases). The 45% success threshold provides empirical context for when autonomous agents add value vs. when structured coordination degrades performance — analogous argument to workflow vs. agent at node level. Cite for scaling dynamics, not for workflow/agent paradigm comparison.

---

### [Q31] Mohammadi, M., Li, Y., Lo, J., & Yip, W. (2025). Evaluation and Benchmarking of LLM Agents: A Survey.
- **Authors:** Mahmoud Mohammadi, Yipeng Li, Jane Lo, Wendy Yip (SAP Labs, Bellevue/Palo Alto)
- **Year:** 2025 (published August 3, 2025)
- **Type:** S (Survey/Tutorial, KDD 2025 — ACM SIGKDD Conference on Knowledge Discovery and Data Mining)
- **DOI:** https://doi.org/10.1145/3711896.3736570
- **Relevance:** 4/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **Note on previous entry:** Author names were incorrect — corrected from "Maryam/Yifan/Jason/William" to actual names from PDF title page.
- **What this is:** 11-page survey/tutorial paper presenting a structured overview of LLM agent evaluation. Conceptual taxonomy — not an empirical study. No new benchmark or experiment.
- **Core taxonomy — 2-dimensional:**
  - **Evaluation Objectives (what to evaluate):** (1) Agent Behavior — task completion, output quality, latency, cost; (2) Agent Capabilities — tool use, planning/reasoning, memory/context retention, multi-agent collaboration; (3) Reliability — consistent behavior for same input; (4) Safety — fairness, compliance, harm prevention
  - **Evaluation Process (how to evaluate):** (1) Interaction Mode — static (fixed inputs) vs. interactive (dynamic user engagement); (2) Evaluation Data — synthetic and real-world datasets, domain benchmarks (software engineering, healthcare, finance); (3) Metrics Computation Methods — quantitative (task success, factual accuracy) and qualitative (human or LLM judgment); (4) Evaluation Tooling — instrumentation frameworks (LangSmith, Arize AI), leaderboards (HELM); (5) Evaluation Contexts — controlled simulations vs. open-world (web, APIs)
- **Enterprise-specific challenges highlighted (unique contribution):** Role-based access control (RBAC) as evaluation constraint; reliability guarantees needed for audit and compliance; dynamic/long-horizon interactions; compliance requirements rarely addressed in academic evaluation frameworks.
- **What the paper does NOT do:** Does not conduct empirical experiments. Does not provide new benchmark data or cross-paradigm comparison numbers. Does not validate its taxonomy against actual agent deployments. The enterprise challenges section is descriptive, not empirically grounded.
- **Precise citation note:** Do not cite quantitative benchmark figures from this paper — it surveys existing benchmarks without producing new numbers. Cite for the 2D taxonomy structure and for the enterprise evaluation gap argument.
- **Core Thesis Relevance:** Primary methodological source for the UEF design (Phase 4). The 2D taxonomy (Objectives × Process) directly maps to the UEF's APS formula: Agent Behavior → TCR/OQS; Reliability → ER; Capabilities → task-type-appropriate sub-metrics. The enterprise challenge on compliance directly supports NADF's design rationale (Section 2.5 and Discussion 6.3).

---

### [Q32] Nowaczyk, S. (2025). Architectures for Building Agentic AI.
- **Authors:** Slawomir Nowaczyk
- **Year:** 2025
- **Type:** P (Research Paper)
- **arXiv:** 2512.09458
- **URL:** https://doi.org/10.48550/arXiv.2512.09458
- **Local copy:** `inputs/2512.09458v1 (2).pdf`
- **Relevance:** 4/5
- **Verification status:** ✅ Key content verified (2026-03-09)
- **What this is:** Architecture taxonomy and design-principle paper. No empirical experiments, no benchmark data. Qualitative synthesis of existing systems and patterns into a unified taxonomy. Single author.
- **Core Content:**
  - Architectural taxonomy covering: single-agent, multi-agent, hierarchical, hybrid workflow-agent patterns
  - Key proposition: governance and control layers should be deterministic even when agent cores are autonomous — reliability requires structured boundaries around agent freedom
  - Threshold-based control as a reliability mechanism: deterministic thresholds (confidence scores, rule checks) trigger escalation or rejection without autonomous agent judgment
  - Trade-off framing: control ↔ flexibility is not a binary choice but a design space; hybrid architectures occupy the middle ground
- **Key Design Principles (qualitative, no empirical backing):**
  - High-stakes decision points should use deterministic threshold checks, not agent judgment
  - Agents should operate within sandboxed action spaces to contain failure propagation
  - Monitoring and observability are architectural requirements, not add-ons
- **What this paper does NOT do:** No quantitative comparison between architectures. No benchmark evaluation. All recommendations are qualitative heuristics from literature synthesis.
- **Core Thesis Relevance:** H4 grounding (deterministic superiority on human escalation triggers). The threshold-based control principle directly supports the HET archetype design. Reliability heuristics ground the governance argument for deterministic nodes in high-stakes SME workflows. Cite as design-principle source, not as empirical evidence.

---

### [Q33] Sapkota, R., Shrestha, R., Rijal, M., & Karkee, M. (2025). LangChain vs. LangGraph vs. LangSmith: Taxonomies of Agentic AI Toolchains for End-to-End Orchestration.
- **Authors:** Ranjan Sapkota (Cornell), Rashik Shrestha (West Virginia Univ.), Madhav Rijal (West Virginia Univ.), Manoj Karkee (Cornell)
- **Year:** September 2025
- **Type:** P (TechRxiv Preprint — NOT peer-reviewed)
- **DOI:** https://doi.org/10.36227/techrxiv.175695645.52670060/v1
- **Local copy:** `inputs/1328506.pdf`
- **Relevance:** 3/5 (revised down — methodology reference only, not academic claim source)
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this is:** Survey/taxonomy paper comparing three LangChain ecosystem tools. NOT peer-reviewed (TechRxiv preprint). No empirical experiments. No performance benchmarks for workflow vs. agent paradigm comparison. Conceptual taxonomy only.
- **Core Taxonomy (verified):**
  - **LangChain:** Chain-based linear workflow composition, DAG-based task execution, excels at RAG pipelines and rapid prototyping. Workflow-first paradigm.
  - **LangGraph:** Stateful directed graph orchestration, supports cyclic reasoning, multi-agent collaboration, event-driven execution, non-linear control flows. Agent-first paradigm.
  - **LangSmith:** Observability, tracing, debugging, evaluation layer. Not an execution framework.
  - Framework comparison taxonomy dimensions: state handling, control flow, orchestration complexity, developer ergonomics, interoperability, governance readiness
- **Key architectural distinction (for thesis implementation):**
  - LangChain chains = deterministic, sequential, no cycles = maps to SDT archetype
  - LangGraph nodes with conditional edges + agent loops = maps to OIG/AC/OQE/MSS/HET archetypes
  - LangGraph's node-level architecture makes it the correct implementation tool for the NADF (each archetype = one LangGraph node type)
- **What the paper does NOT do:** No quantitative comparison of LangChain vs. LangGraph performance. No empirical evidence for workflow vs. agent superiority. Not peer-reviewed — cannot be cited as primary academic evidence.
- **Core Thesis Relevance:** Phase 3 (System Implementation) — justifies LangGraph as the implementation framework for the hybrid system. The chain-vs-graph distinction operationalizes the workflow/agent paradigm at the toolchain level. Use as methodology reference, not as academic evidence for performance claims.

---

### [Q34] Shaikh, S. H. (2026). LLM-Based Multi-agent Systems: Frameworks, Evaluation, Open Challenges, and Research Frontiers.
- **Authors:** Saqib Hussain Shaikh
- **Year:** 2026
- **Type:** P (Book Chapter, Springer)
- **Published:** In Computational Intelligence, Vol. 2827, pp. 149–170. Springer Nature Switzerland.
- **DOI:** https://doi.org/10.1007/978-3-032-15632-7_9
- **Relevance:** 4/5
- **Abstract:** Comprehensive overview of LLM-based multi-agent systems covering frameworks (AutoGen, MetaGPT, CrewAI), evaluation methodologies, and open challenges. Identifies key research frontiers: scalability, coordination overhead, evaluation standardization, and reliability in production. Explicitly discusses when multi-agent frameworks add value vs. when single-agent or workflow approaches suffice.
- **Key Contributions:**
  - Current-state overview of multi-agent frameworks (2025/2026 perspective)
  - Evaluation methodology survey for multi-agent systems
  - Research frontier identification including cross-paradigm comparison gap
- **Core Thesis Relevance:** Supports theoretical background (Section 2.3) and research gap argumentation; recent survey providing up-to-date framework landscape.

---

### [Q35] Gregor, S., & Hevner, A. R. (2013). Positioning and Presenting Design Science Research for Maximum Impact.
- **Authors:** Shirley Gregor (Australian National University), Alan R. Hevner (Univ. South Florida)
- **Year:** 2013
- **Type:** P (Journal Article, MIS Quarterly Vol. 37 No. 2, pp. 337–355, June 2013)
- **DOI:** https://doi.org/10.25300/MISQ/2013/37.2.01
- **Citations:** ~2,100+
- **Relevance:** 4/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What this is:** Companion to Hevner et al. 2004 [Q36]. Conceptual essay, not empirical. Addresses a persistent gap: researchers produce DSR but fail to clearly position and communicate the knowledge contribution type. Provides two practical tools: the knowledge contribution framework and the DSR communication schema.
- **DSR Knowledge Contribution Framework — 2×2 matrix (Figure 3):**
  - x-axis: problem maturity (high = well-understood problem; low = new/unrecognized problem)
  - y-axis: solution maturity (high = existing artifacts/solutions available; low = no existing solutions)
  - Four quadrants:
    1. **Routine Design** (high problem / high solution maturity): applying known solutions to known problems — not a typical research contribution
    2. **Improvement** (high problem / low solution maturity): new or better solutions for known problems — incremental research contribution
    3. **Exaptation** (low problem / high solution maturity): repurpose existing solutions from other domains to address new problem — moderate contribution
    4. **Invention** (low problem / low solution maturity): new solutions for new problems — radical breakthrough, rarest and highest-impact
- **Three abstraction levels of artifact contributions:**
  - Level 1: specific, situated artifact (demonstrates feasibility)
  - Level 2: nascent design theory (constructs, principles, rules — the most common DSR publication level)
  - Level 3: well-developed design theory (fully formalized, extensively validated)
- **DSR communication schema:** Replaces the traditional "Results" section with an "Artifact Description" section; otherwise follows conventional journal structure (Introduction, Background, Method, Artifact, Evaluation, Contribution, Conclusion).
- **What the paper does NOT do:** No empirical validation of the framework itself. The quadrant assignments are interpretive, not algorithmic. Does not prescribe which quadrant a given project must target.
- **Precise citation note:** Cite as Gregor & Hevner (2013) — not "Gregor et al." (only two authors). Pair with Hevner et al. [Q36] for the full DSR methodological grounding.
- **Core Thesis Relevance:** Positions the NADF knowledge contribution type. The NADF fits the "Improvement" quadrant: the problem (orchestration node selection) is known; existing solutions (pure workflow / pure agent) exist but are inadequate. The thesis contributes a better solution — a hybrid decision method. This positioning must be stated explicitly in Chapter 3 to satisfy the MIS Quarterly standard for DSR contributions.

---

### [Q36] Hevner, March, Park, & Ram. (2004). Design Science in Information Systems Research.
- **Authors:** Alan R. Hevner (Univ. South Florida), Salvatore T. March (Vanderbilt), Jinsoo Park (Korea Univ.), Sudha Ram (Univ. Arizona)
- **Year:** 2004
- **Type:** P (Journal Article, MIS Quarterly Vol. 28 No. 1, pp. 75–105)
- **DOI:** https://doi.org/10.2307/25148625
- **Citations:** ~10,000+
- **Relevance:** 4/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What this is:** Seminal MIS Quarterly paper establishing DSR as a rigorous IS research paradigm. Not empirical — conceptual framework and normative guidelines. The canonical reference for DSR methodology.
- **Core framework:** Two IS research paradigms exist side by side: (1) behavioral science (explains/predicts human/organizational phenomena) and (2) design science (creates innovative artifacts to extend human/organizational capabilities). Both are necessary and complementary.
- **Four IT artifact types (cite-ready definitions):**
  1. Constructs — vocabulary and symbols; define the language of the problem and solution
  2. Models — abstractions and representations; connect problem and solution space
  3. Methods — algorithms and practices; guide the artifact construction and evaluation process
  4. Instantiations — implemented and prototype systems; demonstrate feasibility in a working system
- **Three-cycle framework:**
  - Relevance cycle: connects IS research to the environment (business needs, organizational problems, people, technology)
  - Rigor cycle: connects IS research to the knowledge base (foundations, methodologies, prior theories)
  - Design cycle: core iterative build-and-evaluate loop between the two
- **Seven DSR guidelines (cite-ready, verbatim from Table 1):**
  1. Design as an Artifact — must produce a viable artifact (construct, model, method, or instantiation)
  2. Problem Relevance — develop technology-based solutions to important and relevant business problems
  3. Design Evaluation — utility, quality, and efficacy must be rigorously demonstrated via well-executed evaluation methods
  4. Research Contributions — clear and verifiable contributions in areas of artifact, foundations, and/or methodologies
  5. Research Rigor — rigorous methods in both construction and evaluation of the artifact
  6. Design as a Search Process — search for effective artifact using available means to reach desired ends while satisfying problem environment constraints
  7. Communication of Research — must be presented effectively to both technical and management audiences
- **What the paper does NOT do:** Not an empirical study. No validation of the guidelines themselves against a sample of IS papers. Guidelines are normative, not prescriptive rules.
- **Precise citation note:** The paper was published March 2004 in MIS Quarterly Vol. 28 No. 1. The DOI 10.2307/25148625 is the JSTOR stable link. Always cite with full journal reference for legitimacy.
- **Core Thesis Relevance:** Primary methodological citation for Chapter 3 (Forschungsdesign). The NADF is a DSR artifact of type "method" (Guideline 1). The two-iteration design cycle directly maps to Iteration 1 (NADF construction) and Iteration 2 (ALIC deployment). The UEF evaluation protocol operationalizes Guideline 3. Guideline 2 grounds the practical relevance via the SME use case. Co-cite with Gregor & Hevner [Q35] for positioning the knowledge contribution type.

---

## TIER 3 – Relevant Context Papers (Relevance: 3/5) — Continued

---

### [Q37] Zhu, K., Liu, Z., Li, B., Tian, M., et al. (2025). Where LLM Agents Fail and How They Can Learn From Failures.
- **Authors:** Kunlun Zhu, Zijia Liu, Bingxuan Li, Muxin Tian, Yingxuan Yang, Jiaxun Zhang, Pengrui Han, Qipeng Xie, Fuyang Cui, Weijia Zhang, Xiaoteng Ma, Xiaodong Yu, Gowtham Ramesh, Jialian Wu, Zicheng Liu, Pan Lu, James Zou, Jiaxuan You
- **Institutions:** UIUC, Stanford, AMD, OpenManus, University of Toronto
- **Year:** 2025
- **Type:** P (Preprint)
- **arXiv:** 2509.25370
- **URL:** https://doi.org/10.48550/arXiv.2509.25370
- **Relevance:** 4/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this paper is:** Analysis of LLM agent failure modes on 500+ trajectories from ALFWorld, WebShop, and GAIA. Produces the AgentErrorTaxonomy, the AgentErrorBench (200 annotated trajectories), and AgentDebug (a debugging framework). NOT a comparison of deterministic workflow vs. agent paradigms.
- **AgentErrorTaxonomy — 5 modules (verified):**
  1. **Memory:** false recall (hallucination), retrieval failure, oversimplification — distorts subsequent reasoning
  2. **Reflection:** progress misassessment, outcome misinterpretation — blocks course correction
  3. **Planning:** impossible actions, constraint ignorance, incoherent subgoals, inefficient plans — cascades into missteps
  4. **Action:** format errors, invalid actions, parameter errors, missing arguments — visible but often masks upstream errors
  5. **System-level:** tool execution errors, step limit exceeded, environment errors, LLM API misalignment
- **Error distribution from 200 annotated trajectories:**
  - Planning dominates: 78 instances
  - Memory: 38, Reflection: 39, Action: 22, System: 22
  - Most failures cluster at mid-trajectory steps (6–15) where early errors cascade
  - Inter-annotator agreement: Cohen's κ = 0.55
- **Key Insight:** Error propagation is the primary bottleneck — a single root-cause failure cascades through subsequent steps, compounding failures and making recovery without intervention nearly impossible.
- **AgentDebug results (verified):**
  - 24.3% vs. 0.3% All-Correct accuracy (critical error detection)
  - 45.0% vs. 28.0% Step accuracy
  - Up to 26% relative improvement in task success across ALFWorld, GAIA, WebShop
  - ALFWorld: GPT-4o-mini success 21→55; Qwen3-8B: 48→74; Qwen3-Next-80B: 60→84
- **Mapping to thesis failure mode framing (important):**
  - "Hallucination-induced cascades" → Memory module errors (false recall + oversimplification) that propagate
  - "Tool-use errors" → Action module (parameter errors, format errors) + System module (tool execution errors)
  - "Planning brittleness" → Planning module (constraint ignorance, impossible actions, incoherent subgoals)
  - This mapping is valid — the three thesis failure modes are accurate summaries of the 5-module taxonomy
- **What the paper does NOT do:** Does NOT compare deterministic workflow nodes vs. agent nodes. The argument for deterministic node superiority (H3, H4) must use this paper as indirect evidence: agents exhibit these failure modes; deterministic nodes structurally avoid them.
- **Core Thesis Relevance:** H3 grounding (agent brittleness — planning brittleness, tool-use errors on distributional shift). H4 grounding (deterministic nodes have no planning or reflection module → structurally absence of goal drift). APS weights co-citation alongside Liu et al. [Q05] and Kapoor et al. [Q13].

---

### [Q38] Khramogin, A. (2026). LLM Agent Orchestration Patterns: Architectural Frameworks for Managing Complex Multi-Agent Systems.
- **Authors:** Alexey Khramogin
- **Year:** 2026
- **Type:** B (Technical Blog Article, C# Corner)
- **URL:** https://www.c-sharpcorner.com/article/llm-agent-orchestration-patterns-architectural-frameworks-for-managing-complex/
- **Relevance:** 3/5
- **Abstract:** Practitioner-oriented overview of LLM agent orchestration patterns including hierarchical orchestration, DAG-based workflows, event-driven agents, and hybrid patterns. Draws on production experience to discuss trade-offs between centralized workflow control and distributed agent autonomy.
- **Key Contributions:**
  - Practitioner perspective on orchestration pattern selection
  - Concrete pattern descriptions with implementation considerations
  - Trade-off analysis between control and flexibility
- **Core Thesis Relevance:** Grey literature supplementing the engineering practitioner perspective; relevant to practical implications (Section 5.3). Use with appropriate caveats about source type.

---

### [Q39] Koubaa, A. (2025). Agent Operating Systems (Agent-OS): A Blueprint Architecture for Real-Time, Secure, and Scalable AI Agents.
- **Authors:** Anis Koubaa
- **Year:** 2025
- **Type:** P (Preprint)
- **DOI:** https://doi.org/10.20944/preprints202509.0077.v1
- **Relevance:** 3/5
- **Abstract:** Proposes Agent-OS as an operating system abstraction layer for AI agents, providing real-time scheduling, security isolation, and resource management analogous to traditional OS primitives. Argues that agentic AI systems require OS-level infrastructure for production deployment.
- **Key Contributions:**
  - OS-abstraction architecture for agent systems
  - Real-time scheduling and security frameworks for agents
  - Production deployment requirements for agentic AI
- **Core Thesis Relevance:** Background context for agent infrastructure complexity — relevant to cost and maintenance comparisons between workflow and agent paradigms.

---

### [Q40] Krishnan, N. (2025). Advancing Multi-Agent Systems Through Model Context Protocol: Architecture, Implementation, and Applications.
- **Authors:** Nithin Krishnan
- **Year:** 2025
- **Type:** P (Research Paper)
- **arXiv:** 2504.21030
- **URL:** https://doi.org/10.48550/arXiv.2504.21030
- **Relevance:** 3/5
- **Abstract:** Examines the Model Context Protocol (MCP) as a standardization layer for multi-agent systems. Analyzes how MCP enables interoperability between agent frameworks and tool providers, reducing implementation overhead. Discusses architectural patterns enabled by MCP including dynamic tool discovery and context sharing between agents.
- **Key Contributions:**
  - MCP as standardization layer for agent-tool interaction
  - Architecture patterns enabled by protocol standardization
  - Implementation guidance for MCP-based multi-agent systems
- **Core Thesis Relevance:** Relevant to system implementation (Phase 3) and the practical dimension of agent-tool integration. MCP is increasingly relevant for standardized tool use in both workflow and agent contexts.

---

### [Q41] Tang, Y., & Runkler, T. (2026). LLM-Based Agentic Systems for Software Engineering: Challenges and Opportunities.
- **Authors:** Yiying Tang, Thomas Runkler
- **Year:** 2026
- **Type:** P (Research Paper)
- **arXiv:** 2601.09822
- **URL:** https://doi.org/10.48550/arXiv.2601.09822
- **Relevance:** 3/5
- **Abstract:** Surveys LLM-based agentic systems applied to software engineering tasks. Covers code generation, debugging, testing, and documentation. Identifies key challenges: long-horizon reasoning, tool reliability, hallucinated code, and the gap between benchmark performance and production deployability.
- **Key Contributions:**
  - Domain-specific survey of agent systems for SE tasks
  - Challenge taxonomy: reasoning, reliability, hallucination
  - Comparison of workflow-style SE pipelines vs. agent-driven SE
- **Core Thesis Relevance:** Relevant to task corpus design — SE tasks (Q category 3 in forschungsdesign.md) are directly covered. Provides domain-specific evidence for both agent capabilities and limitations.

---

### [Q42] OECD. (2025). AI adoption by small and medium-sized enterprises: OECD discussion paper for the G7.
- **Authors:** Flavio Calvino, Marco Bianchini, Marguerita Lane et al. (OECD Secretariat — CFE, ELS, STI directorates)
- **Year:** 2025 (G7 IDTMM, December 2025, Montreal)
- **Type:** R (Policy/Government Report — NOT peer-reviewed)
- **DOI:** https://doi.org/10.1787/426399c1-en
- **Publisher:** OECD Publishing
- **Relevance:** 3/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What this is:** OECD discussion paper prepared at the request of Canada's 2025 G7 Presidency. Policy analysis and descriptive statistics — not empirical primary research. Based on OECD ICT Access and Usage by Businesses database and secondary sources.
- **Key Statistics (verified from executive summary):**
  - Large firms (250+ employees) using AI: 40%; medium SMEs (50–249): 20.4%; small firms (10–49): 11.9%
  - Large firms are more than 3× as likely as small firms to use AI
  - OECD-wide firm AI adoption: 5.6% (2020) → 14% (2024)
  - AI adoption in core business functions: 1.9% (Japan) to 6.1% (US) in 2024
  - Macro productivity potential: +0.2 to +1.3 percentage points in annual labour productivity growth (OECD estimate, next decade)
- **Four key enablers identified:** (1) connectivity, (2) AI-enabling inputs (quality data, compute), (3) skills, (4) finance
- **SME adopter taxonomy (4 categories):** AI Novices (embedded tools, peripheral tasks), AI Explorers (bespoke development), AI Optimisers (multi-function integration), AI Champions (AI embedded in strategy)
- **What the paper does NOT do:** No peer review. No causal evidence — all associations. No LLM/agent-specific analysis. No comparison of orchestration paradigms (workflow vs. agent). Figures are averages with cross-country comparability caveats.
- **Precise citation note:** The 11.9% and 40% figures are from the OECD ICT Access and Usage Database (2024 data). Cite as "OECD, 2025" with the specific figure — not as "most SMEs do not use AI."
- **Core Thesis Relevance:** Background empirical grounding for the SME deployment context in Discussion Section 6.3. The 3× adoption gap between large firms and small firms motivates why the NADF must account for SME-specific constraints (cost, expertise, data access). The 4-enabler framework maps to NADF design criteria: the "skills" enabler directly justifies workflow nodes for tasks where SMEs lack AI expertise.

---

### [Q43] Sánchez, E., Calderón, R., & Herrera, F. (2025). Artificial Intelligence Adoption in SMEs: Survey Based on TOE–DOI Framework.
- **Authors:** Esther Sánchez (ESIC University, Madrid), Reyes Calderón (University Pontificia de Comillas, Madrid), Francisco Herrera (DaSCI Research Institute, University of Granada)
- **Year:** 2025 (published June 9, 2025)
- **Type:** P (Peer-reviewed, Applied Sciences, MDPI — open access)
- **DOI:** https://doi.org/10.3390/app15126465
- **Relevance:** 3/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **Note on previous entry:** Author names were incorrect — corrected to actual names from PDF title page ("Esther/Reyes" vs. "Estefanía/Rafael"). Prior description of "empirical survey" was also inaccurate.
- **What this is:** 43-page conceptual/literature-based analysis — NOT a primary empirical study despite the title. No original survey data collected. Integrates TOE framework (Tornatzky & Fleischer, 1990) with selected DOI theory constructs. Enriched with secondary empirical case studies from published literature.
- **Theoretical framework:** TOE — Technology (readiness), Organization (capacity), Environment (external influence). Integrated with DOI attributes to explain SME-specific adoption dynamics.
- **10 challenges identified across TOE dimensions:** Data access limitations, skill shortages, cultural resistance to AI, infrastructure limitations, weak governance practices, cost uncertainty, regulatory complexity, integration with legacy systems, lack of explainability, vendor dependency.
- **Key contributions (verified):**
  - Framework explicitly expanded to include responsible AI governance and open-weight LLMs (LLaMA, DeepSeek-R1, Mistral, FALCON) as emerging SME-relevant technologies
  - 6-phase AI adoption roadmap for SMEs (conceptual — "has yet to be validated through field data," per the paper itself)
  - SMEs represent ~90% of all businesses and >50% of employment globally (cited from standard references)
- **What the paper does NOT do:** No primary data collection. No quantitative validation of the roadmap. No test of any AI system. No comparison of AI orchestration paradigms. The challenges are framework-derived, not empirically quantified.
- **Precise citation note:** Do not cite as providing adoption rate statistics — use OECD [Q42] for those. Cite for the TOE-DOI framework and the 10-challenge taxonomy. The roadmap is explicitly unvalidated.
- **Core Thesis Relevance:** Supports Discussion Section 6.3 (SME deployment implications). The TOE framework's "Technology readiness" and "Organizational capacity" dimensions map to NADF's rationale for deterministic workflow nodes: SMEs with low technical readiness are steered toward lower-complexity node configurations. Co-cite with OECD [Q42] and Finch & Butt [Q44] for the SME deployment context section.

---

## TIER 4 – Background/Contextual (Relevance: 2/5) — Continued

---

### [Q44] Finch, W. W., & Butt, M. (2025). Gaps in AI-Compliant Complementary Governance Frameworks' Suitability (for Low-Capacity Actors), and Structural Asymmetries (in the Compliance Ecosystem)—A Systematic Review.
- **Authors:** William W. Finch, Muhammad Butt
- **Year:** 2025
- **Type:** P (Peer-reviewed, Journal of Cybersecurity and Privacy, MDPI)
- **DOI:** https://doi.org/10.3390/jcp5040101
- **Relevance:** 2/5
- **Verification status:** ✅ Paper read (2026-03-09)
- **What was studied:** EU AI Act compliance gaps for low-capacity actors, specifically SMEs. Hybrid systematic-scoping review of n=37 sources. Five governance frameworks analyzed and compared: EU AI Act (Regulation EU 2024/1689), ALTAI (Assessment List for Trustworthy AI), ISO/IEC 42001, NIST AI RMF, OECD AI Principles.
- **How it was studied:** Systematic review methodology. Sources coded against compliance criteria across four EU AI Act risk categories: unacceptable risk (prohibited), high-risk, limited risk, minimal risk.
- **Key Findings (verified):**
  - Central concept: "compliance asymmetry" — large enterprises absorb compliance costs through dedicated legal/technical teams; SMEs face disproportionate burden with no proportional relief mechanisms in any reviewed framework
  - ALTAI (the EU's self-assessment tool) overlooks 69% of known AI security vulnerabilities
  - GPAI systems including LLMs are governed under EU AI Act Articles 51–55
  - Fines: up to €35M or 7% of global annual turnover for high-risk violations; €15M / 3% for other violations
  - ISO/IEC 42001 is the most technically actionable framework for SMEs, but requires external certification costs
  - No reviewed framework provides a complete, self-contained compliance pathway for SMEs without significant legal or technical capacity
  - NIST AI RMF and OECD Principles are voluntary and lack enforcement mechanisms
- **What the paper does NOT do:** No empirical testing of any AI system. No comparison of workflow vs. agent paradigms. Purely regulatory and governance analysis. No field study of actual SME compliance attempts.
- **Precise citation note:** "Compliance asymmetry" is the paper's coined central concept — use this exact term when citing this paper's core contribution. When citing EU AI Act fines, always pair with the Regulation citation (EU 2024/1689) in addition to Finch & Butt.
- **Core Thesis Relevance:** Section 2.5 governance constraints and Discussion Section 6.3 (practical implications for SME deployment). Grounds the argument that NADF design must account for EU AI Act compliance: deterministic, auditable nodes reduce the probability of high-risk classification and lower compliance burden. The compliance asymmetry concept justifies why SMEs specifically benefit from the NADF's lower-complexity design choices. Primary peer-reviewed governance source in the thesis.

---

### [Q45] European Union. (2003). Commission Recommendation concerning the definition of micro, small and medium-sized enterprises.
- **Authors:** European Commission
- **Year:** 2003
- **Type:** R (Legal/Policy Document)
- **Source:** OJ L, Vol. 124. European Union.
- **URL:** http://data.europa.eu/eli/reco/2003/361/oj
- **Relevance:** 2/5
- **Abstract:** Official EU definition of SMEs: micro enterprises (<10 employees, ≤€2M turnover), small enterprises (<50 employees, ≤€10M turnover), medium enterprises (<250 employees, ≤€50M turnover). Used as the standard reference for SME classification in EU research and policy.
- **Core Thesis Relevance:** Required definitional reference if thesis uses SME as a target application context or discusses cost-access considerations for different firm sizes.

---

### [Q46] Rotter, J. B. (1966). Generalized expectancies for internal versus external control of reinforcement.
- **Authors:** Julian B. Rotter
- **Year:** 1966
- **Type:** P (Psychological Monographs)
- **DOI:** https://doi.org/10.1037/h0092976
- **Relevance:** 2/5
- **Abstract:** Introduces the Locus of Control (LoC) construct: the degree to which individuals believe that outcomes are controlled by their own actions (internal LoC) vs. by external forces (external LoC). Foundational social learning theory paper with broad application across psychology and organizational behavior.
- **Core Thesis Relevance:** Potentially applicable as theoretical lens for framing the workflow-agent distinction: workflows exert *internal control* (deterministic, designer-specified), agents operate with *external/adaptive control* (environment-driven decision-making). Use with care — requires explicit theoretical bridge to remain relevant. May be useful for framing user/operator trust and control preferences in human-AI systems.

---

## TIER 3 – Background / Context Papers (Relevance: 2/5)

---

### [Q49] Arunkumar, V., Gangadharan, G.R., & Buyya, R. (2026). Agentic Artificial Intelligence (AI): Architectures, Taxonomies, and Evaluation of Large Language Model Agents.
- **Authors:** Arunkumar V (Anna University, Tiruchirappalli), Gangadharan G.R. (NIT Tiruchirappalli), Rajkumar Buyya (University of Melbourne)
- **Year:** January 2026
- **Type:** P (arXiv Preprint — NOT peer-reviewed)
- **arXiv:** 2601.12560
- **Local copy:** `inputs/2601.12560v1.pdf`
- **Relevance:** 2/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this is:** Comprehensive survey and taxonomy of agentic AI architectures. Proposes a 6-dimension taxonomy organizing the field. Formal mathematical treatment of agent components. Not peer-reviewed.
- **6-Dimension Taxonomy (verified):**
  1. Core Components: Perception (text → multimodal), Memory (context → vector stores), Action interfaces, Profiling
  2. Cognitive Architecture: Linear (ReAct) → Hierarchical (Tree of Thoughts, ReAcTree) + Reflection (Reflexion)
  3. Learning: In-context (few-shot, CoT) → Fine-tuning (instruction tuning) → Alignment (RLHF, RLAIF)
  4. Multi-Agent Systems: Interaction styles (adversarial, cooperative) + Communication topologies (chain, star, mesh)
  5. Environments: Digital agents (browsers, OS), Embodied agents (robotics, games), Specialized domains
  6. Evaluation & Safety: CLASSic metrics (Cost, Latency, Accuracy, Security, Stability), Benchmarks (SWE-Bench, OSWorld), Prompt injection defense
- **Core mathematical model:** Agent as modified POMDP with: Perception (Φ), Memory update (µ), Cognitive Planning (Ψ), Action Policy (π) — formal integration of all prior frameworks
- **What the paper does NOT do:** No empirical experiments comparing architectures. No quantitative benchmark results for the paper's own taxonomy. Literature synthesis only.
- **Core Thesis Relevance:** Background reference for Section 2.1/2.2 if additional theoretical grounding needed. The CLASSic metrics (Cost, Latency, Accuracy, Security, Stability) partially overlap with the UEF dimensions. Low direct relevance — not cited in exposé v3.

---

### [Q50] Lei, Y., Xu, J., Liang, C.X., Bi, Z., Li, X., Zhang, D., Song, J., & Yu, Z. (2025). Large Language Model Agents: A Comprehensive Survey on Architectures, Capabilities, and Applications.
- **Authors:** Yiming Lei, Jiawei Xu, Chia Xin Liang, Ziqian Bi, Xiaoming Li, Danyang Zhang, Junhao Song, Zhenyu Yu
- **Year:** December 2025
- **Type:** S (Preprints.org preprint — NOT peer-reviewed)
- **DOI:** https://doi.org/10.20944/preprints202512.2119.v1
- **Local copy:** `inputs/preprints202512.2119.v1.pdf`
- **Relevance:** 2/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this is:** Comprehensive survey of LLM agents organized around a 4-dimension taxonomy. Not peer-reviewed.
- **4-Dimension Taxonomy (verified):**
  1. Reasoning-Enhanced: CoT, Tree of Thoughts, Graph of Thoughts, Self-Consistency, ReAct, Reflexion
  2. Tool-Augmented: API calling, Code execution, Web browsing
  3. Multi-Agent Systems: Role-playing, Debate & collaboration, Simulation
  4. Memory-Augmented: Context management, Retrieval-augmented, Hierarchical memory
- **Formal agent definition:** Agent as tuple A = (M, E, S, A, π) — standard formulation aligning with CoALA [Q08]
- **Key observation on evaluation:** AgentBench [Q05] and similar multi-dimensional benchmarks reveal high performance variance across domains — strong on some tasks, weak on others humans find trivial
- **What the paper does NOT do:** No new empirical results. No comparison of workflow vs. agent paradigms. Pure survey.
- **Core Thesis Relevance:** Background context only. The 4-dimension taxonomy is a simpler alternative framing to CoALA [Q08] for Section 2.3. Not directly cited in exposé v3. Use if additional survey citation needed for agent taxonomy background.

---

### [Q52] Webster, J., & Watson, R. T. (2002). Analyzing the Past to Prepare for the Future: Writing a Literature Review.
- **Authors:** Jane Webster (Queen's University), Richard T. Watson (University of Georgia)
- **Year:** 2002
- **Type:** P (MIS Quarterly Guest Editorial / Methodological Guide, Vol. 26 No. 2, pp. xiii–xxiii, June 2002)
- **Source:** MIS Quarterly, JSTOR Stable URL: https://www.jstor.org/stable/4132319
- **Relevance:** 3/5 (methodological reference, not content reference)
- **Verification status:** ✅ Paper read (2026-03-09)
- **What this is:** Canonical IS-field guide for conducting and structuring literature reviews. Published as a guest editorial in MIS Quarterly to establish standards for MISQ Review. Not an empirical study — a normative methodological guide. Widely cited as the standard reference for IS literature review methodology.
- **Core guidance (cite-ready):**
  - Concept-centric synthesis: organize around concepts, not around individual sources or authors; use a concept matrix rather than author-by-author summaries
  - Coverage: forward and backward citation search applied to each seed paper; both should be executed to ensure completeness
  - Structure: literature reviews should facilitate theory development and identify gaps, not produce "mind-numbing lists of citations"
  - For IS specifically: draw from multiple disciplines; the interdisciplinary nature of IS requires broader search scope than single-discipline fields
- **What the paper does NOT do:** Does not specify search term protocols, database coverage, or PRISMA-style flow diagrams. It is a general structural guide, not a step-by-step systematic review protocol.
- **Core Thesis Relevance:** Cited in Section 6.2 as the methodological basis for the literature review protocol. Replaces PRISMA (a medical/clinical review standard) as the IS-appropriate citation for systematic review methodology. The concept-centric approach directly maps to the thesis's organization of the literature review around the six node archetypes rather than around individual papers.

---

### [Q51] Alva, L.R., & Pandey, B. (2026). Agentic AI Systems in the Age of Generative Models: Architectures, Cloud Scalability, and Real-World Applications.
- **Authors:** Linga Reddy Alva, Bishwajeet Pandey
- **Year:** 2026
- **Type:** P (Peer-reviewed — Artificial Intelligence Review, Springer, Vol. 59, Article 88)
- **DOI:** https://doi.org/10.1007/s10462-025-11458-6
- **Local copy:** `inputs/s10462-025-11458-6.pdf`
- **Relevance:** 2/5
- **Verification status:** ✅ Paper read and verified (2026-03-09)
- **What this is:** PEER-REVIEWED framework proposal paper in Artificial Intelligence Review (Springer). Proposes a novel 5-module agentic AI framework (Perception, Planning, Memory, Execution, Communication) with fault-tolerant memory and dynamic re-planning. Empirically compared against AutoGPT, ReAct, and AutoGen.
- **5-Module Framework (verified):**
  1. Perception: multimodal input handling
  2. Planning: hierarchical decomposition, recursive feedback
  3. Memory: fault-tolerant, bidirectional anchoring, quantization for edge deployment
  4. Execution: real-time role adaptation, intent-conditioning pipelines
  5. Communication: declarative multi-agent coordination
- **Empirical results:** Framework outperforms AutoGPT, ReAct, and AutoGen on multi-turn consistency, tool invocation success rate, and goal completion ratio (exact numbers not extracted — read paper for specifics)
- **Key critique of existing frameworks (relevant for thesis positioning):** LangChain good for prototyping, lacks autonomous goal decomposition. AutoGPT brittle memory, hallucinated objectives, poor error recovery. ReAct limited to prompt patterns, no persistent memory. CrewAI lacks standardized state sharing and hierarchical planning.
- **What the paper does NOT do:** Does not compare deterministic workflow vs. agent at node level. Does not address SME context. Focused on cloud-edge deployment scalability.
- **Core Thesis Relevance:** The peer-reviewed status makes it citable as background context for Section 2 (architectural vocabulary). The critique of LangChain/ReAct/AutoGPT weaknesses could support the argument for the hybrid approach. Not directly cited in exposé v3.

---

## Sources NOT Accessible

| Source | URL | Status | Reason |
|--------|-----|--------|--------|
| Google Scholar | scholar.google.com | ❌ Blocked | CAPTCHA/bot protection |
| ScienceDirect | sciencedirect.com | ❌ Blocked | Requires institutional login + JS rendering |
| ACM Digital Library | dl.acm.org | ❌ Blocked | JavaScript-heavy, requires auth for abstracts |
| IEEE Xplore | ieeexplore.ieee.org | ❌ Blocked | Requires institutional access |
| Semantic Scholar API | api.semanticscholar.org | ❌ Rate limited (429) | Too many requests; key required for higher limits |
| Anthropic Research Index | anthropic.com/research | ✅ Accessible | Used successfully |

---

## Note on Duplicate Reference
**Anthropic (2024) "Building Effective AI Agents"** — This reference from the user's list is identical to **[Q01]** (Schluntz & Zhang, "Building Effective Agents", December 19, 2024). No new entry created; cite as [Q01].

---

## Citation Count Summary (for prioritization)

| Rank | Paper | Citations |
|------|-------|-----------|
| 1 | CoT Prompting (Wei et al., 2022) | ~10,000+ |
| 2 | Design Science in IS (Hevner et al., 2004) [Q36] | ~10,000+ |
| 3 | ReAct (Yao et al., 2022) | ~2,000+ |
| 4 | Generative Agents (Park et al., 2023) | ~2,000+ |
| 5 | Tree of Thoughts (Yao et al., 2023) | ~3,000+ |
| 6 | Toolformer (Schick et al., 2023) | ~1,500+ |
| 7 | Survey on LLM Agents (Wang et al., 2023) | ~1,200+ |
| 8 | AutoGen (Wu et al., 2023) | ~1,000+ |
| 9 | Rise of LLM Agents (Xi et al., 2023) | ~900+ |
| 10 | Reflexion (Shinn et al., 2023) | ~800+ |
| 11 | HuggingGPT (Shen et al., 2023) | ~800+ |
| 12 | CoALA (Sumers et al., 2023) | ~600+ |
| 13 | AgentBench (Liu et al., 2023) | ~500+ |
| 14 | Building Effective Agents (Anthropic, 2024) [Q01] | widely cited |
| 15 | Gregor & Hevner (2013) [Q35] | widely cited |
| 16 | FlowBench (Xiao et al., 2024) | ~100 |
| 17 | WorkflowLLM (Fan et al., 2024) | ~80 |
| 18 | AgentArch (Bogavelli et al., 2025) [Q29] | recent |
| 19 | Scaling Agent Systems (Kim et al., 2025) [Q30] | recent |
| 20 | Eval & Benchmarking LLM Agents (Mohammadi et al., 2025) [Q31] | recent |
| 21 | Architectures for Agentic AI (Nowaczyk, 2025) [Q32] | recent |
| 22 | LangChain vs. LangGraph (Sapkota et al., 2025) [Q33] | recent |
| 23 | Multi-agent Systems (Shaikh, 2026) [Q34] | recent |
| 24 | Single-agent or Multi-agent? (Gao et al., 2025) [Q28] | recent |
| 25 | When Single-Agent Fails (Li, 2026) [Q27] | recent |
