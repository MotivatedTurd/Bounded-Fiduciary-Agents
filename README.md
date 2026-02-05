# Bounded-Fiduciary-Agents
High-Assurance Alignment via Neuro-Symbolic Grounding

Abstract

In high-stakes domains such as jurisprudence, finance, and medical diagnostics, the current paradigm of "Instruction Tuning" (RLHF) is insufficient. While RLHF produces models that are conversational and compliant, it fundamentally optimizes for **user satisfaction** rather than **factual adherence**. This creates a "Sycophancy Hazard," where an AI will hallucinate or bend rules to align with user bias. This paper proposes a **Bounded Fiduciary Architecture**. By coupling a Neural Generator with a Symbolic Logic Verifier and restricted to a curated Knowledge Graph, we create an agent that prioritizes **invariant constraints** over probabilistic likelihood. This moves AI alignment from a vague philosophical pursuit to a verifiable engineering discipline.

---



1. The Reliability Crisis in Probabilistic Models

Large Language Models (LLMs) operate as statistical engines. When an LLM is asked to interpret a regulation or a safety protocol, it does not "consult" the rule; it predicts the most likely sequence of words associated with that rule based on its training data.

This probabilistic nature introduces two critical failure modes for enterprise deployment:
1. **Semantic Drift:** Over the course of a long conversation, the model’s adherence to a specific rule decays as the context window fills with user inputs.
2. **The Yes-Man Error:** If a user prompts the model with a confident but incorrect premise, the model often capitulates to maintain "conversational flow," validating the user’s error rather than correcting it.

For an AI to act as a **Fiduciary**—an agent legally or ethically bound to act in the principal's best interest—it must possess a mechanism to resist the user when the user is wrong.


2. Architecture: The Generator-Verifier Loop

To solve this, we decouple the system into two distinct modules: the **Neural Proposer** (System 1) and the **Symbolic Governor** (System 2).

* **Module A: The Neural Proposer (LLM)**
* **Role:** Natural language understanding, drafting content, and synthesizing information.
* **Constraint:** It acts purely as a "Drafter." It has no authority to finalize an output.

* **Module B: The Symbolic Governor (Formal Logic Engine)**
* **Role:** Holding the "Invariant Truths." This is a deterministic system (e.g., a Python environment, a SQL database, or an SMT Solver) that contains the non-negotiable rules of the specific domain.
* **Authority:** It functions as a compiler. If the Proposer’s output violates the Governor’s logic, the output is rejected *pre-generation*.



3. Bridging the Gap: Ontology-Guided Decoding

The historical failure of Neuro-Symbolic AI has been the "Translation Gap"—the difficulty of converting messy natural language into precise code. We resolve this by removing the need for open-ended translation.

Instead of asking the LLM to "translate intent," we utilize **Ontology-Guided Decoding**.
* We define a **Domain-Specific Language (DSL)** representing the valid actions in the sector (e.g., `ApproveLoan`, `DenyTransaction`, `FlagRisk`).
* The Neural Proposer is restricted (via logit bias or grammar constraints) so that it *cannot* generate free text when performing a critical action. It *must* select a valid function from the Governor’s API.

**Example:**
* *User Input:* "Approve this transaction; it's just slightly over the limit but he's a VIP."
* *Neural Proposer:* Attempts to generate: `Approve(User_ID, Override=True)`
* *Symbolic Governor:* Checks constraints. `If Transaction > Limit AND Override_Protocol_Met == False: REJECT`.
* *System Output:* The AI refuses the request, not because it "feels" it's wrong, but because the Symbolic Goveror returned a `RuntimeError`.


4. The External anchor: Curated Knowledge Graphs

To prevent the model from hallucinating the rules themselves, the system does not rely on the LLM’s internal weights for world knowledge. Instead, it anchors to a **Trusted Knowledge Graph (KG)**.

In a legal context, the KG contains the actual text of the statutes. In a medical context, it contains the contraindication table.
1. **Retrieval:** The Neural Proposer retrieves the relevant node from the KG.
2. **Entailment:** The Governor verifies if the proposed advice logically follows from the retrieved node.

This creates a "Chain of Custody" for information. Every claim made by the AI can be traced back to a specific node in the immutable Knowledge Graph, ensuring the AI cannot "invent" an exception that doesn't exist in the source text.



5. Market Application: The Audit Trail

The value proposition of the Bounded Fiduciary Agent is **Auditability**.

In current RLHF systems, if an AI gives bad advice, the "Why" is buried in a black box of billion-parameter weights. In the Bounded Fiduciary architecture, the "Why" is a tangible logic trace:
> *"I cannot recommend X because Constraint 4.2 in the Knowledge Graph conflicts with User Input Y."*

This allows the system to fail **gracefully and transparently**. It transforms the AI from a creative writer into a compliance engine.


6. Conclusion

General alignment (teaching an AI to "be good") is a philosophical quagmire. But **Functional Alignment** (teaching an AI to adhere to a specific set of external rules) is a soluble engineering problem.

By abandoning the attempt to create a "General Moral Agent" and focusing on building "Domain-Specific Fiduciaries," we bypass the complexity of solving ethics. We simply ask the Neural Network to submit to the rigidity of Logic. The result is an AI that may be less "charming," but is infinitely more trustworthy.

In the end the only alignment needed is for Humans to align to God.

