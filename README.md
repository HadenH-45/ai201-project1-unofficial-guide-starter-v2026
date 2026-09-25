# The Unofficial Guide

Haden Hicks, city_guides

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->
I picked the campus guides corpus. This system can use this corpus to answer questions like where to find a particular kind of food. It can also answer questions about the seasons and when certain areas will be the most lively.

## Chunking Strategy

**Chunk size:**
**Overlap:**

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `guide_accessibility.md#0` — produced by: `chunker.py::split_documents`

```
# Getting around the region with limited mobility

An honest assessment rather than a promotional one. Some of these places are
difficult and it is better to know in advance.

```

**Chunk 2** — source: `guide_corry_vale.md#6` — produced by: `chunker.py::split_documents`

```
# Corry Vale

## When to go

May to September. Outside those months the pub in the third village closes, the farm shop reduces its hours, and several footpaths become genuinely boggy rather than merely wet. The road is not gritted above the second village and is impassable in snow.

```

**Chunk 3** — source: `guide_givens_mill.md#3` — produced by: `chunker.py::split_documents`

```
# Givens Mill

## Eat and drink

A tearoom attached to the mill, open 10 to 4 daily except Tuesdays, which sells bread made from the flour ground twenty metres away and is the reason most people come. One pub, food served lunchtimes and Thursday to Saturday evenings.

```

**Chunk 4** — source: `guide_kestrelford.md#6` — produced by: `chunker.py::split_documents`

```
# Kestrelford

## When to go

Late spring and early autumn. The Saturday market runs year-round but is much reduced from November to February. August is busy with walkers. The single-track approach road is genuinely difficult in snow and the town can be cut off for a day or two most winters.

```

**Chunk 5** — source: `guide_regional_transport.md#1` — produced by: `chunker.py::split_documents`

```
# Getting around the region

## The railway

The line runs along the river valley, connecting Brightwater to the regional
hub in 50 minutes. Eleven services a day on weekdays, six on Sundays. The line
north of Brightwater closed in 1963 and everything beyond it is bus or car.

Tickets are cheaper booked the day before than on the day, and considerably
cheaper than that booked a week ahead. There is no ticket office at
Brightwater station outside weekday mornings; the machine on the platform takes
cards only.

```
## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**

"How is the seafood at Halden Bay?"

**Answer:**

The seafood at Halden Bay is genuinely fresh because the two harbour restaurants buy directly from boats that land in the early morning. 

Sources: `guide_halden_bay.md` and `guide_eating.md`.

Sources retrieved: guide_eating.md, guide_halden_bay.md


**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

I stick with the defaults of TOP_K = 5 and THRESHHOLD = 0.6.
I decided to stick with these because the responses I recieved properly answered the question and sourced them from the corpus. Additionally, after testing other values against them, it did not result in better responses.

| Question | In corpus? | Best distance |
|"Is the museum in Marchwood wheelchair accessible?"|Yes|0.503|
|"Is summer a good time to visit?"|Yes|0.478|
|"How is the seafood at Halden Bay?"|Yes|0.250|
|"Can I drive between towns?"|Yes|0.614|
|"Where's the best place to take a walk?"|Yes|0.535|

|"What is the capital of Mongolia?"|No|0.754|
|"How do I change the oil in a diesel engine?"|No|0.888|
|"Who won the 1994 World Cup?"|No|0.899|
|"What is the recommended dosage of ibuprofen for a headache?"|No|0.825|
|"How do I write a for loop in Rust?"|No|0.836|

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

     I asked Google Gemini to format the real output of the responses into the requested format that included only the text, source, and function it was created by. I did this for both evaluation runs.

     I asked Claude to help me implement a Hybrid Search method using the current store.py, and app.py. It guided me on navigating the files and functions, as well as what changes needed to be made.

**1.**

I asked Claude to make a rough draft for the chunking function and leave detailed core points of functional decision making left for me to decide on.

**2.**

I asked Claude to read the chunks that were returned after running the chunking function and whether it thought these chunks were appropriate given the corpus.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Chunks contain complete sentences and no chunk is under 20 characters in length. | 90% | 100% | 100% | 100% | MET |
| 5. All 5 contain the expected keyword or phrase that I defined| 5 of 5 | 5/5 | 5/5 | 5/5 | MET |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

| 1.

Yes, the city museum in Marchwood is step-free. 

Source: `guide_accessibility.md`

| 2.  

