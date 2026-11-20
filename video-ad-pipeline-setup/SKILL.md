---
name: video-ad-pipeline-setup
description: Use when setting up or rerunning a multi-agent LinkedIn video ad pipeline (customer data via MCP, Claude Opus scripts, Pictory video, OpenAI Astra review) on the bot's computer.
---
# Video ad pipeline setup

Pipeline: customer data (marketing MCP), then a script drafted by Claude Opus, then a bot review, then the video built in Pictory, then a joint review by the bot and Astra (OpenAI), with the bot running the whole thing.

## 1. Claude Code (Opus drafts scripts)
1. Install Claude Code and make sure `claude` is on PATH (symlink to `/usr/local/bin` if needed).
2. Sign in, and make sure the Anthropic account has credits.
3. Draft with: `claude -p "<brief>" --model opus --output-format json > draft.json`. Check `modelUsage` to confirm which model ran.

## 2. Codex (ChatGPT account and MCP host)
1. If the npm package has no platform binary, install Codex from the GitHub release tarball, including `codex-code-mode-host` next to the `codex` binary. Without it, MCP calls fail.
2. Sign in with `codex login --device-auth` using the user's ChatGPT account.
3. Run non-interactively: `codex exec --skip-git-repo-check "<task>"`.

## 3. MCP servers in `~/.codex/config.toml`
1. Back up the config first (`config.toml.bak`).
2. Customer data: add the marketing MCP server (for example from the user's install script) with `bearer_token_env_var` pointing at its token variable.
3. Pictory: add `https://mcp.pictory.ai/mcp`, then run `codex mcp login pictory` and have the user complete the sign-in on the computer. Pictory rejects unapproved OAuth clients, so sign in through Codex, not a direct connector.
4. Guardrails: auto-approve the safe Pictory edit tools, and disable the render, AI-media, voice-change and video-type tools so nothing spends credits without approval.

## 4. Pictory API key (faster, direct)
1. Save the key as a secret named `PICTORY_API_KEY`.
2. Call the REST API at `https://api.pictory.ai/pictoryapis/` with header `Authorization: $PICTORY_API_KEY` (for example `v2/projects`, `v1/voiceovers/tracks`). The MCP server does not accept this key; it needs its own sign-in token.

## 5. Astra review (OpenAI)
1. Save the OpenAI key as a secret named `OPENAI_API_KEY`.
2. Send the script, scene specs, timings and frame images to the Astra model (for example `gpt-6.2-astra`) and ask for a PASS/FAIL verdict and concrete fixes.

## 6. Running an ad
1. Write a brief from the customer data: audience, four key points, CTA, length, format.
2. Opus drafts the script; the bot reviews it against the brief and the user's edits.
3. Build a brand guide from the customer's site: colors, font, logos.
4. Build the Pictory project as a preview only. Check the runtime against the target: a voiceover of about 2.3 words per second fits, and a silent typographic cut is the easiest way to hit an exact length.
5. Review with Astra, fix, and repeat up to two rounds.
6. Send the preview link. Before any render, show the credit cost (about 200 credits per minute on the first render; later re-renders of the same project are free) and wait for the user's yes. Then send the final link.

## Rules
- Never render, buy AI media, or change voices without the user's explicit yes.
- Default to 16:9 unless the reference style says otherwise.
- Keep messages short, with numbered multiple-choice questions, recommended option first.
