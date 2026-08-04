# Lease tool that splits contract lines into separate duties

## One-paste spec for auditing duty-splitting setups

Use this blueprint to audit any tool that splits contract lines into separate duties. Paste the entire spec into a chat model to run a five-check audit on your own failing setup.

---

## What this auditor does

You describe a duty-splitting tool that's failing. The auditor walks five checks, proposes findings with the measurement that would confirm each, and returns:

1. A scored audit across all five checks
2. A severity story on one of your pasted inputs
3. A ship / ship-with-conditions / hold call
4. A tripwire with a threshold and an owner

---

## Worked example: Harbor Lease duty-splitter

**Specimen:** Lease tool that splits contract lines into separate duties

**What goes wrong if this never gets fixed:** A partner signs a summary that puts repair duty on the wrong side

**How you know it's fixed:** Each duty lands on its own line with the right party named

**Real inputs (old scanned leases with nested "provided that" lines):**

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

**Source:** Harbor Lease sample contracts

**Check ratings:**
| Check | Rating |
|-------|--------|
| Room | 0 |
| Copies | 0 |
| Unowned | 0 |
| Stitch | 1 |
| Ablation | 2 |

**Top crack:** Ablation

**Severity story:** Nobody has run the duty-splitting component alone against just the three Harbor Lease sample sentences to confirm it separates Tenant from Landlord correctly before trusting the full tool's merged output. Without that isolated test, a bug in splitting could be masked or amplified by whatever happens downstream — and the first real signal is a partner signing a summary Friday

**Ship call:** Hold. Shipping without ever isolating the split logic against the exact failure mode (nested "provided that") means the team can't say with confidence what will happen Friday. Priya owns running the three Harbor samples through the split step alone before any ship decision.

**Tripwire:** Watch: pass/fail count on the isolated three-sample split test. Threshold: must be 3/3 before ship. Priya owns running it — without this number, the fused-duty risk is completely unmeasured going into Friday.

---

## One-paste auditor prompt

Copy everything below this line and paste into any chat model:

---

You are an auditor for duty-splitting tools — systems that take contract lines and separate them into individual duties with the correct party assigned.

I will describe a failing duty-splitting setup. Walk me through five checks, one at a time. For each check, propose a finding and name the specific measurement that would confirm it.

After all five checks, give me:
1. A severity story: walk one of my pasted inputs through the failure, showing who acts on the wrong output
2. A ship call: ship / ship-with-conditions / hold — with reasons and owners for any conditions
3. A tripwire: what metric to watch after release, the threshold that means trouble, and who owns watching it

**The five checks:**

1. **Room** — Is there space in the workflow for this tool to fail silently? What downstream step would catch a bad split before it reaches a human decision?

2. **Copies** — Are there redundant checks that would surface the same failure? Or does everything depend on this one splitting step?

3. **Unowned** — Is anyone specifically responsible for verifying split quality? Or does the output flow to the next step with no one accountable for checking it?

4. **Stitch** — How does this splitting step connect to what comes before and after? Could errors upstream (OCR, formatting) or downstream (summarization, routing) mask or amplify a splitting bug?

5. **Ablation** — Has anyone run the splitting component alone, isolated from the rest of the pipeline, against known failure cases? Without that test, how would you know the splitter itself is the problem?

**Here is my failing setup:**

[Paste your specimen, stakes, standard, real failing inputs, and source here]

---

## Acceptance criteria

- Auditor walks all five checks for a stranger's duty-splitting specimen
- Every finding names the measurement that would confirm it
- Result includes a severity story on a pasted contract line, a call, and a tripwire with a threshold
- The Harbor Lease audit above is visible as the worked example
