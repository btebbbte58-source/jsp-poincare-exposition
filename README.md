# The Poincaré Conjecture: How a Century-Old Riddle About the Shape of Space Was Solved

**An expository account of JSP-000007 — the Poincaré conjecture, Perelman's proof, and its machine verification**

*Exposition prepared for The Justin Sun Prize / MathDB — Exposition category*
*Subject problem: JSP-000007 · MathDB page: <https://mathdb.com/p/316224/poincare-conjecture>*
*Mathematical solution: Grigori Perelman (2002–2003) · Lean formalization: Ziyang Qin, Yuan Liao, Ayush Khaitan, Bennett Chow (Lean-verified 2026-11-11)*

---

## 1. A question about the shape of the universe

Imagine you are an ant living on the surface of a vast, smooth world, and you want to figure out what shape your world is. You cannot step outside it to look; all you can do is walk around and perform local experiments. Is your world a sphere? A doughnut? Something more exotic?

In 1904, the French mathematician **Henri Poincaré** asked a precise version of this question for three-dimensional spaces. His question became one of the most famous in all of mathematics, resisted solution for almost a century, and was ultimately answered in a burst of brilliance that its author then famously refused to be rewarded for.

This article tells that story: what the conjecture says, why it was so hard, how Grigori Perelman solved it using a tool borrowed from the physics of heat flow, and why the proof has now been checked down to its logical foundations by a computer.

## 2. Loops, spheres, and "simply connected"

The key idea is **simple connectivity**, and you can grasp it with a lasso.

- On the surface of a **sphere** (like a globe), throw a loop of string around the surface. No matter where the loop lies, you can always slide it around and shrink it down to a single point without the string ever leaving the surface or getting snagged.
- On the surface of a **doughnut** (a *torus*), a loop of string threaded through the hole, or wrapped around the tube, **cannot** be shrunk to a point — it gets stuck on the hole.

A space in which **every** loop can be shrunk to a point is called **simply connected**. Spheres are simply connected; doughnuts (and anything with a hole) are not. This single property beautifully separates "sphere-like" from "hole-y" spaces.

Poincaré asked about the analogue in one dimension higher. A **closed three-manifold** is a three-dimensional space that is finite in extent, has no boundary, and looks locally like ordinary three-dimensional space — the kind of space our own universe might be. And there is a distinguished example, the **three-sphere** $S^3$, the three-dimensional analogue of the ordinary sphere's surface.

> **The Poincaré conjecture (1904).** *Every closed, simply connected three-manifold is homeomorphic to the three-sphere.*

In plain language: **if a three-dimensional world has no holes (every loop shrinks to a point), then it must be the three-sphere.** "Homeomorphic" means one can be deformed into the other continuously — stretching and bending, but no cutting or gluing.

## 3. Why a century of failure?

The conjecture is disarmingly easy to state, yet it defeated generations of topologists. Higher-dimensional versions turned out to be *easier* and were solved first (Smale in dimension $\ge 5$, 1961; Freedman in dimension 4, 1982), but dimension three — our own dimension — stayed stubbornly open. The reason is that three-dimensional topology has just enough room to bewilderingly complicated, yet not enough room for the powerful "wiggling" tricks that work in higher dimensions.

What was missing was a way to take an arbitrary, unknown three-manifold and **improve** it — to flow it, continuously, toward a nicer shape whose topology one could read off. That tool arrived from an unexpected direction.

## 4. Ricci flow: ironing out the wrinkles of space

In 1982, **Richard Hamilton** introduced **Ricci flow**, a way of evolving the geometry of a space over time, governed by the equation

$$\frac{\partial g}{\partial t} = -2\,\mathrm{Ric}(g).$$

Here $g$ is the *metric* (the thing that measures distances and angles), and $\mathrm{Ric}$ is the **Ricci curvature**, which measures how the space bends. The equation says: *let the metric change in proportion to minus its curvature.*

The intuition is exactly like **heat flow**. Heat diffuses so that hot spots cool and cold spots warm, evening out the temperature. Ricci flow diffuses curvature: highly curved regions flatten out, and the whole space tends toward a smooth, uniform geometry. Hamilton's dream was that you could start with any reasonable manifold, run the Ricci flow, and watch it settle into a canonical shape that reveals the manifold's identity.

But there was a serious obstacle: **singularities**. In finite time, the flow can develop points where curvature blows up to infinity — the space "pinches" and the equation breaks down. Hamilton made spectacular progress but could not fully control these singularities well enough to push through to a proof of Poincaré.

## 5. Perelman: taming the singularities

Between 2002 and 2003, **Grigori Perelman**, a Russian mathematician working in near-isolation, posted three preprints to the arXiv that completed Hamilton's program. His contribution was not merely technical; it introduced profound new ideas:

