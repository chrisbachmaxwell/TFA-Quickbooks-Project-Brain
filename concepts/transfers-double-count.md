# Transfers between own bank accounts double-count if both sides are categorized

**The trap:** a $5,000 transfer from Checking A to Checking B appears on **both** bank statements. Categorize A's row to "B Checking" (correct entry: debit B, credit A) — then, when B's statement is imported, its mirror row is still sitting in Uncategorized. Categorize it to "A Checking" and you post the same movement **again**: both bank ledger balances drift $5,000 from their statements, the P&L is untouched, and the balance-sheet check still shows ✓ because every entry is internally balanced. Balanced ≠ correct.

**Why v0 allows it:** the category dropdown offers every active account except the transaction's own bank account — including other bank accounts. Real transfer matching (pairing the two statement rows into one entry) is roadmap M4.

**The v0 convention (until M4):** categorize only **one** side of a transfer — the row on the *sending* account's statement — to the receiving bank account. When the mirror row shows up on the other statement, it must be left uncategorized (annoying, known cost, tracked in M4). Never categorize both sides.

Found in adversarial review, 2026-07-10 (see log/2026-07-10-ledger-v0-built.md).
