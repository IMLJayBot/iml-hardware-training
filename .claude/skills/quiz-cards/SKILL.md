---
name: quiz-cards
description: Write Knowledge Check questions for a deck in the IML hardware training app — the house style, the field shape, the photo rules, and the approval loop. Drafts questions for Steve to review before anything is written, and never embeds a photo he has not approved. Use when adding, rewriting, or reviewing quiz questions in index.html.
---

# Writing quiz questions for a deck

The questions are the part of this app a trainee actually gets tested on, so
they are the part most worth getting right. A card that teaches a wrong part
number reaches a new hire, who repeats it to a customer.

## The loop, and it does not change

1. **Draft the questions in chat.** Question, the four choices with the answer
   marked, the caption, the hint. No file edits yet.
2. **Steve reviews.** He edits wording heavily — expect it, and expect the
   final phrasing to be his rather than yours.
3. **Show him the photos and get approval.** Every photo, including ones you
   pulled from the catalog yourself. He approves before anything is embedded.
4. **Build**, then tell him to reload the preview.

Build **one at a time** when he asks for one at a time. He has said so
explicitly, and a batch of eight is harder for him to steer than one.

## House style

Read the questions already in `index.html` before writing new ones — the KIL
deck especially. They are the reference, not this file.

**An answer is either a real part number or a real description — never an
invented one.** `Schlage 23-030` and `ILC15996` are answers; so are
`FSIC Core`, `Conventional Cylinder` and `Passage`. Both shapes are in use and
both are correct.

Which one to reach for depends on what the question is testing. Asking *what
kind of cylinder goes in here* wants the category — `FSIC Core` — because
telling the formats apart is the skill. Asking *what do I sell this customer*
wants the number, because that is what goes on the order. A question can also
sit between the two, where naming the category is enough to be right and the
number would be over-specific; pick the level the question actually tests.

The rule that never bends: whichever shape you use, it names something real.
No invented part numbers, no made-up categories.

**Every wrong answer is a real thing IML sells, and each is wrong for its own
reason.** Wrong format, wrong brand, right part in the wrong keyway, the part
that goes *into* the thing pictured. Never invent a part number to pad the
choices, and never write a throwaway option nobody would pick.

**Every question gets a hint.** Terse is right: `Sargent`, `KNK (KIK/KIL)`,
`Look at the snowman shape of the lever face`, `Replacement cylinder +
special tailpiece needed`. A hint names what to look at; it does not answer.

**The caption carries the premise.** This is the strongest convention in the
KIL deck and it is easy to miss: *"Arrow levers (conventional cylinder) are
only stocked (Schlage \"C\" Keyway)"* is not a label, it is the fact that
makes the question answerable. Put the stocked keyway, the series, the "less
core" state in the caption.

**Say leverset, not lever or lock**, in customer-facing question text.

**Ask what the deck should cover before you write it.** Identification from a
photo, customer-need scenarios, or both — that is Steve's call per deck, not a
default. Lock Functions runs both passes over the same eight functions;
KIL is mostly "what fits this?" and "what do I sell instead?".

## The field shape

The authoritative field guide is the comment above `buildAuthoredQuiz()` in
`index.html`. Read it. In short:

    {
      photo:    "<card id>",      // borrow a card's photos — BOTH front and
                                  // back come across, so a card shot outside
                                  // and inside stays a two-photo question
      photoSrc: "data:image/...", // OR embed one, for an item with no card
      question: "...",
      choices:  ["...", "...", "...", "..."],
      answer:   "...",            // must match one of `choices`
      answers:  ["...", "..."],   // instead of `answer`, for multi-answer
      caption:  "line under the photo",
      hint:     "nudge above the question",
    }

`quizQuestions` on a subcategory replaces the generated quiz entirely. A deck
that currently has no written questions is being quizzed automatically from
its cards — **adding one written question silently drops the other eight**, so
write them all out, matching what the generated ones did.

A quiz draws `QUIZ_QUESTION_COUNT` (12) at random from whatever is written, so
a deck of sixteen gives a different twelve each attempt.

## Photos

**Hardware comes from the Item Manager.** Use the `research` skill. Sign the
artifact, download, and check the bytes against `content_hash` before using
them. Signed URLs expire in minutes — embed the bytes, never the link.

**Rooms and scenes come from Steve.** The catalog has hardware, not
breakrooms. Ask him; he keeps them in `iml.jpg/Screen Snips/` named for the
function. Never take a photo from the open web — `AGENTS.md` forbids it, and a
stock photo carries a watermark and someone else's rights. One already turned
up watermarked and had to be replaced.

**He approves every photo before it goes in.** Including catalog pulls.

**Look at the photo yourself before you write the question about it.** A hint
that says "note the logo on the face" is a guess until you have seen the face.

**Resize before embedding**: 700px max width, JPEG quality 78, via
System.Drawing in PowerShell (there is no Pillow or ImageMagick on this
machine). Eight room photos went from 825KB to 340KB that way. Keep his
originals untouched.

## What not to do

- Do not fill a gap from general lock knowledge. Sources or Steve, or leave it
  out — same rule as the `research` skill.
- Do not write a question whose photo gives the answer away.
- Do not batch when he asked for one at a time.
- Do not embed a photo he has not seen.
