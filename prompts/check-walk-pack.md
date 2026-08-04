# Check Walk Prompts: Lease tool that splits contract lines into separate duties

Five standalone prompts for auditing a duty-splitting setup. Each prompt walks one check and ends with the measurement it demands. Use any chat model.

---

## Prompt 1: Room Check

You are auditing a lease tool that splits contract lines into separate duties.

**The problem:** On lines with "provided that", the tool still merges two duties so the wrong party looks responsible.

**What goes wrong if unfixed:** A partner signs a summary that puts repair duty on the wrong side.

**Standard for success:** Each duty lands on its own line with the right party named.

**Real inputs the tool sees:** Old scanned leases with nested "provided that" lines.

Here are three real failing inputs from Harbor Lease sample contracts:

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Your task:** Assess whether there is room for this failure to occur in the current setup. Could the splitting logic encounter these nested conditional clauses and produce merged duties?

**End with this measurement:** State the number of input patterns in the real corpus where nested conditionals could trigger merged-duty output. Report as: "Room score: X patterns identified where failure is possible."

---

## Prompt 2: Copies Check

You are auditing a lease tool that splits contract lines into separate duties.

**The problem:** On lines with "provided that", the tool still merges two duties so the wrong party looks responsible.

**What goes wrong if unfixed:** A partner signs a summary that puts repair duty on the wrong side.

**Standard for success:** Each duty lands on its own line with the right party named.

**Real inputs the tool sees:** Old scanned leases with nested "provided that" lines.

Here are three real failing inputs from Harbor Lease sample contracts:

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Your task:** Check whether this failure has been seen before. Are there logged instances, bug reports, or prior test runs showing the duty-splitting tool merging parties incorrectly on conditional clauses?

**End with this measurement:** State the number of documented prior occurrences of this exact failure mode. Report as: "Copies score: X prior instances of merged-duty output on conditional clauses found in logs/reports."

---

## Prompt 3: Unowned Check

You are auditing a lease tool that splits contract lines into separate duties.

**The problem:** On lines with "provided that", the tool still merges two duties so the wrong party looks responsible.

**What goes wrong if unfixed:** A partner signs a summary that puts repair duty on the wrong side.

**Standard for success:** Each duty lands on its own line with the right party named.

**Real inputs the tool sees:** Old scanned leases with nested "provided that" lines.

Here are three real failing inputs from Harbor Lease sample contracts:

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Your task:** Determine whether anyone owns fixing this failure. Is there a named person responsible for the duty-splitting logic, or does this component sit between teams with no clear owner?

**End with this measurement:** State whether an owner exists and name them, or confirm the gap. Report as: "Unowned score: [Named owner] is responsible for the split logic / No owner assigned — component sits unowned between [X] and [Y]."

---

## Prompt 4: Stitch Check

You are auditing a lease tool that splits contract lines into separate duties.

**The problem:** On lines with "provided that", the tool still merges two duties so the wrong party looks responsible.

**What goes wrong if unfixed:** A partner signs a summary that puts repair duty on the wrong side.

**Standard for success:** Each duty lands on its own line with the right party named.

**Real inputs the tool sees:** Old scanned leases with nested "provided that" lines.

Here are three real failing inputs from Harbor Lease sample contracts:

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Your task:** Examine how the duty-splitting component connects to upstream and downstream steps. Does the split output get validated before it flows into the summary? Could a bug in splitting be masked or amplified by whatever happens downstream?

**End with this measurement:** State the number of handoff points where split output passes without validation. Report as: "Stitch score: X unvalidated handoffs between split logic and final summary output."

---

## Prompt 5: Ablation Check ⚠️ TOP CRACK

You are auditing a lease tool that splits contract lines into separate duties.

**The problem:** On lines with "provided that", the tool still merges two duties so the wrong party looks responsible.

**What goes wrong if unfixed:** A partner signs a summary that puts repair duty on the wrong side.

**Standard for success:** Each duty lands on its own line with the right party named.

**Real inputs the tool sees:** Old scanned leases with nested "provided that" lines.

Here are three real failing inputs from Harbor Lease sample contracts:

1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

**This is the top crack identified in the audit.**

**Severity story:** Nobody has run the duty-splitting component alone against just the three Harbor Lease sample sentences to confirm it separates Tenant from Landlord correctly before trusting the full tool's merged output. Without that isolated test, a bug in splitting could be masked or amplified by whatever happens downstream — and the first real signal is a partner signing a summary Friday

**Your task:** Determine whether the duty-splitting component has ever been tested in isolation against the exact failure mode (nested "provided that" clauses). Has anyone run just the split step on these three Harbor Lease samples to confirm Tenant and Landlord land on separate lines with correct party attribution?

**End with this measurement:** State the pass/fail count on an isolated test of the three Harbor Lease samples through the split step alone. Report as: "Ablation score: X/3 samples correctly split in isolated test." If no isolated test has been run, report: "Ablation score: 0/3 — no isolated test performed."

---

## Using These Prompts

Run each prompt independently against your duty-splitting setup. Collect the five measurements:

| Check | Measurement |
|-------|-------------|
| Room | Number of patterns where failure is possible |
| Copies | Number of prior documented occurrences |
| Unowned | Named owner or ownership gap |
| Stitch | Number of unvalidated handoffs |
| Ablation ⚠️ | Pass count on isolated three-sample test |

**Ship call from this audit:** Hold. Shipping without ever isolating the split logic against the exact failure mode (nested "provided that") means the team can't say with confidence what will happen Friday. Priya owns running the three Harbor samples through the split step alone before any ship decision.

**Tripwire:** Watch: pass/fail count on the isolated three-sample split test. Threshold: must be 3/3 before ship. Priya owns running it — without this number, the fused-duty risk is completely unmeasured going into Friday.
