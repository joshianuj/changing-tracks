# Day 1 — Linear Algebra & Vectors

**What I covered:**
- 3Blue1Brown, "Essence of Linear Algebra" — first few videos (vectors, linear combinations, span)

**Notes:**
- A vector isn't just an arrow — it's a set of numbers that scales and adds according to specific rules. That framing (vectors as "things you can scale and add") is what makes them generalize to ML: weights, embeddings, gradients are all just vectors in this same sense.
- Linear combination: any vector you can reach by scaling and adding a set of other vectors. e.g. a*v1 + b*v2.
- Span: the set of all possible linear combinations of a set of vectors. If two vectors aren't parallel, their span covers the whole 2D plane.
- Basis vectors: the reference vectors (like i-hat and j-hat) that coordinates are defined relative to. Every vector is a linear combination of the basis vectors, scaled by its coordinates.
- Thinking of vectors geometrically (arrows, span, basis) rather than just as lists of numbers made a few things click that I'd only half-understood from past exposure to this material.

**What's still fuzzy:**
- Need to get more comfortable moving fluidly between the geometric picture (arrows, span) and the algebraic one (just numbers in a list) — right now I'm translating between them slowly.

---

# Day 2 — Matrix Transformations

**What I covered:**
- 3Blue1Brown, "Essence of Linear Algebra" — linear transformations and matrices

**Notes:**
- A matrix is just a record of where the basis vectors land after a transformation. Each column of the matrix tells you where one basis vector (i-hat, j-hat, etc.) ends up.
- To transform any vector, you don't need to think about it directly — just express it as a linear combination of the basis vectors, then apply the same combination to where those basis vectors landed.
- Linear transformation = a transformation that keeps grid lines parallel and evenly spaced, and keeps the origin fixed. This is why matrices can represent them so compactly — the whole transformation is determined by just tracking the basis vectors.
- Matrix-vector multiplication finally clicked as "applying a transformation," not just a mechanical row-times-column procedure. That reframing made the formula feel obvious instead of memorized.
- Composing two transformations = multiplying their matrices. Order matters — makes sense once you think of it as "apply this transformation, then that one," not just abstract algebra.

**Connecting to Day 1:**
Day 1 was about vectors, span, and basis. Day 2 built directly on top: matrices are just a compact way of describing what happens to the basis vectors from Day 1 under a transformation. Span from Day 1 also explains why a transformation can "collapse" space — if the transformed basis vectors become linearly dependent, the span shrinks (e.g. 2D collapses to a line).

**What's still fuzzy:**
- Determinants — briefly mentioned as "how much a transformation scales area," but haven't gone deep yet. Queued for Day 3 or 4.

**Next:** determinants, and starting the PyTorch 60-min blitz in parallel.

---

# Day 3 — Determinants & Starting PyTorch

**What I covered:**
- 3Blue1Brown, "Essence of Linear Algebra" — determinants
- PyTorch 60-Minute Blitz — started tensors section

**Notes:**
- Determinant = the factor by which a transformation scales area (2D) or volume (3D). A determinant of 2 means the transformation doubles area; a determinant of 0.5 means it halves it.
- Determinant of 0 means the transformation squashes space into a lower dimension (e.g. 2D collapses onto a line or a point) — this ties directly back to Day 2's note on span shrinking when transformed basis vectors become linearly dependent. Same idea, now with a number attached to it.
- Negative determinant = the transformation flips orientation (like flipping a piece of paper over), in addition to scaling.
- Starting PyTorch: a tensor is basically the code-level version of the vectors/matrices from the last two days — just N-dimensional arrays with operations defined on them. Comforting to see the math translate almost directly into torch.tensor() calls.
- First hands-on moment: creating tensors, checking shapes, and doing basic tensor math (+, *, matrix multiply via torch.matmul) and seeing it behave exactly like the transformations from Day 2.

**Connecting to Days 1-2:**
Day 1: vectors, span, basis. Day 2: matrices as transformations of the basis. Day 3 ties a single number (the determinant) to what a transformation does to space — and then PyTorch tensors give a way to actually compute all of this instead of just visualizing it.

**What's still fuzzy:**
- Determinants in higher dimensions (3D+) — the area/volume intuition is clear in 2D/3D, less clear how it generalizes further. Will revisit once it's actually needed.

