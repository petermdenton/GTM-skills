---
name: cold-email-volume
description: Use when planning or running high-volume B2B cold email and you need inbox math, list capacity, provider splits, copy rules, inbox health, and reply triage.
---

# Cold email volume

A system for sending high daily volume without burning domains or dragging the company's normal email into spam. Every figure below is Will Breton's guidance from the source article. Do not invent numbers you cannot explain. Prompts are written for Claude Code or any Claude chat with the relevant exports attached. Swap the brackets for the user's details.

## When this applies

High volume fits best when all 3 are true:

1. The deal is worth $10k+ a year.
2. The market has 50,000+ contacts.
3. Someone on the team can answer replies within a minute.

If the whole market is around 10,000 companies, skip this playbook. That market needs a slower, targeted approach (emails written around signals, ads, LinkedIn, calls). Volume makes a good offer print and a bad one fail faster. A bad offer can burn an inbox inside a month even when the rest of the setup is right, because negative replies hurt reputation with Google.

## 1. Do the inbox and domain math first

Do this before buying a single domain. The author's sending rules:

1. Google inboxes only. After a year of Microsoft inboxes underperforming, the author stopped splitting volume between them and buys more Google inboxes instead.
2. 2 inboxes per domain.
3. 15 cold emails per inbox a day, 20 at the most. Prefer more inboxes over pushing the ones you have. At 25-30 a day they burn faster, and replacing them costs more than the extra inboxes would have.
4. Keep a reserve. A full 1:1 reserve is ideal. 20% is the minimum. Inboxes burn, and a spare that still needs 25 days of warm-up is a spare you do not have.

Worked example at 4,000 emails a day:

1. Inboxes = 4,000 ÷ 15 = 267
2. Domains = 267 ÷ 2 = 134
3. 20% reserve = 54 more inboxes on 27 more domains
4. Total = 321 inboxes on 161 domains

Author's costs, checked at the time of the article:

1. Inboxes (ScaledMail): $3.50 each, about $1,124/mo for 321
2. Domains (Porkbun): $11.81 each, about $1,900/year for 161
3. Sequencer (EmailBison): about $600/mo. Under 50,000 emails a month, PlusVibe (from $37/mo) can replace it.
4. Verification (MillionVerifier): $89 per 50,000 emails checked

```
I want to send [4,000] cold emails a day from Google inboxes.

Work out what I need, showing every step:
1. Inboxes = daily volume ÷ 15
2. Domains = inboxes ÷ 2
3. Add a 20% reserve, then show the 1:1 version too
4. Monthly cost at $3.50 per inbox, and yearly cost for the domains at
   $11.81 each

Then write me 100 secondary domain names for [mycompany.com].
Rules: they must look like my company (try-, get-, go-, -hq versions),
no hyphens, no numbers, no words like "capital", "finance" or "money".
Under 50,000 emails a month, .com only. Past 200,000 a month, mix in .org,
.co and .co.uk.

List them in one column so I can paste them into a bulk domain search.
Don't buy anything.
```

Run the names through a bulk domain search (the author uses Porkbun, 100 at a time). Then start the clock:

1. Day 1: buy the domains and order the inboxes so warm-up starts the same day. Do this only after the market-sizing check in section 2. If that check says the list cannot feed this volume, lower the daily number and rerun the math before buying anything.
2. Days 1-14: warm-up, starting at 5 a day and adding 1 a day up to 20.
3. Day 15: cold sending starts at 5 per inbox.
4. Day 25: full volume, 15 per inbox.

Domains bought today hit full volume about 25 days later. Warm-up stays on the whole time the inbox is sending.

## 2. Size the market and build a list that can feed the volume

Inboxes set sending capacity. The list sets how long you can keep using it.

The author's sequence is 1 follow-up, 3 days after the first email, and that is the whole sequence. The first email always gets the highest reply rate, so spend the volume on new people instead of a long sequence to the same ones.

List math at 4,000 emails a day and 2 emails per person:

1. 4,000 ÷ 2 = 2,000 new people a day
2. 2,000 × 22 sending days = 44,000 new people a month
3. You need a market of 50,000+ contacts, and you will contact all of it inside about 5 weeks.

