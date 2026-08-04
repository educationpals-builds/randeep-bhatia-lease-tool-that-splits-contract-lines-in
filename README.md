# Lease tool that splits contract lines into separate duties

**Verdict: Hold**

This lease-splitting tool is supposed to separate contract lines into individual duties with the correct party named. On lines containing "provided that," it still merges two duties—so the wrong party looks responsible.

## The problem

A partner signs a summary that puts repair duty on the wrong side.

## The standard

Each duty lands on its own line with the right party named.

## The tripwire

Watch: pass/fail count on the isolated three-sample split test. Threshold: must be 3/3 before ship. Priya owns running it — without this number, the fused-duty risk is completely unmeasured going into Friday.

## The call

Hold. Shipping without ever isolating the split logic against the exact failure mode (nested "provided that") means the team can't say with confidence what will happen Friday. Priya owns running the three Harbor samples through the split step alone before any ship decision.

---

## One-paste rebuild block

Copy this into your audit when you need to re-run the five checks on this specimen:

```
Specimen: Lease tool that splits contract lines into separate duties
Stakes: A partner signs a summary that puts repair duty on the wrong side
Standard: Each duty lands on its own line with the right party named
Source: Harbor Lease sample contracts

Sample sentences:
1. Tenant shall repair the roof provided that Landlord funds materials within 10 days.
2. Fees accrue daily; provided, however, that the cap in §4.2 still applies.
3. Notice is deemed given when posted, unless the parties agree otherwise in writing.

Top crack: ablation
Tripwire: 3/3 pass on isolated split test, Priya owns
```

---

## Full audit

See [charter.md](charter.md) for the complete five-check audit, including check ratings, severity story, and the detailed ship decision.

## Method

See [METHOD.md](METHOD.md) for the five-check framework used in this audit.

## Verification

See [VERIFY.md](VERIFY.md) for instructions on running your own failing lease-splitting setup through the audit.

<!-- educationpals-build-verified -->
