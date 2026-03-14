Closest match: **not one model, but a hybrid stack**.

## Best matches to your graph

### 1. **DARPA KAIROS-style schema/event reasoning**

This is the **closest structural match**.

Why:

* your graph is built around **events, actors, roles, timelines, and recurring patterns**
* you are extracting and normalizing **historical motifs**
* you are trying to infer how an event chain may **unfold next**

That is very close to KAIROS’ public description: a schema-based system that identifies complex events, links sub-events and participants, sequences them temporally, and reasons over causal chains to help predict how events may unfold. ([darpa.mil][1])

**If your graph is asking:**
“Which recurring event-structure is this most like?”
then it is most KAIROS-like.

---

### 2. **IARPA HFC-style hybrid geopolitical forecasting**

This is the **closest forecasting workflow match**.

Why:

* your process sounds **human-in-the-loop**
* the graph is a reasoning aid, not an autonomous oracle
* the output is **qualitative probability / candidate branching**, not a hard prediction

HFC publicly describes **hybrid human-machine geopolitical forecasting systems** meant to combine machine processing with human reasoning for more accurate forecasts. ([IARPA][2])

**If your graph is asking:**
“Given the current pattern, what are the top next branches?”
then it is very HFC-like.

---

### 3. **IARPA ACE / superforecasting-style aggregation**

This is a match **if** you are combining multiple interpretations or weighting competing hypotheses.

Why:

* ACE is about eliciting, weighting, and combining probabilistic judgments
* that fits a workflow where multiple candidate narratives or branches are scored and updated over time

ACE is less about graph structure and more about **forecast calibration and aggregation**. ([IARPA][3])

**If your graph is asking:**
“Which branch is more likely, and how should confidence be updated?”
then ACE is relevant.

---

### 4. **GIDE-style indications-and-warning / anomaly detection**

This is the best match for the **“days in advance”** part.

Why:

* GIDE publicly described using AI/ML on global sensors plus commercially available information
* it looked for deviations from normal patterns
* those changes triggered attention and follow-on collection
* the stated goal was getting “days” of decision space in advance in bounded contexts

That is less like a narrative graph and more like a **precursor-detection engine**. ([U.S. Department of War][4])

**If your graph is asking:**
“What precursor anomalies suggest escalation is forming?”
then this is the closest public analog.

---

## What your system most likely resembles overall

From your description, your dual-layer graph is closest to:

> **KAIROS structure + HFC workflow + GIDE cueing**

In plain terms:

* **KAIROS** for event schemas, actor-role chains, temporal/causal structure
* **HFC** for human-guided geopolitical forecasting
* **GIDE** for anomaly/precursor cueing from large live data streams
* **ACE** only if you add disciplined confidence scoring and forecast aggregation

---

## The technical family underneath

Your setup also looks like this, conceptually:

### **Temporal multiplex knowledge graph**

* **mainstream layer** = observed/public narrative edges
* **shadow-rail layer** = hypothesized covert/latent edges
* **cross-layer links** = inferred influence, financing, coordination, proxy, cover, amplification

That is basically a **multi-layer event/relationship graph**.

### **Latent-state inference model**

Because the shadow layer is not directly observed, your process implicitly treats it like a **hidden state** behind visible events.

That makes it resemble:

* **hidden-state / latent-variable models**
* **dynamic Bayesian reasoning**
* **state-estimation over partial observations**

That part is my inference from your graph design, not a claim about a specific public DoD system.

---

## Ranked answer

If I had to rank the similarity:

1. **KAIROS**
2. **HFC**
3. **GIDE**
4. **ACE**

## One-line mapping

* **Pattern library / event motifs** → **KAIROS**
* **Human-guided branch prediction** → **HFC**
* **Precursor anomaly alerts** → **GIDE**
* **Confidence weighting / forecast calibration** → **ACE**

## Practical conclusion

Your graph is **not most similar to a generic LLM** or a simple classifier.

It is much closer to a:

> **schema-based, analyst-in-the-loop, temporal event graph with latent-layer inference and probabilistic branch scoring**

If useful, I can turn your current framework into a **clean model stack diagram**:

**ingest → entity/event extraction → dual-layer graph update → schema match → latent-rail hypothesis scoring → branch forecast → confidence update**

[1]: https://www.darpa.mil/research/programs/knowledge-directed-artificial-intelligence-reasoning-over-schemas "Knowledge-directed Artificial Intelligence Reasoning Over Schemas"
[2]: https://www.iarpa.gov/research-programs/hfc "IARPA - HFC"
[3]: https://www.iarpa.gov/research-programs/ace "IARPA - ACE"
[4]: https://www.defense.gov/News/Transcripts/Transcript/Article/2711594/northcom-commander-gen-glen-d-vanherck-conducts-press-briefing-on-north-america/ "
	NORTHCOM Commander Gen. Glen D. VanHerck Conducts Press Briefing on North American Aerospace Defense Command and U.S. Northern Command Global Information Dominance Experiments > U.S. Department of War > Transcript | U.S. Department of War
"
