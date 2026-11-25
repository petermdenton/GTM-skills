---
name: video-ad-pipeline-setup
description: >-
  Use when setting up or rerunning the B2B short video ad pipeline (customer
  data via MCP, Claude Opus scripts, Wideframe on a Mac). Wideframe is the
  only video maker. Pictory and Fable are legacy.
---

# Video ad pipeline setup

Machine setup for the canonical B2B short video pipeline.

- Roles, steps, and approval gates: [B2B video ad production team](../b2b-video-ad-production-team/SKILL.md)
- Copy rules and the writer/critic loop: [B2B video ad copy loop](../b2b-video-ad-copy-loop/SKILL.md)

Current path: customer data (marketing MCP), then a script drafted by Claude Opus and checked by a separate Opus critic, then licensed stock and a transparent ProRes 4444 type overlay, then Wideframe assembly (`caltools sequence-render-final`) and frame QA. Wideframe is the only video maker. Pictory, Fable, and the Astra review pass are legacy. They are kept at the end of this skill for an existing project, and they are not the path for a new ad.

## 1. Claude Code (Opus writes and critiques copy)

1. Install Claude Code and make sure `claude` is on PATH (symlink to `/usr/local/bin` if needed).
2. Sign in, and make sure the Anthropic account has credits.
3. Draft with: `claude -p "<brief>" --model opus --output-format json > draft.json`. Check `modelUsage` to confirm which model ran. The brief includes the copy loop rules.
4. Run the critic as a second `claude -p` call with a fresh context and `--model opus`. Do not ask the writer call to grade its own draft.

## 2. Codex (customer data via MCP)

1. If the npm package has no platform binary, install Codex from the GitHub release tarball, including `codex-code-mode-host` next to the `codex` binary. Without it, MCP calls fail.
2. Sign in with `codex login --device-auth` using the user's ChatGPT account.
3. Run non-interactively: `codex exec --skip-git-repo-check "<task>"`.
4. In `~/.codex/config.toml`, back up the config first (`config.toml.bak`). Add the marketing MCP server (for example from the user's install script) with `bearer_token_env_var` pointing at its token variable. That server is how the brief gets customer data. Do not add a video-render server here.

## 3. Wideframe

1. Install Wideframe on a Mac with Apple Silicon (M1 or later). Confirm the bundled `caltools` CLI runs in the shell that will do the work.
2. Wideframe needs the Mac online. The app analyzes footage in the cloud and renders on that Mac. Before assembly or `sequence-render-final`, confirm the Mac is on, awake, and online. If it is not, stop and say so.
3. Assembly layout, matching the production team skill: graded footage clips on V1, the transparent ProRes 4444 typography overlay on V2. Render with `caltools sequence-render-final`.
4. The preview render spends no credits. Do not buy a paid asset, and do not start a render that spends credits, until the user has heard the cost and said yes. A paid final render waits for Gate 2 in the production team skill.

## 4. Running an ad

Follow the production team skill end to end. In short:

1. Write a brief from the customer data: audience, required points, banned words, CTA, length, and format. Default to 16:9. Use 1:1 when the LinkedIn placement calls for it.
2. Opus drafts 2-3 options. A separate Opus call critiques them against the copy loop. Show only options that pass, recommended first.
3. After the copy pick, the orchestrator grades licensed stock (Pexels is the usual library), records credits, blurs third-party labels and identifiable faces, and builds the type overlay. State the price and wait for a yes before any paid stock, voice, or music.
4. Wideframe assembles V1 and V2 and renders a preview that spends no credits. If the preview render would spend credits, stop and get a yes first. QA the frames before sending.
5. Send the preview and the cost of the paid render (including a zero cost). Wait for a yes before that render, then deliver the final file.
6. When the user corrects the work, add the underlying lesson as the next numbered rule in the copy loop skill, or in the production team skill for a picture or process issue.

## Rules

- Never render a paid file, buy paid stock, or spend credits without the user's explicit yes. State the cost first, including a zero cost.
- Wideframe needs the Mac online.
- Wideframe is the only video maker. Do not start a new ad in Pictory or Fable.
- Default to 16:9 unless the brief asks for 1:1 or another placement.
- Keep messages short, with numbered multiple-choice questions, recommended option first.

## Legacy: Pictory, Fable, and Astra

Do not use this section for a new ad. It remains so an existing Pictory project can still be rerun, and so the old path is not mistaken for the current one.

Fable is dropped. It was a previous video maker that built the ad as code (HTML or Remotion) and rendered it locally to MP4 with headless Chrome and ffmpeg, with no watermark and no render credits. The chief of staff and Fable used to review each render together. Frame QA now belongs to the orchestrator, and assembly belongs to Wideframe.

Astra was the previous joint reviewer. To rerun that pass on an old project: save the OpenAI key as a secret named `OPENAI_API_KEY`, send the script, scene specs, timings, and frame images to the Astra model (for example `gpt-6.2-astra`), and ask for a PASS/FAIL verdict and concrete fixes. New ads use the Opus critic for copy and the orchestrator's frame QA for the picture.

### Pictory MCP (legacy)

1. Add `https://mcp.pictory.ai/mcp` in `~/.codex/config.toml`. The server uses OAuth 2.0 (authorization code with PKCE) and supports dynamic client registration, so the URL is enough. Do not put an API key header on this server. Run `codex mcp login pictory` and have the user finish sign-in on the computer, starting from Codex so the callback Codex registers is the one Pictory sees. Pictory accepts registered clients and checks the return address: if the login page errors instead of showing the form, that callback is not recognized. Do not open the MCP URL directly in a browser.
2. Guardrails: auto-approve the safe Pictory edit tools, and disable the render, AI-media, voice-change and video-type tools so nothing spends credits without approval.

### Pictory API key (legacy)

1. Save the key as a secret named `PICTORY_API_KEY`. Pictory keys start with `pictai_` and are separate from the MCP account sign-in.
2. Call the REST API at `https://api.pictory.ai/pictoryapis/` with header `Authorization: $PICTORY_API_KEY` and no `Bearer` prefix (for example `v2/projects`, `v1/voiceovers/tracks`). The MCP server does not accept this key. It uses the Pictory account OAuth sign-in above.

### Old Pictory render cost (legacy)

Build a Pictory project as a preview only. A voiceover of about 2.3 words per second fits, and a silent typographic cut is the easiest way to hit an exact length. Those two timing notes still apply to the current pipeline. They are repeated in the production team skill.

Before any Pictory render, read the cost from the connected account (including a zero cost) and wait for the user's yes. On plans that charge render credits, a Pictory 3 or motion-graphics video made through MCP costs 200 AI Credits per video minute for that project's first successful render, with minutes rounded to two decimal places. Later renders of the same project add no Pictory 3 render credits. Eligible Enterprise and API Self-Service plans are not charged AI Credits for that render. Voice-over and AI media are billed separately, so do not treat 200 per minute as the whole cost.
