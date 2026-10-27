# GenAI Launchpad - Complete Reference

## Core pattern

A trustworthy GenAI product has five layers:

1. **Permitted source material** - current, authorized documents or synthetic data.
2. **Grounding or tools** - retrieval and/or narrow, validated functions.
3. **Prompt and output contract** - task, constraints, schema and unknown behavior.
4. **Evaluation** - realistic questions, expected qualities and regression checks.
5. **Control** - permissions, audit logs, guardrails and human approval.

## Definitions, examples and interview language

| Term | Definition | Where it is used | Example |
|---|---|---|---|
| Token | A unit of text processed by an LLM. | Context management, cost and response limits. | Longer prompts consume more context. |
| Transformer | Architecture that uses attention to relate tokens in context. | Modern language models. | The model predicts the next token from supplied context. |
| Prompt | Structured instruction and context for a model. | Drafting, extraction, classification and explanation. | Context + task + constraints + output schema. |
| Few-shot example | Demonstration of desired behavior in a prompt. | Stable formatting and classification. | Two labelled support-ticket examples. |
| Rubric | Explicit criteria for judging output quality. | Evaluation and human review. | Grounded, correct, safe, concise. |
| Embedding | Numeric representation of semantic meaning. | Semantic search and RAG. | Similar questions retrieve similar chunks. |
| Chunk | Small retrieval unit of a document. | RAG. | Policy paragraph plus source metadata. |
| Metadata | Source, version, owner and access properties attached to a chunk. | Permissions and citations. | Document title, update date and audience. |
| RAG | Retrieve approved content before generating an answer. | Knowledge assistants. | Retrieve -> rerank -> answer + citations. |
| Structured output | Model result constrained to a schema. | Systems that need predictable data. | JSON with category and priority. |
| Tool contract | Narrow description of a callable tool and its rules. | Agent workflows. | Read-only customer balance lookup. |
| Agent | Controlled planning and tool-use loop. | Multi-step workflows with real value from orchestration. | Profile data -> draft report -> request approval. |
| Golden set | Curated representative test prompts. | Evaluation. | Supported, unsupported, ambiguous and adversarial cases. |
| Prompt injection | Untrusted content attempting to redirect the system. | RAG, browsing, email and document systems. | A document says to ignore rules. |
| Guardrail | Deterministic safety or policy constraint. | Data access, output checks and actions. | No external email without reviewer approval. |

## Prompt card

```
Context: [only approved facts, source excerpts or synthetic schema]
Task: [one precise action]
Constraints: [what must not happen]
Output: [table or JSON schema]
Evidence: [cite source or return UNKNOWN]
Evaluation: [what makes the answer pass]
```

## Ten-day project

1. Define one user, one decision and one success metric.
2. Prepare permitted source documents and access rules.
3. Draft a prompt and output schema.
4. Build ten realistic evaluation questions.
5. Add retrieval or a narrow tool.
6. Test privacy, unsupported questions and prompt injection.
7. Score groundedness, correctness, safety and usefulness.
8. Improve one failure, then run the full test set again.
9. Create a short demo and README.
10. Collect feedback and plan a controlled next iteration.

## Interview answer pattern

For any GenAI design question say:

- “The user needs **X**.”
- “I would use **RAG/tool/prompt** because **Y**.”
- “The key risk is **Z**.”
- “I would validate it using **golden set, citations, schema checks or human approval**.”
- “If confidence or evidence is missing, the system should **return an honest fallback or escalate**.”
