Day 1 — Linear Algebra & Vectors

What I covered:

3Blue1Brown, "Essence of Linear Algebra" — first few videos (vectors, linear combinations, span)

Notes:

A vector isn't just an arrow — it's a set of numbers that scales and adds according to specific rules. That framing (vectors as "things you can scale and add") is what makes them generalize to ML: weights, embeddings, gradients are all just vectors in this same sense.
Linear combination: any vector you can reach by scaling and adding a set of other vectors. e.g. a*v1 + b*v2.
Span: the set of all possible linear combinations of a set of vectors. If two vectors aren't parallel, their span covers the whole 2D plane.
Basis vectors: the reference vectors (like i-hat and j-hat) that coordinates are defined relative to. Every vector is a linear combination of the basis vectors, scaled by its coordinates.
Thinking of vectors geometrically (arrows, span, basis) rather than just as lists of numbers made a few things click that I'd only half-understood from past exposure to this material.

What's still fuzzy:

Need to get more comfortable moving fluidly between the geometric picture (arrows, span) and the algebraic one (just numbers in a list) — right now I'm translating between them slowly.