Refresh and re-enrich the whole market every 30-60 days. A temporary no from a few months ago can be ready today. An opt-out, or any request for no further contact, is different: keep those people on a do-not-contact list that applies across every sending account and every provider bucket. Apply that list before every import and every send. A refresh must not put them back. The author estimates that 30-50% of the contacts on a 6-month-old list have moved jobs or changed their details.

Volume also forces you to look past paid databases when the audience is not in them. If the market-sizing prompt says the market lasts about 3 weeks, turn the volume down before you buy inboxes.

```
I sell [what you sell] to [who].
I plan to contact [2,000] new people a day, 3-5 decision makers per company.

1. Split my market into segments: one industry, one region, one size band
   each.
2. Estimate how many companies are in each segment, and say how you got
   each number. Label every estimate as an estimate.
3. For each segment, name where the company data lives: paid databases,
   Google Maps, directories, association lists, job boards.
4. Tell me how many weeks of sending my market can feed at my volume,
   and which segments to add when the first ones run out.

Save it as a table. Don't invent any numbers you can't explain.
```

Verify the list twice before sending: MillionVerifier, then BounceBan on the catch-alls.

## 3. Split every list by receiving provider

Every list goes out as 4 separate campaigns, one per email provider on the other end:

1. Google
2. Outlook
3. Security gateways (Mimecast, Barracuda, Proofpoint, and similar)
4. Personal emails (gmail.com, yahoo.com, outlook.com, and similar)

The personal bucket gets its own sequencer account and its own domains, so it never touches the main sending reputation. Outlook campaigns get a much shorter email, with no signature block and no link. Keep a plain-text opt-out that tells them to reply if they want no further email, and keep the sender's name and postal address. Outlook recipients are not exempt from those. It should still read like a quick note from a coworker.

A domain that matches none of the four tags (Zoho or Fastmail hosted directly, or an MX lookup that failed) stays out of the four sending campaigns. Hold those rows in a manual-review file until they can be classified.

The split exists so that when one provider starts bouncing everything, you can pull that bucket while the other three keep sending. Companies where every contact sits behind a gateway should go to callers. Enterprise inboxes sit behind those gateways, and cold email alone rarely reaches the person who signs at a company with 1,000+ employees.

```
Here's my lead list: [file].

1. Look up the MX record for every email domain on the list.
2. Tag every row: Google, Outlook, Gateway (Mimecast, Barracuda, Proofpoint
   and similar), or Personal (gmail.com, yahoo.com, outlook.com and
   similar).
3. Save 4 campaign files, one per tag. Save every unmatched or unresolved
   domain (Zoho, Fastmail, anything else, or a lookup that failed) in a
   fifth file for manual review. Do not put those rows in the 4 campaign
   files.
4. Give me the count in each file, and flag any company where every
   contact sits behind a gateway.

Don't delete any rows. Do not send the manual-review file.
```

## 4. Write copy that survives being sent at volume

Spam filters read patterns, not just words. The same few lines sent tens of thousands of times is a pattern. The author's copy rules:

1. Spintax on every line, so no two emails match.
2. Change the shape now and then (1 thick paragraph, or a short PS).
3. Write 100k, never 100,000.
4. Keep "$" away from a number ("$ 500" passes, "$500" gets flagged).
5. Subject lines of 1-4 words, all lowercase, no emojis or symbols.
6. Cut these words: free, guaranteed, discount, click here, sign up, and "can I get 15 minutes?"
7. Swap the meeting ask for a permission ask, like "worth a look?" or "can I share it with you?"
8. Keep it to about 30 words. Someone reading 50 cold emails a day gives yours 5 seconds.
9. Skip AI personalisation. The author tested adding it against leaving it out, and adding it made results worse because it added fluff and pulled attention away from the offer. A tight list makes the email relevant without a personalised line.
10. Write 3-5 versions of the email, each with a different offer and everything else the same. Changing "mind if I" to "cool if I" tells you nothing. A different offer tells you which one the market wants.

