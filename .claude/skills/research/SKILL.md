---
name: research
description: Look up a hardware item in the IML Item Manager for a training card — photos, hot number, brand, attributes, and what the supplier's own documents say. Reports "not found" rather than filling gaps from general knowledge, and asks Steve when a fact is tribal rather than documented. Use when building or checking a flashcard and you need facts you can point at a source for.
---

# Research an item for a training card

Find what the sources actually say about a hardware item, so a card can be
built on facts somebody can point at rather than on recollection.

**The whole value of this skill is that it does not guess.** A confident wrong
answer about a chamber number or a keyway is worse than no answer, because it
reaches trainees and they repeat it to customers. Everything below serves that.

## The three outcomes

Every fact you report lands in exactly one of these. Say which.

1. **Found in a source** — quote it and name where it came from: the catalog
   field, or the document and page. Prefer the supplier's own words to your
   summary of them.
2. **Not in the sources, but Steve may know** — say the sources are silent,
   then ask him. This is tribal knowledge: things true on the counter that no
   catalog records. Write his answer down (see below).
3. **Neither** — say so plainly and leave it out of the card. Do not soften
   this into a guess. "The sources here don't say, and you weren't sure" is a
   real, useful answer.

**Never fill a gap from general knowledge about locks.** Not even when you are
fairly confident. If it did not come from a source or from Steve, it does not
go on a card.

## Before you ask Steve anything

Read `TRIBAL-KNOWLEDGE.md` at the project root first. If the answer is already
there, use it and cite it as his — do not ask again. Asking twice is how this
becomes tiresome and gets waved through.

**Ask only about facts the card actually needs.** An attribute that is blank in
the catalog but irrelevant to the card is not worth his attention. One or two
real questions per lookup; not an audit of every empty field.

When he answers, append it to `TRIBAL-KNOWLEDGE.md` under the item or topic,
with the date and a note that it came from him. Over time that file becomes
the reference for everything the catalog does not hold.

## The token

Read it from `.agent/itemmanager-token` (one line, no quotes). It is gitignored
because this repo is public — **never** write it into a file that gets
committed, and never echo it in full.

```bash
T=$(cat .agent/itemmanager-token)
B="https://deva-itemmanager.imlss.com"
```

Tokens last about 12 hours. On `401 AUTH_TOKEN_EXPIRED`, stop and tell Steve
plainly that the token has expired and you need a new one pasted into that
file. There is no self-service renewal. Do not retry.

## Calls that work

Verified against a `read_only` token. It cannot change anything, which is the
correct scope for research.

**Find by hot number** — the number Steve usually has. Use an exact phrase so
it does not relax into a fuzzy match:

```bash
curl -s -X POST -H "Authorization: Bearer $T" -H "Content-Type: application/json" \
  -d '{"q":"\"206760\"","size":3}' "$B/search/v1/items"
```

**Find by description** — add the image filter when the card needs a photo:

```bash
curl -s -X POST -H "Authorization: Bearer $T" -H "Content-Type: application/json" \
  -d '{"q":"Sargent 6300 LFIC core","size":10,"include":{"has_primary_image":["true"]}}' \
  "$B/search/v1/items"
```

**Which count to believe, because they differ by query shape:**

- **Plain text** (`Sargent 6300 LFIC core`) runs a strict pass, then relaxes if
  strict found nothing — and the relaxed pass drops your filters. So read
  `strict_total`. A `strict_total` of 0 with a large `total` means nothing
  really matched and the results are noise.
- **A quoted phrase** (`"206760"`) runs one honest pass with no relaxation, so
  it omits `strict_total` entirely. There, `total` is the real count. Same for
  the other operators: `a|b`, `-term`, `+term`, `term*`.

**Item detail** — attributes, identifiers, brand, media, literature:

```bash
curl -s -H "Authorization: Bearer $T" "$B/catalog/v1/items/<item_id>/detail"
```

**Photo or document bytes** — sign the artifact, then fetch it. Signed URLs
expire in minutes, so never paste one into a card; download and embed instead:

```bash
curl -s -H "Authorization: Bearer $T" "$B/artifacts/v1/artifacts/<artifact_id>/url?ttl=300&prefer=webp"
```

Always check the downloaded bytes against the `content_hash` the response
carries before using them. A mismatch means do not use it.

## Depth

**Catalog first.** Attributes, identifiers, brand and photos answer most
questions and cost one or two calls.

**Open the documents when the catalog is silent, or when Steve asks.** An
item's `literature` array carries spec sheets, price books and product
catalogs — often eight or more. These hold the real answers about housings,
functions and compatibility. They are also slow and large, so do not open them
by reflex. When you do, cite the document and the page.

## What to report back

Lead with the answer, then the support. For a card lookup, usually:

- the item's title, brand, and hot number
- the attributes that matter for the card, each marked found or absent
- whether a usable photo exists, and its dimensions
- what the documents add, if you opened them
- **the gaps** — clearly separated, with your question for Steve

Keep it short enough to read. If a fact is missing, that absence is part of the
answer, not a failure to be papered over.

## What this skill does not do

- It does not write cards. It reports; Steve decides what goes on a card.
- It does not browse the open web. Supplier sites and the `imlss.com` family
  are allowed by `AGENTS.md`; competitors and general browsing are not.
- It does not change catalog data. The token is read-only by design.
