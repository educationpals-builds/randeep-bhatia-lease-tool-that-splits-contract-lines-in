# The Five-Check Method

This document explains the audit framework used to evaluate whether a setup's checks actually split the work. The acronym **PRISM** captures the five principles.

---

## P — Partition the Space

Before testing anything, define the distinct regions your tool must handle. For a lease duty-splitter, this means identifying every clause structure that could contain multiple obligations: simple conjunctions, nested "provided that" conditions, exception phrases, and cross-references to other sections.

If you haven't partitioned the input space, you can't know which regions your checks actually cover.

---

## R — Run in Parallel

Each check should be able to run independently. Don't chain checks so that one must pass before another can execute. When checks run in parallel, a failure in one doesn't mask failures in others.

For duty-splitting: test party extraction separately from clause boundary detection separately from conditional-phrase handling. If they're fused, you can't isolate which component failed.

---

## I — Individuate the Pattern

Each check targets exactly one failure pattern. A check that looks for "wrong party assignment" and "missed clause boundaries" simultaneously tells you something broke but not what.

One check, one pattern. When it fails, you know precisely which capability is broken.

---

## S — Stitch the Spectra

After running checks independently, combine their results to see the full picture. A tool might pass party-extraction checks and pass boundary-detection checks but still fail when both operate on the same nested clause.

Stitching means running the checks together on realistic inputs after you've verified each works alone.

---

## M — Map What Each Head Sees

For every check, document exactly what input it receives and what output it produces. If you can't describe the transformation a component performs in isolation, you can't verify it works.

Mapping means: this component takes X, does Y, produces Z. No hidden state, no implicit dependencies.

---

## The Anti-Pattern: Collapse to Monochrome

The opposite of PRISM is treating the entire pipeline as a single black box. You feed in a lease clause, you get out a duty assignment, and you either trust it or you don't.

This is "collapse to monochrome" — all the distinct checks blur into one undifferentiated test. When it fails, you don't know where. When it passes, you don't know why.

The risk: a bug in one component gets masked by behavior in another. The first signal that something is wrong comes too late — like a partner signing a summary that puts repair duty on the wrong side.

---

## Applying PRISM

When auditing any setup that splits work across components:

1. **Partition** — List every input class the tool must handle
2. **Run in Parallel** — Verify each check can execute independently
3. **Individuate** — Confirm each check targets exactly one failure mode
4. **Stitch** — Combine results on realistic inputs
5. **Map** — Document what each component sees and produces

If any principle is missing, the audit identifies which check to add or isolate before shipping.
