---
status: Draft
owner: "Oleksii Smoliankin"
updated_at: "2026-10-31"
depth: "medium"
---

# Idea brief — personal-finance-tracker

## 1. Raw idea

> I want to build personal finance tracker

## 2. Problem

- **Underlying problem: not yet established.** The current way of tracking money and what's painful about it hasn't been stated (unknown).
- **Owner-proposed solution (owner-reported, 2026-10-31):** "I want to have form to input value of spent money, choose category, input comment and button for submit" — i.e. manual expense entry: amount, category, comment, submit.
- **Desired outcomes from the entered data (owner-reported, 2026-10-31):**
  1. See a list of my expenses.
  2. See totals by category.
  3. See spending over time (compare periods).
- **Not chosen:** budget limits / alerts (owner did not select it when offered, 2026-10-31).

## 3. Users

- **Single user: the owner themself** (owner-reported, 2026-10-31). No other users, sign-ups, or shared access planned.
- **Usage situation (owner-reported, 2026-10-31):** enters expenses on a computer, catching up in batches later — not on a phone at the moment of paying. One machine is enough; multi-device access is not needed.

## 4. Why now

No trigger or deadline established. Owner reports no deadline, no course requirement, and no required technology (owner-reported, 2026-10-31).

## 5. Out of scope

- **Excluded from the first version (owner-accepted, 2026-10-31):**
  - Budget limits / alerts (not chosen as a desired outcome).
  - Phone use and syncing between devices (owner enters data on one computer).
  - Other users, sign-up, sharing (single user).
  - Importing transactions from a bank (owner wants manual entry).
  - Income tracking (expenses only).
  - Multiple currencies (one currency).
- **Constraints:** none (owner-reported, 2026-10-31). The AWS Lambda diagram in `mermaid.test` is **not** a requirement.

## 6. Risks

- **Weakest assumption: the underlying problem was never stated.** The owner described a solution (the entry form) and the outcomes they want, but not what is painful about how they track money today. Risk: the tool gets built and not used, e.g. if batch catch-up entry turns out to be too tedious. This is low cost: a personal tool, easy to drop or change.
- **Usage habit:** the value depends on the owner keeping up with manual entry (assumption). The owner chose manual entry and "catch up later" deliberately.
- **Reversibility:** high. Single user, no public contract, no other people's data, no required technology.
- **Critique:** done inline only; no independent devil's-advocate review. It wasn't warranted: no consequential access/data/public-contract change and nothing hard to reverse.

| Claim / question | Class | Source / origin | Finding / limit |
|---|---|---|---|
| Single user, the owner | owner-reported | interview answer, 2026-10-31 | — |
| Wants a form: amount, category, comment, submit | owner-reported | interview answer, 2026-10-31 | a proposed solution, not a problem statement |
| Wants an expense list, totals by category, spending over time | owner-reported | interview answer, 2026-10-31 | budgets/alerts not selected |
| Enters on a computer in batches, one machine | owner-reported | interview answer, 2026-10-31 | — |
| No deadline, course requirement, or required technology | owner-reported | interview answer, 2026-10-31 | — |
| Expenses need a settable date (batch entry later) | assumption → owner-accepted | inferred from batch entry; included in the accepted direction | exact rules belong in specify |
| Repo is effectively empty (README + `mermaid.test`) | source-verified | `git ls-files` + working tree, 2026-10-31, commit 0bd38d9 | greenfield; no architecture yet |

## 7. Recommendation

**Direction (owner-accepted, 2026-10-31):** build a personal expense tracker for one user on one computer. First version:
- manual expense entry: amount, category, comment, date of the expense, submit;
- a list of expenses that can be edited and deleted;
- totals per category;
- spending over time (compare periods).

**Intended result:** the owner can enter their expenses in catch-up batches and see where their money goes by category and over time.

**Main tradeoff:** building something custom vs. using an existing app or a spreadsheet. A spreadsheet could already do this with no build. The owner was offered that alternative and chose to build.

**Outcome: ready-for-roadmap**

**Next action:** the repo has no foundation yet, so run `survey` (greenfield) to pick the stack and structure, then `roadmap` to split the first version into steps.

## 8. Open questions

| Question | Consequence | Blocking? | Verification action | Owner |
|---|---|---|---|---|
| What is painful about tracking money today? | Without it, it's unclear what would make the tool better than a spreadsheet; it's a usage risk, not a build blocker | nonblocking | owner reflects after a few weeks of real use | Oleksii Smoliankin |
| Categories: a fixed list or your own, editable ones? | Shapes the entry form and the totals | nonblocking | decide in `specify` | Oleksii Smoliankin |
| How should "spending over time" be grouped (by month, week, or a custom range)? | Shapes the time view | nonblocking | decide in `specify` | Oleksii Smoliankin |
