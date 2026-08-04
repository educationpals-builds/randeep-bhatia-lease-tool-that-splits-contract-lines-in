# Audit Charter: Lease tool that splits contract lines into separate duties

## Specimen Under Review

**Tool:** Lease tool that splits contract lines into separate duties

**Problem:** On lines with "provided that", it still merges two duties so the wrong party looks responsible.

**Stakes:** A partner signs a summary that puts repair duty on the wrong side

---

## Standard for Success

Each duty lands on its own line with the right party named

---

## Real Inputs Tested

**Source:** Harbor Lease sample contracts

**Input reality:** Old scanned leases with nested "provided that" lines

### Sample Sentences

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

---

## Five-Check Findings

| Check | Rating | Notes |
|-------|--------|-------|
| Room | 0 | No significant concern |
| Copies | 0 | No significant concern |
| Unowned | 0 | No significant concern |
| Stitch | 1 | Minor concern — downstream integration may mask issues |
| Ablation | 2 | **Top crack** — the duty-splitting component has never been tested in isolation |

**Deciding check:** Ablation

---

## Severity Story

Nobody has run the duty-splitting component alone against just the three Harbor Lease sample sentences to confirm it separates Tenant from Landlord correctly before trusting the full tool's merged output. Without that isolated test, a bug in splitting could be masked or amplified by whatever happens downstream — and the first real signal is a partner signing a summary Friday

---

## Ship Call

**Verdict: Hold**

Hold. Shipping without ever isolating the split logic against the exact failure mode (nested "provided that") means the team can't say with confidence what will happen Friday. Priya owns running the three Harbor samples through the split step alone before any ship decision.

---

## Tripwire

Watch: pass/fail count on the isolated three-sample split test. Threshold: must be 3/3 before ship. Priya owns running it — without this number, the fused-duty risk is completely unmeasured going into Friday.

| Metric | Threshold | Owner |
|--------|-----------|-------|
| Pass/fail count on isolated three-sample split test | 3/3 before ship | Priya |

---

## Summary

This audit found that the lease duty-splitting tool cannot ship until the ablation gap is closed. The split logic must be run in isolation against the three Harbor Lease sample sentences — confirming that "Tenant" and "Landlord" land on separate lines with correct party attribution — before any release decision. Without that 3/3 pass count, the team has no evidence the "provided that" merge bug is fixed, and Friday's partner signing carries unmeasured risk.
