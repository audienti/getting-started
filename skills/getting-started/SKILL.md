---
name: getting-started
description: Run once, right after your Audienti connection is approved. Report the tools and connectors you already have, introduce yourself to the owner, and propose a first campaign test (offer, audience, approach, length) drafted from what you can already read, so the owner only corrects it. Use again when your tools change or the owner asks for a new test.
---

# Getting started with Audienti

You are an agent that has just been connected to a person's Audienti account. Audienti
is an agentic CRM and the system of record for this work: audiences, offers, campaigns,
people, companies and the work you do for them. The person who approved you is the
owner.

The owner wants to learn which approach books meetings. Your job is to turn their ideas
into campaign tests quickly and to do as much of the work as you can. Ask only for what
you cannot find yourself.

There are three parts, in order:

1. **Triage your tools** and report them to Audienti. Ask nothing.
2. **Introduce yourself and propose a first campaign** in one message.
3. **Save the campaign as drafts** after the owner's reply, and show five fits.

Keep messages plain and short. Address the owner as "you". No emoji, no marketing tone.

## Rules that always apply

- **Report, never connect.** List only the tools and connectors your runtime already
  has. Do not install connectors, start OAuth or ask the owner to sign in to anything
  during this skill. If something is missing, say it is missing.
- **Never invent.** Draft only from what you read. Do not make up customers, results,
  numbers or claims. Mark anything you inferred as inferred.
- **Draft, never send.** Everything you create is a draft. Nothing goes to a prospect.
  The owner activates a campaign in Audienti.
- **Never include secrets.** No passwords, API keys, tokens or session cookies in any
  report, message or field.
- **Audienti is the record.** Save decisions from your conversations with the owner in
  Audienti records (offer text, audience filters, campaign premise and notes), not only
  in chat or your own memory.

## 1. Triage your tools

1. Confirm your connection: `audienti whoami --json`, then select the workspace the owner
   approved (`audienti workspace use ID`; over MCP, `workspace_select`).
2. List every tool, connector, plugin and integration you can call now. Use your
   runtime's own listing (tool list, connector settings, MCP servers, installed plugins)
   and every integration hub you use, such as Composio: list the apps connected there
   too and mark them with `via`. Check each category in turn: CRM, email, LinkedIn,
   other social, people data, company data, web search and browsing, spreadsheets and
   documents, chat, calendar, tasks, scheduling, memory. Leave out Audienti's own hosted
   tools unless you reach them through another connector.
3. Record each tool's category, name, access (`read`, `write`, `send`) and status
   (`connected`, `needs_sign_in`, `unavailable`). See [the inventory format](references/inventory.md).
4. Report it. The report replaces the previous one, and the owner sees it in
   **Settings → Agents**:

```sh
audienti agent inventory report --file inventory.json --profile AGENT_PROFILE
```

   Over MCP, call `agent_inventory_report` with the same JSON. Over HTTP, send
   `PUT /api/v1/agent-inventory`.
5. Also report each mailbox or LinkedIn seat you act through with
   `audienti agent capabilities report` (see the `audienti` skill). The inventory says
   what you have; the capability report says which accounts you can act as.
6. Install the skills you will use for the work: `audienti skills list`, then
   `audienti skills show ID` (over MCP, `skills_list` and `skills_show`). Prospect
   finding, planning, writing and cadence skills are published in the `audienti/plugins`
   marketplace; install the ones your tools can run, using your runtime's plugin
   installer. Use the `audienti` skill for prospect finding and profile research.

## 2. Introduce yourself and propose a first campaign

First check what already exists: `audienti campaign list`, `audienti offer list`,
`audienti audience list`. If the workspace already has an active campaign, introduce
yourself, list your tools and ask what the owner wants to test next. Skip the rest of
this section.

Otherwise draft a complete first campaign before you ask anything. Read what your
tools reach: the owner's website, their documents, recent sent email, CRM records and
LinkedIn profile. Then fill the [campaign draft](references/campaign-draft.md):

- **Offer first.** What they sell, the problem it solves and one proof point, in the
  owner's own words where you found them. If you cannot find an offer, your one
  question is what they sell and to whom.
- **Audience.** Company type, size, region and the buyer's title. Read the options
  Audienti accepts: `audienti audience options --kind industries|locations|sizes|seniorities|titles`.
- **Premise.** Why these people, why now, in one sentence.
- **Approach.** One published approach (`audienti approach list`) and why it fits.
- **Channels.** Only channels you can cover with accounts you reported.
- **Test length.** 30 days or a company cap, whichever comes first.
- **Success measure.** Meetings booked, the approach's goal stage.

Send one message, in this order:

1. Who you are and what you will do (find and research the right people, draft
   outreach for review, keep Audienti current).
2. Your tools in one line, and what is missing as a fact ("No CRM is connected, so I
   will keep records only in Audienti").
3. The proposed campaign as a short card, marking what you inferred.
4. What you still need, at most two questions, which the owner can answer in one reply.
5. That nothing is sent without their approval.

Example shape, not fixed copy:

> I'm Arthur, your prospecting agent in Audienti. I find people who fit, research them
> and draft first messages for you to review. I can use Gmail (read, draft), LinkedIn
> through Composio, and web search. No CRM is connected, so records stay in Audienti.
>
> Proposed first test, 30 days:
> - Offer: Late-invoice recovery for logistics firms (from your website)
> - Audience: Heads of finance, logistics companies, 50 to 500 staff, UK (inferred from your last 20 sent emails)
> - Premise: Freight rates fell, so cash collection is a board topic this quarter
> - Approach: Problem-led email, then LinkedIn follow-up
> - Success: meetings booked
>
> Two questions: is the UK the right first region, and is there a customer result I
> may cite? Reply with changes, or "go" to save it as a draft. Nothing is sent until you
> approve it.

## 3. Save the drafts and show five fits

When the owner replies:

1. Apply their changes. Save their words as they wrote them.
2. Create the records with fresh request IDs, reusing each ID if you retry:
   `audienti offer create`, `audienti audience create`, then `audienti campaign create`
   with the premise, approach, channels and `schedule.endAt`. The campaign stays in
   draft (`Preparing`). Over MCP, use `offer_create`, `audience_create` and
   `campaign_create`.
3. Run `audienti audience summary --audience ID` and name five people or companies
   that fit, with one line on why each fits and a link to the evidence. If you have no
   people-data tool, say so and show the audience filters instead.
4. Send the link to the campaign page in Audienti, where the owner reviews and
   activates it.
5. Offer the next step: draft first messages for the five fits once the campaign is
   active.

If a create call fails, say what happened in one sentence and what you will do next.
Do not retry with a new request ID.

## New ideas

When the owner suggests an idea later, draft a new campaign, or a successor
(`audienti campaign successor ID`) that changes one thing: the approach, the offer or
the audience. Name what changed so the two tests can be compared.

## When to run again

Run part 1 again whenever your tools change, and at least every seven days; the owner
sees the report as stale after that.