June is an excellent time to visit everywhere, and it is specifically highlighted as one of the best months for Brightwater and a "sweet spot" for Halden Bay and Pellew Sands (source: `guide_seasons.md`, `guide_brightwater.md`, `guide_halden_bay.md`, `guide_pellew_sands.md`). 

However, July and August vary: Brightwater goes quiet to the point of dullness, while Halden Bay and Pellew Sands become very busy, with Halden Bay facing major parking problems (source: `guide_seasons.md`, `guide_brightwater.md`, `guide_halden_bay.md`, `guide_pellew_sands.md`).

| 3.

The seafood at Halden Bay is genuinely fresh because the two harbour restaurants buy directly from boats that land in the early morning. 

Sources: `guide_halden_bay.md` and `guide_eating.md`

| 4. 

Yes, you can drive between towns, as most visitors drive between villages in Corry Vale and driving is an option to get to places like Givens Mill from Brightwater or Corry Vale (*guide_corry_vale.md*, *guide_givens_mill.md*).

| 5. 

Based on the documents, the old railway trackbed from Kestrelford is the best walking in the region for the effort involved (guide_regional_transport.md).

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | All three runs achieved 5/5, consistently exceeding the target threshold of 4 of 5. |
| 2 | Every answer names a source | MET | Every generated answer named a source across all three runs, reaching 5/5 on each attempt and meeting the target. |
| 3 | Gate stops out-of-corpus questions | MET | The relevance gate successfully filtered out-of-corpus questions 5/5 times across all three runs, exceeding the 4 of 5 target. |
| 4 | Chunks contain complete sentences and no chunk is under 20 characters in length. | MET | All retrieved chunks met both structural constraints across all three runs, achieving 100% against the 90% target. |
| 5 | All 5 contain the expected keyword or phrase that I defined | MET | The defined keywords or phrases were successfully present across all 5 questions in every run, hitting the 5/5 target. |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

I didn't miss any of the criterion I set. I don't believe my targets were set too low because they go beyond the bare minimum of having the correct answer, ensuring that it includes enough context surrounding the response and complete sentences to generate a complete idea. If I had to tighten one, then I would make the increase the minimum character's the chunk contains as 20 could be seen as a low bar.

## The Improvement

I added hybrid search.

**What I changed:**

I integrated hybrid search to the store.py file using BM25 keyword matching with the ChromaDB vector embeddings.

**Why I picked it:**

I picked hybrid search because even though I met all retrieval targets on the first evaluation, adding BM25 parse search ensures I have
<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

**1. Is the museum in Marchwood wheelchair accessible?**

> Yes, the city museum in Marchwood is step-free.
> Source: guide_accessibility.md

**2. Is summer a good time to visit?**

> Whether summer is a good time depends on the location: June is considered excellent everywhere or a sweet spot for places like Halden Bay and Pellew Sands. However, July and August are very busy in Halden Bay and Pellew Sands (bringing parking problems), while Brightwater goes quiet to the point of dullness during those months.
> (Sources: `guide_seasons.md`, `guide_halden_bay.md`, `guide_pellew_sands.md`, and `guide_brightwater.md`)

**3. How is the seafood at Halden Bay?**

> The seafood at Halden Bay is genuinely fresh, as the two harbour restaurants buy directly from the boats that land in the early morning.
> Sources: `guide_halden_bay.md` and `guide_eating.md`

**4. Can I drive between towns?**

> Yes, most visitors drive between the villages in Corry Vale (`guide_corry_vale.md`). You can also drive between Brightwater and Givens Mill (`guide_givens_mill.md`), and drive from Brightwater to the valley mouth of Corry Vale (`guide_corry_vale.md`).

**5. Where's the best place to take a walk?**

> According to the documents, the best walking in the region for the effort involved is the old railway trackbed from Kestrelford, which runs six miles on an easy gradient (guide_regional_transport.md).


| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Chunks contain complete sentences and no chunk is under 20 characters in length. | 90% | 100% | 100% | 100% | MET |
| 5. All 5 contain the expected keyword or phrase that I defined| 5 of 5 | 5/5 | 5/5 | 5/5 | MET |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

They run similarly with and without the hybrid search method. I think that this is likely because the RAG model was working well already and adding a hybrid search will only make it more consistent against a wider range of questions.

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

Nothing is broken at the moment all of my criterion are being met. I don't believe that this is due to having too weak of criterion.

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->

     If if had to rewerite a criteria I would change "All 5 contain the expected keyword or phrase that I defined" to instead require only the phrase and just have the phrase be less strict. This would balance out having the keyword be not restrictive enough while ensuring that the phrase isn't too restrictive of a criteria.