```
Here's my cold email: [paste it].

1. Check it for spam patterns: trigger words (free, guaranteed, discount,
   click here, sign up), "$" touching a number, commas in big numbers,
   any link, any image, a meeting ask. List every hit with the line it's on.
2. Rewrite it at about 30 words with a permission ask instead of a meeting
   ask.
3. Spin every sentence 3-4 ways in {option|option|option} format.
   Keep the meaning the same. Never spin names, numbers or proof.
4. Write 3 subject lines, 1-4 words, all lowercase.
5. Count the total number of unique emails the spintax can produce.

Then write a shorter Outlook version with no signature block and no link.
Keep a one-line reply opt-out ("reply if you want no further email") and
the sender's name and postal address on that version and on the main version.
```

## 5. Watch inbox health every morning

Burned inboxes rarely die overnight. The reply rate slides first, then the bounces creep up. Catch the slope early and you swap a few inboxes. Leave it and the whole campaign drops while you rebuild infra.

Watch every inbox for bounce rate, reply rate, and whether Google and Outlook are both seeing the emails. The author's thresholds:

1. Bounce over 3%: swap those inboxes.
2. Bounce over 10%: check the list cleaning, then replace them.
3. Reply rate around 0.5% or lower with 3-5% bounce: replace them.
4. Once a month, pull the bottom 20% by reply rate. If 2 inboxes on the same domain are flagged, flag the whole domain.

Plan for every inbox to be replaced. The author says they last 3-6 months on a normal offer, 6-9 on a great one, and about a month on a bad one.

When a winning campaign's reply rate halves overnight and you changed nothing, check the inboxes before the copy. Run a placement test (the author uses EmailGuard or Mailmeteor):

1. Landing in Google, missing Outlook: pull the Outlook side, or rewrite that copy.
2. Landing everywhere, no replies: the copy is stale or the offer stopped working.
3. Landing nowhere: replace the inboxes.

Blacklists, in the author's experience, matter far less than people think.

The sending export does not show which reserve inboxes exist or whether their warm-up is finished. Ask for that inventory before assigning a replacement. A spare that still needs warm-up is not usable.

```
Here's my sequencer export for the last 30 days: [file].
Columns: inbox, domain, emails sent, replies, bounces.
Also attach the reserve inventory: [file].
Columns: inbox, domain, warm-up complete (yes/no), already sending (yes/no).

1. Work out the reply rate and bounce rate for every sending inbox.
2. Flag the bottom 20% by reply rate.
3. Also flag any inbox with bounce over 3%. Flag an inbox at about 0.5%
   reply or lower only when its bounce is also over 3%. Do not flag low
   replies by themselves.
4. If 2 inboxes on the same domain are flagged, flag the whole domain.
5. Assign a replacement only from reserves whose warm-up is already
   complete. If the inventory is missing, or there are not enough warmed
   reserves, report the shortage and do not invent replacements. Say how
   many new inboxes to order to refill the reserve.

Don't pause or change anything in the sequencer.
```

## 6. Turn replies into booked calls

At volume, replies land all day. This is where most teams lose the money they spent on everything above.

The target is a reply inside 1 minute. A rough reply sent fast books more meetings than a perfect one sent a day later. The author's conversion guidance:

1. Inside 5 minutes, about 20-30% of positive replies become meetings.
2. After an hour, it's about 5%.
3. If you take over a day to reply, you have already lost the lead.

How replies reach the author's team:

1. A reply lands in the sequencer.
2. AI tags the intent.
3. Positive replies get a phone number lookup and a CRM record.
4. Everything lands in Slack with the full thread and an AI-drafted answer.
5. The rep sends it, edits it, or calls them.

Then call the positive replies. When they pick up, the author sees 80-90% book, and the call takes about 60 seconds because they replied minutes ago. Offer 2 specific times instead of a booking link, and book inside 2 days. A pre-call workflow (a confirmation with a 60-second "what to expect" video, then reminders by email and text) takes show rate from 20-30% to 60-80%.

On the author's own offer, an AI reply agent that writes and sends the answer (checking the calendar for open times) booked around 10 meetings a week at 4,000 emails a day.

