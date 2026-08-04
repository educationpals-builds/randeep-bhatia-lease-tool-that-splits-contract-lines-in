# Verify: Lease tool that splits contract lines into separate duties

## What this verification confirms

When a stranger runs their own failing lease-splitting setup through `/play`, the tool must:

1. Surface the **ablation finding** — whether the duty-splitting component has been tested in isolation against the exact failure mode
2. Demand a **numeric measurement** for that finding (pass/fail count on isolated samples)

---

## Run the verification

### Step 1: Open /play with your own lease-splitting setup

Describe:
- The tool you're auditing (what it's supposed to split)
- The failure mode you've observed (e.g., nested clauses merging duties)
- Three real contract lines where it fails

### Step 2: Confirm the tool walks the ablation check

The audit must ask whether you have run the splitting component **alone** against your failing inputs — not just whether the full pipeline produces correct output.

If the tool skips this question or accepts "the full tool works fine" as an answer, verification fails.

### Step 3: Confirm the tool demands a number

The audit must require a specific measurement for the ablation check:

- **Acceptable:** "Pass/fail count on isolated split test: ___"
- **Not acceptable:** "Have you tested it?" (yes/no with no count)

The worked example shows the standard:

> Watch: pass/fail count on the isolated three-sample split test. Threshold: must be 3/3 before ship. Priya owns running it — without this number, the fused-duty risk is completely unmeasured going into Friday.

Your audit result must include the same structure: a count, a threshold, and an owner.

---

## Verification checklist

| Check | Pass criteria |
|-------|---------------|
| Ablation surfaced | Tool asks whether the split logic has been tested in isolation against the failure mode |
| Numeric measurement required | Tool demands a pass/fail count (not just yes/no) |
| Threshold stated | Result includes a number that means trouble (e.g., "must be 3/3") |
| Owner named | Result assigns a person to watch the metric |

All four must pass for the audit tool to be verified.