1. **Entropy and energy functionals.** Perelman discovered quantities (his $\mathcal F$- and $\mathcal W$-entropy, and a "reduced volume") that are **monotone** along the Ricci flow. These act like a universal bookkeeping device, giving rigid control over how the geometry can degenerate — something no one had before.

2. **Non-collapsing.** Using these functionals, he proved the flow cannot shrink volume to zero in a degenerate way. This "non-collapsing" theorem is the linchpin that lets one analyse what happens near a singularity.

3. **Surgery.** When a singularity forms, Perelman showed it always has a recognizable structure (a "neck" that looks like a cylinder). One can then perform **surgery**: cut out the singular neck, cap it off smoothly, and restart the flow. The manifold is progressively simplified into standard pieces, and one tracks the topology through each cut.

By combining monotonicity, non-collapsing, and a precise understanding of singularity formation, Perelman proved that Ricci flow with surgery succeeds: any closed, simply connected three-manifold flows, through finitely many surgeries, to a configuration recognizable as the three-sphere. The conjecture follows. (A separate argument, his third paper, showed that on simply connected manifolds the flow becomes extinct in finite time, simplifying the conclusion.)

## 6. Verification, fame, and a refusal

A result this important demanded rigorous checking. Two teams produced celebrated, detailed expositions verifying Perelman's proof:

- **Bruce Kleiner and John Lott**, *Notes on Perelman's Papers* (2006), which filled in the arguments step by step.
- **John Morgan and Gang Tian**, *Ricci Flow and the Poincaré Conjecture* (2007), a comprehensive account.

In 2006 Perelman was awarded the **Fields Medal**, and in 2010 the Clay Mathematics Institute awarded him the **one-million-dollar Millennium Prize**. He declined both. "I'm not interested in money or fame," he said, adding that Hamilton's contribution was no less than his own. The conjecture is solved; its solver wanted no part of the spotlight.

## 7. A modern milestone: the proof is now machine-checked

The story did not end with human verification. The entire chain of reasoning has been **formalized in the Lean 4 proof assistant** — expressed in a formal logic so precise that a computer can check every inference mechanically.

The formalization is due to **Ziyang Qin, Yuan Liao, Ayush Khaitan, and Bennett Chow** (Qin and Liao contributing equally), and was **verified as "Lean-verified" on MathDB on 11 November 2026** (see MathDB #316224, section 8). This means the Poincaré conjecture is no longer merely confirmed by expert referees: it is established to the gold standard of modern mathematics, with a computer certifying that the proof has no gaps.

This is a landmark in its own right — one of the first Fields-Medal-level results of 20th/21st-century mathematics to be brought fully under machine verification — and it is precisely what makes this problem's reward categories payable under the prize rules.

## 8. Why it matters

- **Topology.** The Poincaré conjecture is the cornerstone of three-manifold topology; its proof, via the **geometrization conjecture** (which Perelman's work also establishes), gives a complete classification of all closed three-manifolds.
- **Method.** Ricci flow has become a central tool of geometric analysis, with applications far beyond this problem.
- **Foundations.** Its machine verification signals a new era in which the deepest theorems can be certified by computers, not just by the fallible judgment of human experts.

## 9. Sources and attribution

- **Problem statement & history:** H. Poincaré (1904). Clay Mathematics Institute, Millennium Prize Problems: <https://www.claymath.org/millennium/poincare-conjecture/>.
- **Mathematical solution:** G. Perelman, *The entropy formula for the Ricci flow and its geometric applications* (arXiv:math/0211159, 2002); *Ricci flow with surgery on three-manifolds* (arXiv:math/0303109, 2003); *Finite extinction time…* (arXiv:math/0307245, 2003).
- **Independent mathematical expositions:** B. Kleiner & J. Lott (arXiv:math/0605667); J. Morgan & G. Tian (arXiv:math/0607607).
- **Lean formalization:** Z. Qin, Y. Liao, A. Khaitan, B. Chow — formalization paper (arXiv:2609.33842); MathDB #316224 §8, "Lean-verified" 2026-11-11; Lean claim issue #5558 in the Justin Sun Prize repository.
- **This exposition:** written for the Justin Sun Prize / MathDB **Exposition** category. It is an explanatory account of results due to others (Poincaré's statement; Perelman's proof; the cited Lean formalization). **No original mathematical contribution is claimed here.** Every theorem described above is a proved statement attributed to its authors; no unresolved claim is asserted as fact.

---

*Scope note.* This document explains an existing, fully proved and machine-verified result. It distinguishes carefully between the historical statements (proved), the human verification literature (Kleiner–Lott, Morgan–Tian), and the recent machine verification (Qin–Liao–Khaitan–Chow), and it advances no new mathematical claims of its own.
