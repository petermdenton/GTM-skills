---
name: b2b-video-ad-copy-loop
description: >-
  Use whenever writing or revising copy for a short B2B video ad (LinkedIn,
  silent or voiced) before showing it to the user. Applies the copy rules,
  runs an Opus writer and a separate Opus critic, and turns user feedback
  into the next numbered rule.
---

# B2B video ad copy loop

The copy standard for the [B2B video ad production team](../b2b-video-ad-production-team/SKILL.md). Copy reaches the user only once it already reads well, and every correction becomes a rule so the user never has to give it twice.

Examples below use placeholder names (Acme, Kit, the city library). Swap in the client's own names. Do not copy a real client's facts into this skill.

## Copy rules (append new ones as the user gives feedback)

1. Write full sentences or bold statements. Do not stack headline fragments, and do not use labels such as "CASE STUDY:".
2. The whole script must make sense read top to bottom in a document, as one coherent thought.
3. Use one protagonist, usually the viewer ("you"). Proof points such as customers or case studies are evidence, not the subject.
4. Tell one arc, not stacked claims: stakes, then proof, then payoff. The last card pays off the first, and nothing new is introduced at the end.
5. Use less text. For a short silent ad, write about 3 big statements of roughly 3-8 words each, in display-size type, plus a small CTA line. Cut supporting detail, including component names, rather than cramming it in.
6. Every statement leads into the next.
7. Use the brief's required ideas (they can be compressed) and avoid its banned words exactly.
8. Speak to the target buyer in that buyer's own terms, not generic AI-buyer language ("unlock", "supercharge", "next-gen").
9. Use the buyer's own vocabulary. When the brief or the buyer already has a word for something, use that word. Do not swap in a near-synonym that sounds smaller or more generic to them. If they say "workspace", write "workspace".
10. Credit proof to the named organization. Name the organization that did the work (the company, the lab, the university), not a weaker-sounding group inside it such as "students" or "interns". Stay accurate by choosing a modest verb. Do not sound careful by shrinking who did the work.
11. Brand the proof. When the proof uses the client's open-source product, name the client as its owner: "{Client}'s open-source {Product}". For example, "Acme's open-source framework Kit". A bare product name leaves the credit with the project, not the client.
12. The payoff card can be a short lead-in plus 3 concrete product benefits as bullets (for example "Acme's platform gives you:" then three items of 2-5 words), sourced from the client's own pages. This is an allowed exception to rule 1.
13. Every proof point needs a "so what". Say why the viewer should care: the result or benefit to them, not only what someone built.
14. Proof sentences use a plain "built AI for [problem] on [product]" shape. For example, "The city library built AI for catalog search on Acme's open-source Kit." Keep the technical mechanism (which model, which method, which stack) out of the proof line, and move it to a short follow-on "so what" line.
15. A follow-on line may be a punchy parallel fragment that continues the previous sentence. For example: "In the tools their team already opens, / On the stack their team already runs."
16. When the user writes a line themselves, use it verbatim. Note critic concerns only once, and do not rewrite their line to satisfy the critic.
17. Give each text card enough reading time. In a silent ad, hold every card for 5-7 seconds. Hold a long proof line (about 15 words or more) for about 7.5 seconds, even if the ad runs past 30 seconds.

## Steps

1. Writer: have Opus (`--model opus`) write 2-3 options against the brief and the rules above. See the production team skill for who runs this call.
2. Critic gate: a separate Opus call acts as a senior B2B copywriter. It does not share the writer's context. It reads each option as a document and aloud, checks it against every rule, says pass or fail with reasons, and rewrites any failures. Repeat up to 2 times. Show only options that pass.
3. Present the options to the user as a numbered pick, with the recommended one first, each statement on its own line.
4. Do not render until the user picks. Picture, frame QA, and delivery belong to the production team skill. Before anything is sent, QA the frames for clipping and for word-for-word copy accuracy.
5. Learn: when the user rejects or corrects copy, find the underlying rule (not only the wording fix) and append it as the next numbered rule in this skill. Keep a log of picks and reasons in the campaign project folder, such as `copy-log.md`. That log stays in the campaign project. It does not go in this repo.