```
Here are yesterday's replies: [paste or file].

Label every reply: interested, wants more info, asking the price,
wrong person, later, out of office, not interested.

For interested and wants more info: draft a 2-3 line answer that
offers 2 specific times from [my calendar].
For asking the price: explain what the price depends on and ask for
7-9 minutes on a call. Never give an exact number.
For wrong person: draft a short email to the person they named,
CC the original contact.
For later: note the date they gave. That is a temporary objection, not an opt-out.
For out of office: note when to put them back in, 7-14 days out.
Split not interested into temporary objections and opt-outs (unsubscribe,
remove me, do not contact, or any request to stop).
Write every opt-out onto the do-not-contact list. That list applies across
every sending account and every provider bucket, and a later refresh must
not put those people back.
List temporary objections separately so they can be reconsidered on the
30-60 day refresh.

Send nothing. Keep everything as drafts.
```

## 7. Judge campaigns on contacts per lead, then scale the winner

Reply rate can climb while nothing gets better, because a reply and a lead are different things. Judge every campaign by contacts per lead: how many people you contacted for every positive reply. The author's ranges:

1. Under 500: a good range, and lower is better.
2. Around 1,000: where offers that catch existing demand sit.
3. 2,000-3,000: the offer or the segment needs to change.

Author examples of where some campaigns landed: manufacturing client 60; construction event client about 99; agency targeting 7-figure ecom brands 266; lending company selling to small businesses about 467; enterprise-focused B2B team 867. Enterprise takes more contacts for every lead, so it needs volume and precision together.

At 4,000 a day you have enough replies inside a week to know which offer is winning. Mark anything under 1,000 people contacted as too early to judge. Flag anything over 2,000 contacts per lead and say whether the offer or the segment looks like the problem. Make one change a week, so you know what moved the number.

```
Here's last week's campaign data: [file].
Columns: campaign, offer, segment, provider bucket, people contacted,
replies, positive replies, meetings booked.

1. Work out contacts per positive reply for every campaign, offer
   and segment. Show the math.
2. Mark anything under 1,000 people contacted as too early to judge.
3. Flag anything over 2,000 contacts per lead and say whether the
   offer or the segment looks like the problem.
4. Name the winning offer and the 2 segments I should scale it into next.

One change only for next week. Don't touch the campaigns.
```

## 8. The 25-day plan and ongoing cadence

1. Before any purchase: size the market with the prompt in section 2. If the market lasts about 3 weeks, or the list cannot feed the planned volume, lower the daily volume and rerun the inbox math. Do not buy domains or inboxes until that is done.
2. Day 1: buy the domains and order the inboxes so warm-up starts the same day.
3. Days 2-14: build the first list from that sizing, verify it twice (MillionVerifier, then BounceBan on the catch-alls), and split it into the 4 provider buckets plus a manual-review file for unmatched domains. Write 3-5 versions of the email with different offers, then run the spam check prompt on each. Set up reply routing into Slack and the pre-call workflow in your calendar.
4. Day 15: cold sending starts at 5 per inbox, plus 1 a day.
5. Day 25: full volume at 15 per inbox, with the reserve warming in the background.
6. Every morning: check bounce and reply rate per inbox. Every positive reply answered inside a minute, and called.
7. Every Monday: check contacts per lead by offer and segment, then make one change.
8. Every month: swap the bottom 20% of inboxes, using only reserves whose warm-up is already complete, and buy new ones to refill the reserve. Report a shortage instead of assigning a reserve that is still warming.
9. Every 30-60 days: re-pull and re-enrich the whole market, then hit it again with a new angle. Before every import and every send, drop anyone on the do-not-contact list. A refresh does not clear opt-outs. Temporary objections can come back; opt-outs cannot.

## Failure modes

The author's 4 ways this can go wrong:

1. A bad offer burns inboxes in about a month, whatever the setup.
2. A market under 10,000 companies runs out before the volume pays off.
3. Enterprise needs the phone from day one, because email alone will not reach the signer.
4. Volume with no one owning the replies wastes every positive you paid for.

## Source

Will Breton, [How To (Safely) Send So Many Cold Emails It Feels Illegal](https://x.com/bretonwill/status/2123035672504045982)
