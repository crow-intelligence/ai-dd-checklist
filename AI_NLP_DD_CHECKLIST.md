<img src="img/ai-dd-checklist.svg" alt="AI DD Checklist" width="280">

# AI and NLP technical due diligence checklist

A practical checklist for investors evaluating AI and NLP startups. Maintained by [Crow Intelligence](https://crowintelligence.org/). Licensed CC BY 4.0.

## How to use this

This checklist is designed for early-stage venture investors in Central and Eastern Europe who need to assess whether an AI or NLP company is technically real, defensible, and compliant with the regulatory environment it will actually have to operate in. It assumes the reader is a smart non-engineer — a partner or principal who can read code but does not write it for a living. The questions are the ones a working NLP engineer would ask in a real diligence call, written so they can be passed to a target company as a self-assessment, used as a script for a technical session, or worked through with an external reviewer.

The checklist is opinionated by design. Where existing public checklists hedge, this one commits. If a question is marked as a red flag at a particular stage, that is a position, not a hedge. We expect investors to disagree with some of the calls, and that is fine — the value is in forcing the conversation, not in pretending there is one right answer.

It deliberately does not cover general software engineering hygiene that any tech diligence would catch (basic version control, ticketing, code maintainability), nor financial or commercial diligence beyond the points where unit economics and AI architecture intersect. It is also not an AI ethics document. Fairness, safety, and responsible use appear where they affect investability or regulatory exposure, not as standalone virtues.

### Severity tiers

Each question carries a tier in brackets after its number:

- **[T1] — Dealbreaker.** Missing or fudged answers should kill the deal at the relevant stage absent overwhelming compensating evidence.
- **[T2] — Material concern.** Addressable post-investment, but the gap should be reflected in the term sheet, conditions precedent, or 100-day plan.
- **[T3] — Maturity signal.** Not a blocker; presence indicates operational depth.

Tiers describe severity at the company's *current* stage. A T1 at Series B may be a T2 at seed.

### How to weigh findings

The tiers are a guide, not an algorithm. As a rough heuristic for assembling a verdict:

- **One or two T1 gaps** at the company's current stage — stop, unless there is overwhelming compensating evidence (a category-defining team, an unrepeatable customer, a regulatory tailwind).
- **Four or more T2 gaps** — price the risk into the term sheet, or convert one or two into conditions precedent and a 100-day plan.
- **A pattern of evasiveness, rehearsed answers, or refusal to show artefacts** — override the score. Founders who cannot say "we don't know" on a technical question are a category of their own.

### Stage-appropriate expectations

| Section | Pre-seed | Seed | Series A | Series B+ |
|---|---|---|---|---|
| 1 — Is the AI real? | expected | expected | expected | expected |
| 2 — Data | directional | expected | expected | expected |
| 3 — Evaluation | directional | expected | expected | expected |
| 4 — LLM-specific | directional | expected | expected | expected |
| 5 — Infrastructure / MLOps | n/a | directional | expected | expected |
| 6 — Security | directional | directional | expected | expected |
| 7 — Team / bus factor | expected | expected | expected | expected |
| 8 — Legal / EU AI Act | directional | directional | expected | expected |
| 9 — Governance / observability | n/a | directional | expected | expected |
| 10 — Commercial reality | directional | expected | expected | expected |

"Expected" means the artefact should exist and be inspectable. "Directional" means a credible plan and a plausible timeline are sufficient. "n/a" means do not penalise absence.

### Applicability beyond LLM-centric systems

This checklist is optimised for companies whose product depends materially on LLMs, retrieval-augmented generation, or agentic NLP. For startups building classical ML, computer vision, speech, or hybrid symbolic systems, **section 4 and parts of section 6** will be largely irrelevant — skip or adapt them. Sections **1, 2, 3, 5, 7, 8, 9, and 10** remain universal.

---

## Top 20: first-meeting triage

Use this list when you have one 30-minute session and need a fast read on the company. Each line points to the full question for follow-up. **Pick five to seven to ask live based on the nature of the pitch and the team's claims, and defer the rest to a written follow-up.** A "yes" everywhere does not mean the company is investable — use the full checklist before final commitment.

1. **[T1]** What kind of AI is this, in one sentence? *(see 1.1)*
2. **[T1]** Is the product a working system, or a demo dressed up as one? *(see 1.2)*
3. **[T1]** What stays valuable if the underlying foundation model becomes free and ubiquitous? *(see 1.4)*
4. **[T1]** Where did every dataset come from, and who owns it? *(see 2.1)*
5. **[T1]** Is there a real data moat, or is the underlying dataset commoditised? *(see 2.2)*
6. **[T1]** How does the company comply with GDPR for training data, retrieval indices, and prompt logs? *(see 2.7)*
7. **[T2]** Is there a closed loop of feedback data from production back into training? *(see 2.9)*
8. **[T1]** Is there a held-out, contamination-proof evaluation set? *(see 3.1)*
9. **[T1]** What metrics are tracked, and do they correspond to anything a customer cares about? *(see 3.2)*
10. **[T1]** Have dumb baselines been built and beaten? *(see 3.6)*
11. **[T1]** What is the company's defence against prompt injection, direct and indirect? *(see 4.1)*
12. **[T1]** How is hallucination measured, and what is the rate on the company's actual workload? *(see 4.3)*
13. **[T1]** What is the cost per successful task, not per call? *(see 4.6)*
14. **[T1]** What input and output guardrails are in place, and how are they tested? *(see 4.11)*
15. **[T2]** How is data, concept, and prediction drift detected in production? *(see 5.3)*
16. **[T1]** How are credentials and provider API keys managed, scoped, rotated, and budgeted? *(see 6.5)*
17. **[T1]** Where do prompts and responses physically reside, and does that match the customer contracts? *(see 6.6)*
18. **[T1]** Who can retrain the production model, and how many of those people are still at the company? *(see 7.1)*
19. **[T1]** Has the company classified each AI system against the EU AI Act's risk tiers, with documented rationale? *(see 8.1)*
20. **[T1]** What is the gross margin on the AI workload at current scale, and what does it look like at projected scale? *(see 10.2)*

---

## 1. Is the AI real?

### 1.1 What kind of AI is this, in one sentence? [T1]

*Why this matters:* Before anything else, force a precise answer — classical ML, fine-tuned model, prompted LLM, retrieval-augmented generation, multi-step agent, or some combination. Founders who cannot or will not answer this cleanly are either confused or hiding the architecture.
*What good looks like:* "We use GPT-4o through the Azure API with a retrieval layer over the customer's own documents and a small fine-tuned classifier for intent routing." Specific, boring, falsifiable.

### 1.2 Is the product a working system, or a demo dressed up as one? [T1]

*Why this matters:* Demos curated for investor screens routinely outperform production systems by an order of magnitude. The relevant question is not whether the demo works but whether real users hit real edge cases without the founders in the room.
*Red flag:* All shown outputs come from the same handful of inputs, or the founder always types the prompts.

### 1.3 If a model provider — OpenAI, Anthropic, Google, or whoever you depend on — changes terms, prices, or model behaviour, what happens to the product, and how quickly can the company route around it? [T1]

*Why this matters:* Provider-side changes — pricing, deprecation, output drift, regional availability — are the single most common cause of unplanned engineering work in AI startups today. The answer reveals how much of the company's value is borrowed, and how readily it can be re-grounded elsewhere.
*What good looks like:* A written runbook, a tested fallback path to at least one alternative provider, and a recent example of swapping a model in production. The eval suite has been run against at least two providers in the last quarter, with documented quality and latency deltas. A claim of multi-provider portability without that evidence is a claim, not a capability — most companies have prompts tuned to one provider's quirks, structured-output formats specific to one API, and evaluation harnesses that have never been run against an alternative.

### 1.4 What stays valuable if the underlying foundation model becomes free and ubiquitous? [T1]

*Why this matters:* The wrapper-versus-moat question, in plain form. If the answer is "nothing", the company is renting its competitive position from a lab whose interests are not aligned with the startup's.
*Red flag:* The answer is the prompt. Prompts are not defensible.

A second test, sharper: if foundation-model capability improves tenfold over the next eighteen months, what part of the company's product becomes irrelevant, and what part becomes more valuable? Founders who have not done this exercise are betting the company on the assumption that capability stops where it is now.

### 1.5 Is there an undisclosed human-in-the-loop doing the work the AI is credited with? [T1]

*Why this matters:* Offshore annotation teams, contractor review, and "AI-assisted" pipelines are legitimate at small scale, but become a fraud risk when investors are told the system is autonomous. Ask for the production logs and per-task wall-clock distribution.
*Red flag:* Median latency per "AI" decision is in minutes, not seconds, with no plausible inference-cost explanation.

### 1.6 If the word "AI" were removed from the pitch deck, would the business still make sense? [T2]

*Why this matters:* Borrowed from common practice and worth keeping. A well-built AI company solves a real problem; the AI is the means. A poorly-built one is a search for a problem the technology can be made to fit.
*What good looks like:* The pitch reduces to a clear customer pain, a measurable outcome, and a defensible reason this team will deliver it. The AI is one paragraph among many.

---

## 2. Data: provenance, licensing, and defensibility

This section is where we push hardest. Most AI companies overstate their data position. The job here is to find out whether there is a real moat — proprietary, growing, hard to copy — or whether the company is sitting on the same Common Crawl, scraped UGC, and public benchmarks as everyone else.

### 2.1 Where did every dataset used in training, fine-tuning, and evaluation come from, and who owns it? [T1]

*Why this matters:* A data provenance ledger should exist as a working document. If the company cannot list its sources, licensing terms, and acquisition methods on demand, it cannot defend itself in a copyright dispute or a regulatory audit.
*Red flag:* "Mostly scraped from the web" with no further detail at Series A or later.

### 2.2 Is there a real data moat, or is the underlying dataset commoditised? [T1]

*Why this matters:* The honest test — could a well-funded competitor reproduce this dataset in a quarter with a checkbook and a small engineering team? If yes, there is no data moat, regardless of what the deck claims. Public datasets, scraped UGC, and synthetic data on public seeds are anti-moats.
*What good looks like:* Proprietary data flowing in from customer workflows, regulated sources unavailable to general buyers, or a structural reason the data cannot be acquired at speed.

### 2.3 What is the cold-start story for a new customer, and how long does it take to become useful? [T2]

*Why this matters:* Many AI products work well only after they have absorbed weeks of a customer's data. That delay is hidden in the sales cycle and shows up later as churn. The cold-start curve is a real product metric and should be measured.
*Red flag:* Founders cannot answer how the system performs on day one of a new deployment versus day ninety.

### 2.4 If customer data is used to improve the system, is this disclosed, contractual, and isolated per tenant? [T1]

*Why this matters:* Cross-tenant data leakage through shared fine-tunes or shared retrieval indices is a serious commercial and legal exposure. Enterprise buyers increasingly require contractual confirmation that their data is not used to train models serving competitors.
*What good looks like:* Customer data is processed in tenant-isolated pipelines, training opt-in is explicit in the DPA, and there is technical evidence — not just policy language — that isolation holds.

### 2.5 Is synthetic data being used as a moat, or as a substitute for not having real data? [T2]

*Why this matters:* Synthetic data layered on top of a real proprietary seed is a genuine technique. Synthetic data with no real grounding usually means the team could not get access to the data that matters and is hoping the model will not notice.
*Red flag:* The training mix is dominated by synthetic data generated by the same family of model the product depends on. This closed loop is what researchers call model collapse: the synthetic distribution narrows the model's representation of the real one, and degradation compounds with each generation.

### 2.6 What is the company's exposure to copyright claims on training and fine-tuning data? [T1]

*Why this matters:* The legal landscape is moving and the picture is less clean than the 2025 headlines suggested. The June 2025 summary judgments in Bartz v. Anthropic and Kadrey v. Meta found that the act of training itself can qualify as fair use — but the subsequent USD 1.5 billion Bartz settlement was driven by Anthropic's separate liability for downloading pirated copies, which the court explicitly held was not protected. The European position under the DSM Directive Article 4(3) opt-out remains stricter than the US fair-use posture. The relevant question is what the company would have to disclose about both the training act and the acquisition channel if subpoenaed.
*Red flag:* Training corpora include scraped content from sites whose terms of service prohibit it, or content where rightholders have signalled an opt-out.

### 2.7 How does the company comply with GDPR for training data, retrieval indices, and prompt logs? [T1]

*Why this matters:* The right to erasure under Article 17 collides with the practical impossibility of selectively unlearning a record from trained model weights within the regulation's timelines. Hallucinated personal data, in particular, is hard to rectify under Article 16. Investors should understand which mitigations the company actually relies on — data minimisation, redaction at ingest, retraining cadences, retrieval-only architectures — and which they hope no regulator will test.
*What good looks like:* A documented lawful basis per processing activity, a retention schedule for prompt and response logs, a redaction pipeline for PII before any persistent storage, and a written position on Article 17 requests with named decision-makers. Retrieval-only architectures, where the underlying model never memorises personal data, are one of the few credible technical mitigations and worth probing for explicitly.

### 2.8 If labelling is required, who does it, and can the labelling pipeline scale? [T2]

*Why this matters:* Many NLP startups quietly depend on a small number of in-house annotators or a single BPO contract. Both are fragile. The cost, throughput, and quality of labelling determine the rate at which the model can improve.
*Red flag:* Inter-annotator agreement is not measured, or is measured and is below 0.6 Krippendorff's alpha on a non-trivial task, with no remediation plan.

### 2.9 Is there a closed loop of feedback data from production back into training or evaluation? [T2]

*Why this matters:* The strongest data moats compound — every user interaction makes the next better. Most claimed feedback loops are aspirational. Ask to see the path a single user correction takes from production to the next model version, and how long that path takes in practice.
*What good looks like:* A documented pipeline from production telemetry to a curated training or eval set, with an owner, a cadence, and evidence of at least one model improvement attributable to it.

---

## 3. Model and evaluation methodology

### 3.1 Is there a held-out, contamination-proof evaluation set? [T1]

*Why this matters:* This is the foundation of every other claim about model quality. Without a held-out set that has never been used for training or model selection, all reported metrics are unfalsifiable. The contamination problem is sharper for fine-tuned LLMs: the underlying foundation model may have seen MMLU, HumanEval, GSM8K, and TruthfulQA during pre-training, so claimed wins on public benchmarks are often measuring memorisation, not capability.
*What good looks like:* A private, recently-collected evaluation set built from data dated after the base model's training cutoff, with provenance documentation and a process for retiring items that leak. Test items have never been published.
*Red flag:* If there is no held-out test set at any stage past pre-seed, this is a serious problem and should be treated as one. There is no good answer here other than "yes, here it is."

### 3.2 What metrics are tracked, and do they correspond to anything a customer cares about? [T1]

*Why this matters:* Accuracy, F1, and BLEU are easy to report and frequently uncorrelated with user value. The more interesting question is whether the team has defined a task-success metric grounded in customer workflow, and whether they can show its correlation with a leading commercial signal such as retention.
*Red flag:* The headline metric is a benchmark score with no link to customer outcomes.

### 3.3 Are there regression tests on the evaluation set that gate every model or prompt change? [T2]

*Why this matters:* Without a regression gate in CI, every change is a roll of the dice in production. The presence of such a gate is one of the most reliable signals of operational maturity. (See 9.5 for how adversarial findings feed this gate.)
*What good looks like:* Every change to a model, prompt, or retrieval configuration triggers an automated eval run, with a fail threshold that blocks deployment, and a record of the last time the gate caught a regression.

### 3.4 Is the model evaluated out of distribution — by time, geography, customer, or demographic slice? [T2]

*Why this matters:* Aggregate metrics hide failures on the slices that matter. A system that performs at 92% on average and 60% on the largest customer is a system about to lose the largest customer. For CEE-focused products, linguistic slice coverage matters: an NLP system whose evaluation set is overwhelmingly English will fail in unpredictable ways across Slavic, Finno-Ugric, and Baltic languages, and the failure modes differ by family.
*What good looks like:* Slice-level metrics published as part of every model card, with clear thresholds for when a slice failure blocks release, and an explicit per-language breakdown for any product sold into multiple linguistic markets.

### 3.5 Is there human evaluation, with documented annotation guidelines and inter-annotator agreement? [T2]

*Why this matters:* For generative and subjective tasks, automated metrics are necessary but never sufficient. Ask for the annotation guideline document, the panel composition, and the agreement statistic. The absence of any of these is informative.
*Red flag:* The team uses LLM-as-judge as the primary evaluation method without a calibrated human anchor and without acknowledging the well-documented biases of judge models.

### 3.6 Have dumb baselines been built and beaten? [T1]

*Why this matters:* A surprising number of "AI" systems do not outperform a regex, a logistic regression, or a nearest-neighbour search on a sensible representation. Karpathy's recipe — overfit a single batch, train an input-independent baseline, beat a linear model — is a reliable filter.
*What good looks like:* The team can show, in writing, what the simplest possible solution achieves, and how the production system improves on it.

---

## 4. LLM-specific concerns

### 4.1 What is the company's defence against prompt injection, both direct and indirect? [T1]

*Why this matters:* OWASP ranks prompt injection as the top LLM risk for 2025, and the consensus among security researchers — including the UK NCSC — is that no foolproof prevention exists at the model level. The only credible defence is structural: separation of trust levels between system instructions, user input, retrieved documents, and tool outputs, with least-privilege tool design.
*What good looks like:* Tool calls that touch destructive actions or sensitive data require human confirmation, retrieved content is tagged as untrusted, and the team can describe a recent red-team finding and the fix.

### 4.2 If the product uses retrieval-augmented generation, what is the retrieval quality, measured separately from generation quality? [T1]

*Why this matters:* Most RAG failures are retrieval failures, but they are usually reported as generation failures because the team only measures end-to-end. Recall@k, MRR, and NDCG on a labelled query set are the relevant numbers, and they should be tracked over time.
*Red flag:* The team cannot produce retrieval-only metrics, or has never separated retrieval failure from generation failure in incident analysis.

### 4.3 How is hallucination measured, and what is the rate on the company's actual workload? [T1]

*Why this matters:* Generic factuality benchmarks are a starting point, not an answer. The relevant question is the hallucination rate on the company's own task, measured with claim decomposition (FActScore-style) or grounded faithfulness against retrieved context, and reported as a number with a denominator. For pure generation products without retrieval, adequate measurement looks like claim-level factuality scoring against a curated reference set, with a target rate and a denominator.
*Red flag:* The answer is "very low" without a methodology, or "we use GPT-4 to check GPT-4" without acknowledging self-preference bias.

### 4.4 What is the company's policy on system-prompt secrecy, versioning, and testing? [T2]

*Why this matters:* System prompts often contain business logic, guardrails, and occasionally credentials. They should be in version control, reviewed like code, tested against a regression suite, and never assumed to be confidential — system-prompt leakage is now a named OWASP risk for 2025 (LLM07).
*What good looks like:* System prompts live in a repository, have unit tests, and contain no information whose disclosure would be a material incident.

### 4.5 For agentic systems, what stops a runaway loop, a runaway cost, or a runaway action? [T1]

*Why this matters:* Agents fail in ways classical software does not — they retry, recurse, and consume tokens until something external stops them. Hard caps on steps, recursion depth, wall-clock time, and cost per task are not optional.
*Red flag:* No production cost ceiling per session, or no kill-switch on tool execution.

### 4.6 What is the cost per successful task, not per call, and how does it trend with usage? [T1]

*Why this matters:* Per-call cost is the wrong unit. The right unit is cost per successful unit of business value, with retries and failures included. The trajectory of this number under realistic workloads determines whether the gross margin survives scaling.
*What good looks like:* A finance-grade ledger of token, GPU, and tool-call cost normalised to a customer-facing outcome, with sensitivity analysis if a key provider raises prices by thirty percent.

### 4.7 How is embedding drift detected when a provider silently updates an embedding model, or when the corpus distribution shifts under a fixed model? [T2]

*Why this matters:* Mixed-version vectors in a single index produce nonsensical neighbourhoods, and the failure is silent — search just gets worse. Production teams pin embedding model versions in collection metadata and monitor neighbourhood stability over time. Neighbourhood stability is typically measured as recall on a fixed query pack over time, or drift in the top-k neighbour set for a stable seed.
*Red flag:* No version pinning on embeddings, or no recall metric tracked over time on a stable query pack.

### 4.8 What latency does the system actually deliver at P95 and P99, and how does it degrade at long context? [T2]

*Why this matters:* Streaming hides total latency. Time-to-first-token is a UX metric; time-to-task-completion is the business metric. Reasoning models have long pre-token delays that streaming cannot mask. Long-context performance degrades non-linearly.
*What good looks like:* P50, P95, and P99 reported separately for time-to-first-token and total task time, measured against real customer traffic.

### 4.9 What does fine-tuning add over prompting, and is the cost of the fine-tune justified by the lift? [T2]

*Why this matters:* Fine-tuning is often performed for reasons that retrieval or better prompting would solve more cheaply, and it locks the company into a model version. The relevant question is the measured lift versus the operational cost.
*Red flag:* Fine-tuned model in production without a head-to-head evaluation against a strong prompting baseline.

### 4.10 For systems that expose tools to the model — function calls, plugins, MCP servers, external APIs — what is the security posture of the tool-integration surface? [T1]

*Why this matters:* OWASP published an Agentic Top 10 in December 2025 alongside the LLM Top 10, and tool-integration vulnerabilities have already produced material incidents — CVE-2025-59536 (a Claude Code RCE triggered by opening a hostile repository) and the mcp-remote OAuth-proxy compromise that affected hundreds of thousands of developer environments are recent examples. The attack surface is distinct from the prompt-injection question in 4.1: it includes tool-output spoofing, authentication bypass on tool servers, indirect prompt injection through tool responses, and over-permissioned tool registrations.
*What good looks like:* A tool registry with authentication, signed tool manifests where available, scoped least-privilege credentials per tool, output validation as untrusted, and at least one penetration test against the tool surface specifically.
*Red flag:* A public MCP server with no authentication, or a tool catalogue the security team has never reviewed.

### 4.11 What input and output guardrails are in place — content policy, refusal behaviour, topical scoping, PII redaction — and how are they tested? [T1]

*Why this matters:* Guardrails are the runtime layer between the model and the customer, and they are a separate primitive from prompt-injection defence (4.1). Input guardrails enforce what the system will accept; output guardrails enforce what it will produce, refuse, or sanitise. The relevant question is not whether the team has a guardrails library installed — most do — but what the guardrails actually catch on the company's traffic, what they let through, and how the false-positive and false-negative rates are measured.
*What good looks like:* A defined policy in writing covering forbidden topics, refusal patterns, PII handling, and topical scope; a test set of adversarial inputs exercising each policy item; a measured precision/recall on guardrail decisions against that test set; and a path for users to appeal a refusal that fired in error.
*Red flag:* "We rely on the model's built-in safety", or guardrails that have never been tested against intentionally adversarial prompts on the company's own task.

---

## 5. Infrastructure, MLOps, and scale

### 5.1 Is there a model registry that links every production model to its training data, code, and evaluation results? [T2]

*Why this matters:* Without a registry, no one can answer simple questions — what is in production, what changed last week, what would we revert to. MLflow, Weights and Biases, SageMaker Model Registry, and equivalents are mature; the question is whether the discipline is observed, not whether the tool is installed.
*Red flag:* The production model is identified by a filename on a shared drive.

### 5.2 What does the deployment pipeline look like for a model or prompt change — shadow, canary, A/B, blue-green? [T2]

*Why this matters:* Deploying a model the same way as a config change is how silent regressions reach customers. A working pipeline includes shadow evaluation against live traffic, canary rollout, and one-command rollback.
*What good looks like:* The team can describe a rollback they actually executed, with its trigger and time-to-resolution.

### 5.3 How is data, concept, and prediction drift detected in production? [T2]

*Why this matters:* Models decay. The question is whether the team will know about decay before the customer does. Tools like Evidently, NannyML, Arize, and Whylogs are well established; the bar is monitored thresholds and alerting on a defined set of features and outputs.
*Red flag:* Drift is detected by customer complaints.

### 5.4 What observability exists for LLM calls — traces, prompts, responses, costs, errors? [T2]

*Why this matters:* LangSmith, Langfuse, Arize Phoenix, Helicone, and similar provide LLM-aware tracing. The question is whether traces tie to user sessions, whether costs are attributed per feature and per customer, and whether errors are classified.
*What good looks like:* A debugging session can be reconstructed end-to-end from traces alone, without a developer having to re-run the request.

### 5.5 What happens to cost and latency at ten times current load, and at one hundred times? [T2]

*Why this matters:* Linear extrapolation is rarely correct for AI workloads. Provider rate limits, GPU availability, and context-window economics introduce non-linearities. The team should have done the modelling.
*Red flag:* "We will buy more GPUs" without a written plan for capacity, contracts, or alternative providers.

### 5.6 Is there an incident-response runbook for AI-specific failures — bad outputs reaching customers, model unavailability, cost spikes, prompt-injection incidents? [T2]

*Why this matters:* AI incidents do not look like classical outages. They include silent quality regressions, mass hallucination events, and bills that arrive a week after the cause. The runbook should name owners, communication paths, and rollback authority.
*What good looks like:* At least one post-mortem of a real AI incident exists in writing, with concrete remediations tracked to closure.

### 5.7 Is training reproducible from a clean checkout — same data, same code, same hyperparameters, same result — end-to-end on the company's own infrastructure, today, by someone other than the original author? [T1]

*Why this matters:* If the model cannot be retrained at will, by someone other than its author, it cannot be debugged, audited, or improved. This is both a research-discipline question and a continuity question — the bus factor on reproducing the model is the bus factor on the company.
*Stage note:* Apply as T1 from Series A onward. At seed, a credible written plan for second-person reproducibility — and a date by which it will hold — is sufficient.
*Red flag:* The current production model was trained by a former employee whose laptop is no longer accessible, or reproducibility depends on a single person's environment.

---

## 6. Security

### 6.1 What is the application-security posture for AI-specific endpoints — input validation, output sanitisation, rate limits, authentication? [T1]

*Why this matters:* LLM output handed unvalidated to a downstream system is the route to XSS, SQL injection, SSRF, and remote code execution by way of the model. OWASP LLM05 — Improper Output Handling — captures this. The question is whether the team treats model output as untrusted by default.
*What good looks like:* Structured outputs validated against a schema, downstream consumers that assume hostile input, and rate limits scoped per user, per tenant, and per cost ceiling.

### 6.2 How are model artefacts and dependencies vetted — model hubs, weights, pickled files? [T2]

*Why this matters:* Hugging Face and similar hubs have a documented record of malicious models, often using Python pickle deserialisation for arbitrary code execution. Picklescan has known bypasses; safetensors is preferred where available. Model artefacts are dependencies and should be treated like package dependencies — pinned, signed, and scanned.
*Red flag:* Production loads pickled weights from a hub by name without commit pinning or scanning.

### 6.3 What is the exposure to model-extraction, model-inversion, and membership-inference attacks? [T3]

*Why this matters:* APIs that expose probabilities, confidence scores, or unbounded queries enable a competitor or adversary to clone the model or recover training records. This is most acute where training data is sensitive — health, finance, regulated text. For startups training on special-category personal data under GDPR Article 9 or commercially sensitive customer records, treat this as **T2** rather than T3, and demand an explicit threat model before proceeding.
*What good looks like:* Rate-limited APIs, output rounding or top-k truncation where it does not harm utility, and an explicit threat model for the data classes used in training.

### 6.4 How are training data and fine-tuning data protected against poisoning, particularly if any portion comes from user submissions or scraped sources? [T2]

*Why this matters:* OWASP LLM04 captures this. A handful of crafted records in a fine-tuning corpus can install a backdoor that no general benchmark will detect. The mitigation is provenance tracking, content filtering, and curation discipline, not vigilance.
*Red flag:* User-submitted content flows into fine-tunes without curation or anomaly detection.

### 6.5 How are credentials and provider API keys managed, scoped, rotated, and budgeted? [T1]

*Why this matters:* Leaked OpenAI or Anthropic keys are now a routine class of breach, and the financial exposure is immediate. Per-environment scoping, vault storage, regular rotation, and per-key budget caps are the minimum.
*What good looks like:* Keys are short-lived, rotated automatically, scoped to one environment and one purpose, and have a hard cost ceiling that pages an on-call when approached.

### 6.6 Where do prompts and responses physically reside, and does that match the company's contractual commitments to customers? [T1]

*Why this matters:* Data residency for inference is now a deal-breaker for European enterprise customers. A claim of EU residency that quietly routes through a US-hosted provider is a material misrepresentation. The OpenAI preservation order in the New York Times litigation is a live example of US litigation conflicting with European erasure rights, and the resolution lives in contract design, provider selection, and tested fallbacks — not in policy language.
*What good looks like:* Documented inference paths per customer tenant, written zero-data-retention agreements with providers where claimed, contractual residency claims that match the actual data flow, and a tested process for handling jurisdictional conflicts.

### 6.7 What is logged on every LLM call, where is it stored, for how long, who can read it — and how is logging reconciled with GDPR data minimisation? [T1]

*Why this matters:* Every prompt and response is potentially personal data, business confidential, or both. Observability is necessary; uncontrolled logging is a breach waiting to be reported. The Article 12 logging duties under the EU AI Act collide with the Article 5 data-minimisation principle of GDPR — the resolution is deliberate design, not silence.
*What good looks like:* Redaction at ingest, encryption at rest, role-based access, retention limits per data class, and a tested response to a regulator-style data subject access request.

### 6.8 What is the supply chain for the model and its components — base weights, fine-tunes, datasets, inference runtime, vector store, libraries? [T2]

*Why this matters:* OWASP LLM03 makes the AI supply chain a first-class concern. A dependency tree that no one has mapped is a dependency tree no one is defending.
*What good looks like:* A model SBOM that names every component, its version, its source, and its licence, updated when components change.

### 6.9 What is the concentration risk on non-LLM AI vendors — vector database, GPU cloud, annotation supplier, observability platform? [T2]

*Why this matters:* The model-provider conversation has matured (see 1.3), but the surrounding stack is just as concentrated and rarely scrutinised. A single vector-database vendor whose pricing or terms shift, a GPU cloud that throttles a region, an annotation BPO that loses a critical staff member — any of these can stall the company in ways that resemble a model-provider crisis but with no analogous playbook.
*What good looks like:* A named substitute for each critical vendor, a documented switching cost in person-weeks, and at least one drill or incident that exercised the alternative.

---

## 7. Team depth and bus factor

### 7.1 Who can retrain the production model, and how many of those people are still at the company? [T1]

*Why this matters:* The classical bus-factor question, sharpened. In NLP teams, retraining ability often concentrates in one person, and that person is often the one most likely to be poached.
*Red flag:* Bus factor of one on the model anyone is paying for.

### 7.2 Who owns the evaluation suite and the prompt library, and are they treated as first-class artefacts? [T2]

*Why this matters:* Eval sets and prompt libraries are usually owned by no one in particular and decay accordingly. The bus factor on these is as material as the bus factor on the code, and far less often examined. Ownership also predicts the company's *learning velocity* — how fast a user complaint becomes an evaluation item, how many experiments the team runs in a quarter, how long the loop takes from production signal to shipped improvement.
*What good looks like:* A named owner, a review cadence, and a recent commit history that shows active maintenance. Bonus signal: the team can quote experiment throughput, eval iteration cadence, and feedback-loop latency from memory, and can name three concrete things — a bug fix, an eval addition, a prompt or data change — that improved the system in the last thirty days, with evidence. Early-stage investing is more about trajectory than current quality, and trajectory is the question this answer reveals.

### 7.3 What is the mix of full-time employees, contractors, and freelancers on the technical team, and which key responsibilities sit with non-employees? [T2]

*Why this matters:* In Central and Eastern Europe, contractor and freelancer arrangements are common and often legitimate, but they affect IP assignment, continuity, and information security. The relevant question is whether any production-critical responsibility — model training, on-call, security response — sits with a contractor.
*Red flag:* The person who built the production model is on a service contract with no IP assignment clause and no notice period.

### 7.4 Is there a working balance between founder-engineers and operating engineers, or does the company depend on the founders to ship? [T2]

*Why this matters:* Founder-built systems are common at seed; founder-only systems at Series A are a scaling risk. The question is whether engineering hires can ship to production without founder approval on each release.
*What good looks like:* Recent meaningful releases shipped by non-founders, and a documented review process that does not bottleneck on a single person.

### 7.5 Does the hiring plan match the technical roadmap, and does the local labour market support it? [T2]

*Why this matters:* CEE talent pools are deep but specialised. A hiring plan that assumes ten senior LLM engineers in Budapest, Warsaw, or Bucharest within a quarter should be tested against the actual market — not the founder's optimism.
*Red flag:* The plan assumes hires the company has not hired before, in roles the company has not retained before, on timelines tighter than the company's track record supports.

### 7.6 Are employee and contractor agreements clear on IP assignment, particularly for work performed before the company existed? [T1]

*Why this matters:* University spin-outs, side-project commercialisations, and open-source contributions all carry IP-assignment risk. CEE jurisdictions vary on default assignment rules; the question is whether the assignment is explicit, written, and covers the work that matters.
*What good looks like:* A clean chain of IP assignment from every contributor to the company, including any pre-incorporation work.

---

## 8. IP, legal, and EU AI Act readiness

The EU AI Act — Regulation (EU) 2024/1689 — entered into force on 1 August 2024 and applies in stages: prohibitions and AI literacy from 2 February 2025, GPAI obligations and governance from 2 August 2025, most high-risk obligations from 2 August 2026, and the remainder from 2 August 2027. This section assumes the reader is familiar with the headline structure and probes for substance.

The Commission's Digital Omnibus on AI (proposed 19 November 2025, in trilogue at the time of writing) is likely to push the high-risk obligations deadline from 2 August 2026 to 2 December 2027 for stand-alone Annex III systems and 2 August 2028 for Annex I product-embedded systems, alongside amendments to AI literacy responsibility and a broadened legal basis for sensitive-data processing in AI development. The questions below are written against the original Regulation. Treat any post-Omnibus extension as an additional buffer for evidence-building, not as cause to defer it.

### 8.1 Has the company classified each AI system against Article 5 (prohibited), Article 6 with Annex III (high-risk), Article 50 (transparency), and the residual minimal-risk tier, with documented rationale? [T1]

*Why this matters:* Risk classification is the gateway to every other obligation. A company that has not done it cannot know what compliance costs it faces, and a misclassification is itself a risk.
*Red flag:* The team has not read Annex III, or treats classification as a legal task to be done later.

### 8.2 If any system is high-risk, where is the Article 11 technical documentation per Annex IV, and is it kept current? [T1]

*Why this matters:* Annex IV technical documentation is the regulator-facing record of what the system is, how it was built, and how it has been tested. Building it retroactively is harder than maintaining it, and authorities can request it.
*What good looks like:* A living document covering the system description, development process, design choices, training and validation data, monitoring, and conformity assessment route.

### 8.3 For high-risk systems, what evidence exists for the operational obligations under Articles 9 to 15? [T1]

*Why this matters:* Articles 9 (risk management), 10 (data governance), 12 (logging), 13 (deployer transparency), 14 (human oversight), and 15 (accuracy, robustness, cybersecurity) are concrete obligations that will be audited. The relevant question is whether the company can produce artefacts — not whether it agrees with the principles.

The operational artefact map for these articles is roughly:

| Article | Obligation | Typical artefact to ask for |
|---|---|---|
| 9 | Risk management | Risk register; mitigations linked to identified risks; review cadence |
| 10 | Data governance | Provenance records; bias and representativeness analysis per data class |
| 12 | Logging | Configured logs covering inputs, outputs, and operator actions; retention schedule |
| 13 | Deployer transparency | Instructions for use; performance and limitation disclosures; intended-use boundaries |
| 14 | Human oversight | Documented oversight design; intervention and override procedures; operator training |
| 15 | Accuracy, robustness, cybersecurity | Test results against defined metrics; adversarial robustness testing; security review |

*Red flag:* The answer is a policy document with no operational evidence behind it.

### 8.4 If the company provides or builds on a general-purpose AI model, what are its obligations under Article 53, and if applicable Article 55? [T2]

*Why this matters:* Article 53 imposes technical documentation per Annex XI, downstream-provider information per Annex XII, a copyright policy compliant with Article 4(3) of the DSM Directive, and a public summary of training data following the AI Office template. Article 55 adds adversarial evaluation, systemic-risk assessment, incident reporting, and weight cybersecurity for models above the 10²⁵ FLOP compute threshold or otherwise designated as having systemic risk.
*What good looks like:* If the company does not believe these apply, a written analysis of why. If they do, an evidence pack mapped to each obligation.

### 8.5 If a Fundamental Rights Impact Assessment under Article 27 is required, has it been done, and by whom? [T2]

*Why this matters:* The FRIA is a deployer obligation for certain high-risk systems used by public bodies and specified private deployers. It is not theatrical; it has a defined content set and must be communicated to the relevant authority.
*Red flag:* Customers in scope have not been told a FRIA is needed, or the company has assumed the customer will handle it without confirmation.

### 8.6 What is the company's exposure under Article 99 penalties, and has it been modelled against worst-case turnover? [T2]

*Why this matters:* Penalties scale to seven percent of worldwide annual turnover for prohibited-practice violations, three percent for most other obligations, and one percent for incorrect information to authorities. For SMEs and startups the lower of the two figures applies, but the absolute exposure can still exceed the company's enterprise value.
*What good looks like:* A written risk model, with named legal advisor, and contractual indemnification language reviewed against the exposure.

### 8.7 What is the open-source licence hygiene of every model, dataset, and library used in production? [T1]

*Why this matters:* Some open-weight models carry licences that restrict commercial use, downstream training, or redistribution. Some datasets carry research-only clauses. Some libraries are GPL-family and create derivative-work obligations on linked code. A clean inventory is the only way to know.
*Red flag:* The team has not read the licence on the base model in production.

### 8.8 What sectoral regulation — medical device, financial services, employment, education, child safety — applies on top of the AI Act, and is the company structured to comply? [T2]

*Why this matters:* The AI Act sits alongside existing sectoral regulation, not in place of it. A medical-device-classified AI system under MDR carries obligations the AI Act does not duplicate. Financial services AI in the EU operates under DORA and EBA guidance. The relevant question is whether the team has identified the stack, not just the top layer.
*What good looks like:* A regulatory inventory per market, per use case, with named external advisors where the in-house team is not specialised.

### 8.9 What is the company's position on ownership of AI-generated outputs — code, content, embeddings, or downstream artefacts — produced in or by the product? [T2]

*Why this matters:* The IP status of AI-generated outputs is unsettled across jurisdictions and contractually unsettled across customer contracts. Code generated by an assistant may carry licence obligations from training data; content generated for customers raises questions about who owns derivatives; embeddings of customer data sit ambiguously between processor and controller. The question is whether the company has *taken a position* in writing, not whether the position is bulletproof.
*What good looks like:* Customer contracts and internal acceptable-use policies that name an owner for each class of output, with a backstop indemnity sized to the realistic exposure.

---

## 9. Post-deployment governance, documentation, and observability

### 9.1 Does every shipped model have a model card covering intended use, out-of-scope use, training data, evaluation results, and known limitations? [T2]

*Why this matters:* Mitchell et al.'s model cards are now a baseline expectation in regulated procurement. The relevant question is whether the cards are accurate and current, not whether they exist as templates.
*What good looks like:* Cards that name out-of-scope uses explicitly and report intersectional metrics across the slices that matter to the business.

### 9.2 Does every training and evaluation dataset have a datasheet covering motivation, composition, collection, preprocessing, licence, and maintenance? [T2]

*Why this matters:* Gebru et al.'s datasheets are the equivalent for data, and the EU AI Act's Article 10 data-governance obligation operationalises much of the same content. A datasheet that does not exist is a dataset that cannot be defended.
*Red flag:* The largest training dataset has no documented provenance, consent record, or sensitive-attribute analysis.

### 9.3 Are model and prompt changes recorded in a change log, with the rationale, the evaluation evidence, and the approver? [T2]

*Why this matters:* Version control captures what changed; a change log captures why, and that is the artefact regulators, customers, and incoming engineers need. It also imposes a useful discipline at the moment of change.
*What good looks like:* A short, current log linked to the registry and the eval system, readable in five minutes by an outsider.

### 9.4 What user feedback channels exist, and how does feedback reach the team that can act on it? [T3]

*Why this matters:* Many AI products either over-collect feedback (every response gets a thumbs-up button no one looks at) or under-collect it (no in-product channel at all). The useful pattern is targeted, sampled, and reviewed.
*Red flag:* No one has read user feedback in the last month, or the feedback queue has more than a quarter of unreviewed items.

### 9.5 Are red-team and jailbreak exercises run on a defined cadence, and do findings flow back into the regression suite? [T2]

*Why this matters:* OWASP ranks prompt injection and jailbreak among the top LLM risks for 2025, and one-off red teams are theatre. The value is in continuous adversarial testing — internal or contracted — whose findings become permanent regression items in the gate from 3.3. Cadence, tooling, and the closed loop matter more than any single exercise.
*What good looks like:* A documented cadence, a tooling stack (NVIDIA garak, Lakera Guard, Microsoft AI Red Team patterns, internal harnesses, third-party assessments), and an audit trail showing findings closed.
*Red flag:* The last red-team exercise was the launch.

### 9.6 Is there a written AI policy covering staff use of third-party AI tools in the company's own work, especially for code and customer data? [T2]

*Why this matters:* Employees pasting customer data into ChatGPT, or using AI coding assistants whose outputs may carry licence obligations, are common sources of incident. The question is whether the company has decided what is allowed, said so in writing, and trained staff on it — Article 4 of the AI Act now requires the last of those.
*Red flag:* No written policy, or a policy written but never communicated.

---

## 10. Commercial and product reality

This section sits at the boundary between technical and commercial diligence and is included deliberately: AI architecture and unit economics are too entangled to assess separately.

### 10.1 What customer problem does the AI solve that a non-AI solution would solve materially worse, and how is "materially worse" measured? [T2]

*Why this matters:* AI is often deployed where heuristics, rules, or a search box would work. The relevant question is the measured advantage, not the architectural choice.
*What good looks like:* A head-to-head comparison against a non-AI baseline, with a clear win on a metric the customer pays attention to.

### 10.2 What is the gross margin on the AI workload at current scale, and what does it look like at projected scale? [T1]

*Why this matters:* AI-native gross margins routinely run 40 to 60 percent, against 75 to 85 percent for traditional SaaS. The interesting question is the trajectory — does scale improve margin through caching, batching, distillation, and provider negotiation, or does context inflation and model upgrades erode it?
*Red flag:* Founders cannot articulate gross margin at the AI workload level, or conflate it with overall company margin.

### 10.3 What is the customer evidence beyond pilots — paid deployments, renewals, expansion, and net revenue retention? [T2]

*Why this matters:* Pilots are cheap to win and easy to confuse with traction. The numbers that matter are paid renewals at original or higher price, expansion within an account, and how those compare to the pilot conversion rate.
*What good looks like:* A clear pilot-to-paid conversion rate, a named cohort of renewed customers, and a candid view of which pilots did not convert and why.

### 10.4 If a customer asked tomorrow to take the AI in-house or to a competitor, how hard would that be? [T2]

*Why this matters:* The answer reveals where the lock-in lives — in workflow, in data, in integrations, or nowhere. "Nowhere" is a poor answer for an enterprise AI company.
*Red flag:* Lock-in depends on the customer not realising they could switch.

### 10.5 What do customers actually do with the AI's output, and do they trust it appropriately? [T2]

*Why this matters:* Over-trust and under-trust are both failures. A system whose output is rubber-stamped is a liability waiting to fire; a system whose output is always overridden is a system the customer is paying not to use. The behavioural question is more important than the accuracy question.
*What good looks like:* The team has measured override rates, can name the cases where users defer too readily, and has UX patterns — citations, confidence indicators, refusal affordances — designed for calibrated trust.

### 10.6 Can the company articulate, in plain language to a non-technical buyer, what the system cannot do? [T2]

*Why this matters:* The teams that can do this tend to have customers who trust them and stay; the teams that cannot tend to over-promise and churn. It is also a fair test of whether the team understands its own system.
*What good looks like:* A short, written list of out-of-scope use cases that the company actively turns away.

### 10.7 How much custom engineering is required to integrate this AI into a customer's existing systems and data, and who does that work? [T1]

*Why this matters:* Many AI startups die in implementation, not in selling. A model that requires three months of bespoke data engineering on every deployment is a consulting business with a model attached, and the gross margins reveal it. The question is the *unit* of integration work — measured in person-weeks, paid by whom, charged how — and how that number trends as the customer base grows.
*What good looks like:* A bounded, declining time-to-value per deployment, a clear split between product surface and per-customer work, and a candid view of which customers required disproportionate engineering and why.

---

## Appendix A: Glossary

Short, non-specialist definitions for the technical terms used in this checklist.

- **Claim decomposition** — Breaking a generated answer into individual factual claims, each scored separately for accuracy. The basis of FActScore-style hallucination measurement.
- **DPA** — Data Processing Agreement. The contract between a controller (the customer) and a processor (the AI vendor) under GDPR Article 28.
- **DSM Directive** — The EU's Digital Single Market copyright directive (2019/790). Article 4(3) gives rightholders the option to opt out of text-and-data-mining of their content.
- **Embedding drift** — The phenomenon where vector representations of similar content shift over time, either because the embedding model has been silently updated by its provider, or because the underlying corpus distribution has changed under a fixed model.
- **FActScore** — A method for measuring factuality of generated text by decomposing it into atomic claims and verifying each against a reference source.
- **FRIA** — Fundamental Rights Impact Assessment. A pre-deployment assessment required under Article 27 of the EU AI Act for certain high-risk systems used by public bodies and specified private deployers.
- **GPAI** — General-Purpose AI; the EU AI Act's term for what the lab and research community call foundation models. Distinct from "AI system" in the Act. Article 53 imposes baseline obligations; Article 55 adds heavier ones for systemic-risk models.
- **Krippendorff's alpha** — A statistical measure of agreement between annotators on a labelling task; ranges from −1 to 1, with conventional thresholds at 0.6 (acceptable) and 0.8 (good). More robust than Cohen's kappa for multi-annotator settings.
- **LLM-as-judge** — Using an LLM to evaluate the output of another LLM. Convenient at scale, but well-documented to suffer from self-preference bias, length bias, and position bias.
- **Model collapse** — Progressive degradation when models are trained on data generated by earlier models. The synthetic distribution narrows the model's representation of the real one, and the loss compounds across generations.
- **MRR** — Mean Reciprocal Rank. The average reciprocal of the position of the first relevant result across a set of queries; a quick read on whether the right answer is near the top.
- **NDCG** — Normalised Discounted Cumulative Gain. A ranking metric that rewards correct items at higher positions in a result list. Standard alongside Recall@k and MRR for retrieval evaluation.
- **Neighbourhood stability** — The degree to which the top-k nearest neighbours of a fixed query in a vector index remain consistent over time. Measured by recall on a stable query pack or drift in the top-k neighbour set for a stable seed.
- **P95 / P99** — The 95th and 99th percentiles of a latency distribution. The customer experience that the worst-served 5% (and 1%) of requests actually receive — and where degradation hides if you only report the median.
- **Recall@k** — The fraction of relevant items that appear within the top *k* retrieval results. The simplest retrieval-quality metric and the easiest one to track over time.
- **SBOM** — Software Bill of Materials. An inventory of every component in a system, its version, source, and licence. The "model SBOM" in this checklist extends the concept to model weights, datasets, and inference runtimes.
- **Shadow / canary deployment** — Deployment patterns that route traffic to a new model conservatively. Shadow runs the new model alongside the old without serving its output; canary serves a small percentage of real traffic to the new model and watches metrics before scaling up.
- **Time-to-first-token** — Latency between the request and the first token of the response. A UX metric, not a task-completion metric — streaming hides total latency behind it.

---

## Sources and influences

This checklist draws on the EU AI Act (Regulation (EU) 2024/1689), the NIST AI Risk Management Framework 1.0 and its Generative AI Profile (NIST AI 600-1), ISO/IEC 42001:2023, the OWASP Top 10 for LLM Applications (2025), MITRE ATLAS, and the Microsoft Responsible AI Standard v2. It builds on Mitchell et al.'s Model Cards, Gebru et al.'s Datasheets for Datasets, Breck et al.'s ML Test Score, and Andrej Karpathy's Recipe for Training Neural Networks.

## License and contributing

This work is published under a Creative Commons Attribution 4.0 International licence (CC BY 4.0). You may use, adapt, and redistribute it, including for commercial purposes, with attribution to Crow Intelligence and a link to the canonical repository.

Contributions are welcome. Open a pull request on the GitHub repository with a clear description of the change, a reason, and where applicable a citation. We are most interested in items the existing checklist gets wrong, items that have aged badly, and items that real diligence calls have shown to be missing. We are least interested in additions that restate a principle without giving an investor something falsifiable to ask about.

The canonical home of this checklist is the GitHub repository linked from [Crow Intelligence](https://crowintelligence.org/). Crow Intelligence offers an independent AI and NLP technical due diligence service for early-stage venture funds in Central and Eastern Europe. The checklist is a public artefact and is not a marketing document for that service.

## About the maintainers

**Zoltán Varjú** is an NLP engineer and architect with two decades in the field. He co-founded Complytron, a RegTech company applying AI to anti-money-laundering and KYC, which was acquired by SEON in 2023. He is a Manning Publications author on applied NLP and runs one of Hungary's longest-standing technical communities, an NLP meetup with over 2,500 members. His background combines philosophy and linguistics with applied data science, and he writes regularly on AI, cognition, and the practice of building NLP systems.

**Orsolya Putz, PhD** is a cognitive linguist and AI engineer, and an adjunct professor at the Technical University of Budapest (BME). Her doctorate is in cognitive linguistics, and her work joins cognitive science, decision intelligence, and applied AI — particularly the ways language and conceptual framing shape how organisations interpret what AI systems produce. Together with Zoltán, she leads Crow Intelligence's research and advisory work on the hard problems that come before and after the code: specification, evaluation, and interpretation.

---

<a href="https://crowintelligence.org/"><img src="img/crow-intelligence.svg" alt="Crow Intelligence" width="200"></a>
