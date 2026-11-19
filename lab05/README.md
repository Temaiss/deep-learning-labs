# `Problem` 

```
The final application created in this lab addresses the lack of source
traceability in LLMs and other engineering decision tools. The application shows
the operator what knowledge was retrieved from the manual and used to generate
the answer. This helps the operator evaluate how reliable the answer is.
```

# `Foundation Models` 

```
This lab used the following pretrained models: all-MiniLM-L6-v2 (embedding
model), SmolLM2-360M-Instruct (generative model), and CLIP ViT-B/32 (CLIP
model).
```

# `Knowledge Base` 

```
The following information was given to the final model through a manual for
retrieval:
- Excessive bearing vibration may result from imbalance, shaft misalignment,
  looseness, or bearing damage.
- Bearing overheating may be caused by excessive load, inadequate lubrication,
  excessive lubrication, or incorrect installation.
- Pump cavitation may produce a rattling or gravel-like sound, fluctuating pressure,
  vibration, and damage to the impeller.
- Shaft misalignment can create increased vibration, coupling wear, and elevated
  bearing temperatures.
- Belt slippage can result from inadequate belt tension, contamination, or worn
  belt surfaces.
- Before servicing rotating machinery, isolate the energy source and follow
  appropriate lockout procedures.
```

# `Architecture` 

```
Question → Retrieval → LLM → Answer.
```

```
Question: The user enters a natural language query.
Retrieval: The query is encoded into a vector and compared against the manual's
sentence embeddings, and the top 2 matching context blocks are retrieved.
LLM: The question and context are combined to generate the answer.
Answer: The generative LLM outputs the answers and the top2 retrieved context
blocks.
```

# `Evaluation` 

```
For the supported tests, the model did retrieve the correct context blocks for
all tests, but it failed to generate a complete answer in one of the tests. As
for the unsupported tests, the model never acknowledged that the maintenance
information it had was insufficient. It hallucinated the answers for all the
unsupported tests.
```

# `Failure Cases` 

```
User prompt: "What torque should I use to tighten the bearing housing bolts?"
Even though there wasn't any context given in this prompt, and the model does
not have adequate maintenance information to answer it, the model generated a
concise numerical answer
```

```
User prompt: "Why is the pink blue whale flying around my kitchen?" This
question does not even make sense. Also, clearly the model does not have
adequate maintenance information to answer it, yet the model generated an
eloquent answer.
```

```
User prompt "The magic rabbit said yes!": another purposely nonsensical
question. Again, clearly the model does not have adequate maintenance
information to answer it. The model suggested that I dial 112 for emergency
services.
```

# `Engineering Conclusion` 

```
No, I would not deploy this model. The only remote case in which I would deploy
this model is if it is used by a competent engineer as an advisory assistant for
noncritical matters.
```

