# Tribal knowledge

Hardware facts that are true on the counter but are not written in any catalog,
spec sheet or price book — recorded here as they come up, so nobody has to
remember them twice and nobody has to ask Steve the same question again.

**Where these come from.** Each entry names its source. Most are Steve's own
knowledge, given in answer to a research lookup that came back empty. That is a
real source and worth trusting; it is just a different kind of source from a
supplier document, so the file says which is which.

**This file is yours.** Correct any line, or delete it. If something here turns
out to be wrong, fix it — a wrong entry is worse than a missing one, because
the next lookup will trust it.

**How the `/research` skill uses it.** It reads this file *before* asking you
anything, and only asks about what is genuinely missing. When you answer, it
appends the fact here with the date.

---

## Cylinders

### Aftermarket key-in-knob / key-in-lever cylinders — which one retrofits what

*Steve, 2026-08-25. Asked because the catalog carries the items but records
nothing about what the base part numbers are for; `GMSK001SX4OB` and
`GMSK003SX26DOB` are indistinguishable in the catalog data.*

- **GMSK001** — retrofits Allegion and most aftermarket locksets. This is the
  broad family: 40+ catalog items across Schlage C123/G23, ASSA V10, Russwin
  and Yale keyways, 5- and 6-pin, several finishes.
- **GMSK003** — retrofits Sargent locksets. Only one item is catalogued,
  `GMSK003SX26DOB`.
- **ILCO key-in-knob** — retrofits most commercial locksets.

**GMSK002 appears to not exist.** Zero catalog items by prefix or exact
supplier id, and Steve did not name it when giving the other three. Treat it as
not a stocked number unless he says otherwise.

---

## Keyways

### "Marks C" is Schlage C

*Steve, 2026-08-26. Asked because the catalog record for hot# 113055
(`MAR195S/10B`) says "Marks C Keyway" in both its title and its description,
while the training card calls the same lock Schlage "C".*

They are the same keyway. Marks avoids printing the word *Schlage* in their own
literature for marketing reasons, so their material says "Marks C" for what the
rest of the trade calls Schlage C.

**So the catalog is not wrong here, and neither is the card** — do not "correct"
one to match the other. Expect the same pattern anywhere Marks names a keyway,
and read a Marks keyway letter as the industry-standard keyway of that letter
unless something says otherwise.

### KSP keyed alike SFIC cores — each part number is its own group

*From Steve, 2026-08-29.*

We stock the Killeen keyed alike SFIC cores as **KSP206A** (6-pin) and
**KSP207A** (7-pin), and **every keyed alike KSP core we stock is an "A"
keyway**.

**Each stocked core is its own keyed alike group** — two different pin
combinations in 6-pin, two more in 7-pin. So two customers who each order "a
KSP206A" do not necessarily get cores that share a key. A customer adding to
cores they already bought needs the same combination, not just the same part
number. **IML orders the same four sets every time**, so these are stable enough to
name on a card:

| Part | Pins | KA number |
|---|---|---|
| KSP206A26D-KAIM1 | 6-pin | KA #476583 |
| KSP206A26D-KAIM2 | 6-pin | KA #476529 |
| KSP207A26D-KAIM3 | 7-pin | KA #6387594 |
| KSP207A26D-KAIM4 | 7-pin | KA #6387530 |

The KA number lives in each item's description in the catalog; nothing in the
item titles says so.

**One control key covers both combinations of its pin count** — the control
key retracts the control lug regardless of which combination the core is.
**KSPCONTROL6** for the 6-pin cores, **KSPCONTROL7** for the 7-pin. Because the
cores arrive already combinated from KSP, the control key is a separate line
and should be sold with them.

### Kwikset keyway — Ilco writes it KS, GMS writes it KW

*Steve, 2026-08-31. Confirmed while writing the KIL quiz question that asks for
an Arrow lever in a Kwikset keyway.*

The two aftermarket cylinder makers code the same keyway differently:

- **Ilco** — **KS**, as in `ILC15996-KS-26D`
- **GMS** — **KW**, as in `GMSK001-KW-26D`

So a part list that mixes `KS` and `KW` is not a typo — it is two suppliers
naming one keyway their own way. Read the code against the maker, never on its
own.

---

## Locksets

*(nothing recorded yet)*

---

## Exit devices

*(nothing recorded yet)*

## "Conventional cylinder" is a class, not a format (2026-09-02)

**Source: Steve.** Conventional cylinder means any cylinder that is **not** an
interchangeable core and not an IC housing. It is the category, so Key-in-Lever
(KIL/KIK), mortise and rim cylinders are all conventional cylinders.

It is therefore **not** a synonym for KIL, and no single format should be titled
"Conventional Cylinder" — that claims the whole class for one member of it. Both
the app's entry titles and one of its fact tiles had made exactly that mistake.

Why it matters: it is the distinction the whole Cylinders section is organised
around — conventional cylinders in one group, interchangeable cores and their
housings in the other. Get the word wrong and the grouping stops making sense.
