# Transfers between own accounts: categorize ONE side as a transfer — matching handles the mirror

**Since goal 009 (2026-07-10), the app handles this properly.** Categorize the transfer on either account's statement by picking the other cash account under the dropdown's "Transfer to / from" group. The app posts one balanced entry and automatically matches the mirror row on the other statement (exact opposite amount, within 3 days, closest date wins) — whether the mirror is already imported or arrives later. Matched rows sit in "Matched transfers" on the review screen; undoing the transfer releases them.

**The trap this solves** (found in goal 001's adversarial review): categorizing *both* statement rows of one transfer posts the movement twice — both bank balances drift from their statements while the balance-sheet check still shows ✓, because each entry is internally balanced. Balanced ≠ correct.

**Still true:** never categorize the mirror row manually to the other bank account. If a mirror didn't auto-match (amount differs by a fee, >3-day gap), exclude it and post the difference as a manual journal entry — or undo and redo the transfer side once both statements are in.
