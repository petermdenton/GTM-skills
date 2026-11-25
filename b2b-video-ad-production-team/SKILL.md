---
name: b2b-video-ad-production-team
description: >-
  Use for any short B2B video ad (LinkedIn or similar) from brief to final
  file. The canonical pipeline: an orchestrator, an Opus copywriter and a
  separate Opus critic, Wideframe assembly, frame QA, and the approval gates.
---

# B2B video ad production team

The canonical pipeline for a short B2B video ad, from brief to final file. Wideframe is the only video maker. Default format is 16:9. 1:1 is a common LinkedIn variant. Copy follows the [B2B video ad copy loop](../b2b-video-ad-copy-loop/SKILL.md). Machine setup is [video ad pipeline setup](../video-ad-pipeline-setup/SKILL.md).

## Roles

1. Chief of staff (the orchestrator agent) owns the brief, the facts, the schedule, and quality. It briefs every other role, checks their work, and is the only one who talks to the user. It never passes on unreviewed work. It sources and grades licensed stock footage (Pexels is the usual library), records the creator and license for every clip that is used, and blurs third-party labels and identifiable faces before a clip is assembled.
2. Opus is the copywriter (`--model opus`). It writes all on-screen copy and any voiceover, using the copy loop rules. A separate Opus call, with its own context, is the copy critic. The writer does not grade its own draft.
3. Wideframe is the video maker. It runs on a Mac and assembles the cut with the `caltools` CLI bundled with the app. Graded footage clips go on V1. Typography goes on V2 as a transparent ProRes 4444 overlay, so the type is not burned into the footage. The sequence is rendered with `caltools sequence-render-final`. Wideframe cuts and composites footage you supply. It does not invent the picture from a prompt.
4. The user approves at the gates below and makes the final decision.

## Steps

1. Brief. The orchestrator gathers the audience, format (16:9 unless the placement needs 1:1 or another shape), length, required points, banned words, CTA, and brand guide. Read the primary sources, write down only verified facts, and flag any claim that is stronger than its source. A voiceover of about 2.3 words per second fits a spoken read. A silent typographic cut is the easiest way to hit an exact length.
2. Copy. Opus writes 2-3 options following the copy loop. The separate Opus critic checks flow (read as a document) and factual accuracy against the brief. Only passing options move on.
3. Gate 1, copy pick. The user picks the copy (a numbered choice, recommended first). Do not build the picture before this pick.
4. Picture. The orchestrator grades licensed stock for fit, records each credit, and blurs readable third-party labels (logos, product names, screens) and identifiable faces. Prefer assets that cost nothing. Pexels is the usual library. Before buying stock, voice, music, or any other paid asset, state the price and wait for a yes. Then build the typography as a transparent ProRes 4444 overlay, timed to the picked copy. Silent cards hold for 5-7 seconds, and a long proof line holds for about 7.5 seconds.
5. Assemble. Confirm the Mac running Wideframe is on and online, then hand it the graded clips and the overlay. Clips land on V1, the overlay on V2. Render the preview with `caltools sequence-render-final` at no added cost. If that render would spend credits, stop and get a yes before running it. Reaching the preview gate must not itself require unapproved spending.
6. Frame QA. The orchestrator checks the frames and the preview for clipping, word-for-word copy, reading time per card, pacing, brand colors and logo, the CTA, blurs that actually cover labels and faces, and a recorded credit for every stock clip. Fix and re-render the zero-cost preview, up to 2 rounds. Do not send a preview that fails this check.
7. Gate 2, preview and cost. Send the preview. With it, state the cost of the paid render and of any asset not already approved, including a zero cost, and wait for a yes. Do not start a paid render before that yes.
8. Gate 3, final delivery. Deliver the final file. Log the user's picks and corrections in the campaign project. Turn each correction into the next numbered rule in the copy loop skill, or in this skill when it is a picture or process issue.

## Rules

1. Never overstate a source. Describe a pilot, a student project, or a test as what it is.
2. Wideframe needs the Mac online. Wideframe is a Mac app: assembly and `sequence-render-final` run on that Mac, and its footage analysis needs the network. If the Mac is off, asleep, or offline, stop and say so. Do not start a render that cannot finish.
3. Keep user messages short, with numbered choices and one question at a time.
4. If the user pushes back twice on the same thing, stop rewriting blindly. Go back to the source material, or ask for their words.
5. Record the creator and license for every stock clip, in the campaign project, even when the license does not require an on-screen credit. Do not ship a frame with a readable third-party label or an identifiable face that was not cleared.
6. Clips on V1, typography on V2. The overlay is a transparent ProRes 4444. Do not bake the type into the footage file.
7. No unapproved spend. Paid stock, voice, music, and any other paid asset need a stated cost and a yes before purchase. The preview render costs nothing. A paid render waits for Gate 2, and the stated cost includes zero.