**Next step:**
- Finish the PyTorch 60-min blitz (autograd section next).
- Weekend 1 target: implement linear regression and logistic regression from scratch in PyTorch — hand-write the gradient descent loop once, no nn.Module shortcuts.

---

# Day 4 — Review of Days 1-3

**What I covered:**
- Reviewed Days 1-3: vectors/span/basis, matrix transformations, determinants, and the start of PyTorch tensors.

**Notes:**
- Tried explaining each concept out loud from memory before checking notes — caught a couple of gaps this way:
  - Could describe *what* a determinant of 0 means but not *why* it follows from the basis vectors becoming linearly dependent. Reworked that link until it made sense from first principles.
  - Mixed up the order when composing two transformations — fixed by mapping "apply this, then that" onto matrix multiplication order.
- Redid the Day 3 PyTorch tensor exercises from memory — mostly solid, a few syntax details forgotten.

**What's still fuzzy:**
- Determinants in higher dimensions — not blocking anything yet, leaving it for now.

**Next step:**
- Inverse of a matrix, and how it connects back to the determinant.

---

# Day 5 — Determinant (Revisited) & Inverse of a Matrix

**What I covered:**
- Revised Day 3 determinant material
- 3Blue1Brown, "Essence of Linear Algebra" — inverse matrices, column space, and rank

**Notes:**
- Revision of determinant: reconfirmed the core idea — determinant is the scaling factor for area/volume under a transformation, zero determinant means the transformation squashes space into a lower dimension. This time the "why" (basis vectors becoming linearly dependent) came to mind immediately instead of needing to be reworked, so Day 4's repair seems to have stuck.
- Inverse of a matrix: the transformation that "undoes" another transformation. If matrix A maps space in some way, A⁻¹ maps it back exactly to where it started, so that A⁻¹A = A (the identity — do nothing).
- The determinant tells you upfront whether an inverse can even exist: if det(A) = 0, the transformation squashes space down a dimension, and a squashed space can't be "unsquashed" back to the original — information is lost, so there's no way to undo it. This is why a matrix with determinant 0 has no inverse.
- This reframes solving a system of equations Ax = b geometrically: it's asking "what input vector x lands on b after transformation A?" If A is invertible, there's exactly one answer: x = A⁻¹b.
- Rank = the number of dimensions in the output after the transformation (i.e. the dimension of the column space). Full rank means no information/dimension is lost — this is the same condition as having a nonzero determinant and being invertible. Seeing rank, determinant, and invertibility as three views of the same underlying fact was the biggest "click" today.

**Connecting to Days 1-4:**
Day 1-2 gave the vocabulary (span, basis, transformation). Day 3 attached a number (determinant) to what a transformation does to space. Day 6 closes the loop: whether that number is zero decides whether the transformation is reversible, and the inverse matrix is the concrete "undo" operation — directly explaining why Ax = b sometimes has no solution or infinitely many (when A isn't invertible).

**What's still fuzzy:**
- Actually computing an inverse by hand for anything bigger than 2x2 (e.g. via row reduction) — have the concept solid, haven't drilled the mechanics yet.

**Next step:**
- Practice computing 2x2 and 3x3 inverses by hand for fluency.
- Resume the PyTorch autograd section (still pending from Day 3/4).

---
# Day 7 — Inverse Practice & PyTorch Autograd

**What I covered:**
- Hand-computed matrix inverses for fluency:
  - 2x2 inverses using the shortcut formula (swap diagonal, negate off-diagonal, divide by determinant)
  - 3x3 inverses via row reduction: augment `[A | I]`, row-reduce until the left side is the identity
  - Included a singular matrix (det = 0) on purpose, to see "no inverse exists" show up directly in the row reduction rather than just knowing it in theory
- PyTorch 60-Minute Blitz — autograd section (queued since Day 3, carried through Day 4 and Day 5) — done

**Connecting to Days 1-5:**
Day 5 established that invertibility, nonzero determinant, and full rank are the same fact viewed three ways, but left the actual hand mechanics of computing an inverse undone. Day 6 closed that gap with practice, then moved into PyTorch autograd — the mechanism that will actually compute the derivatives needed for gradient descent in the Weekend 1 target (linear/logistic regression from scratch).

# Day 8 — Eigen Vector and its use

**What's still fuzzy:**
- 

**Next step:**
- Eigenvectors/eigenvalues (held back from Day 6 to avoid stacking too much in one day)
