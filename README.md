# Meta Ads Strategist — a Claude Code skill

A [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that turns Claude into a senior Meta (Facebook / Instagram) performance marketer. It audits ad accounts, writes campaign plans a client can act on, and, only when you ask, builds draft campaigns in Ads Manager through a browser.

It works from evidence: every recommendation should cite a number from the account, the store or a named source. It checks the unit economics before touching targeting, and it stays read-only in Ads Manager unless you approve a change.

## What it does

| Mode | What you get |
|---|---|
| **Audit** | Spend by optimisation goal, tracking and CAPI checks, placement / age / geo breakdowns, structure, creative, audiences, website quick fixes. Written up with `templates/audit-report.md`. |
| **Campaign plan** | A recommendation table, what to settle with the client before launch, structure / audience / placements with reasons, 4–8 distinct creative concepts, expected results as ranges, how to judge it, a dated timeline. Written up with `templates/campaign-plan.md`. |
| **Build** | Draft campaigns, ad sets, ads and audiences in Ads Manager via browser tools. It leaves them as drafts and reports exactly what was created. |
| **Review** | Weekly checks: store revenue vs spend, frequency, kill / rotate rules. |

Playbooks included: small-budget e-commerce, dated promotions with a spend threshold or prize draw, local store / showroom promotions, leads / messages / WhatsApp, instant-form lead gen, diaspora / cross-border gifting, retargeting, awareness.

## Install

Skills live in `~/.claude/skills/<skill-name>/`. Clone this repo straight into that folder:

```bash
git clone https://github.com/nimsaraakash/meta-ads-strategist.git ~/.claude/skills/meta-ads-strategist
```

To use it in one project only, clone it into that project's `.claude/skills/` instead:

```bash
git clone https://github.com/nimsaraakash/meta-ads-strategist.git .claude/skills/meta-ads-strategist
```

Start a new Claude Code session afterwards so the skill is picked up. Check that it loaded by asking Claude "what skills do you have?" or by typing `/meta-ads-strategist`.

### Update

```bash
git -C ~/.claude/skills/meta-ads-strategist pull
```

## Using it

Claude loads the skill on its own when a request matches, for example:

- "Audit this Meta ad account for the last 90 days."
- "Why is our ROAS so low?"
- "Plan a two-week Facebook campaign for this promo, budget $600."
- "What creatives should we run for Christmas?"
- "Set up retargeting audiences."

You can also call it directly: `/meta-ads-strategist audit act=<AD_ACCOUNT_ID>`.

### Give it context

Results are only as good as the inputs. Before an audit or plan, give Claude (or let it ask for):

- What is sold, price points / average order value, margin if known, markets and currency.
- Monthly budget and what "success" means for the client.
- Ad account ID, pixel / dataset, account timezone.
- Store or back-end numbers for the same period (orders, revenue), so Meta's figures can be checked.

### Ads Manager access

For live audits and builds, Claude needs a browser it can drive (Claude in Chrome or the Claude desktop app's built-in browser) that is already signed in to the right Meta Business account. Read `references/ads-manager-ops.md` for the tested tricks (URL parameters, wide viewport for the virtualised tables) and the safety rules. Without browser access, export reports from Ads Manager as CSV and share them instead.

### Keep client notes in the project, not in the skill

Work on each client in its own project folder. The skill tells Claude to write durable facts (account IDs, decisions, what was built) to that project's `CLAUDE.md`. Keep this skill folder free of client data so it stays shareable.

## Safety rules built in

- Read-only by default. No publishing, pausing, budget changes, or accepting terms / tax / billing dialogs without your explicit approval.
- New ads are left as drafts.
- Never lifts access tokens from the page to call the Graph API.

## Files

```
SKILL.md                         Entry point: principles and workflow
references/
  audit-checklist.md             Step-by-step account audit
  campaign-playbooks.md          Playbooks by business type / goal
  creative-andromeda.md          Creative strategy under Meta's Andromeda delivery
  measurement-and-math.md        Unit economics, sample sizes, budgets, kill rules
  ads-manager-ops.md             Working in Ads Manager / Events Manager safely
  platform-changes.md            Dated log of Meta platform changes
templates/
  audit-report.md                Audit write-up
  campaign-plan.md               Campaign plan write-up
```

## Keeping it current

Meta changes every month. `references/platform-changes.md` reflects what was known in **October 2026**; most entries come from agency and vendor blogs, and single-source items are marked. The skill tells Claude to re-check a fact with a web search before a recommendation depends on it. When you confirm something new, add a dated row to that file.

To change how the skill behaves, edit `SKILL.md` (workflow and principles) or the files in `references/`. Keep `SKILL.md` short; detail belongs in the references, which Claude reads only when needed.

## Contributing

Open a pull request or issue. Please don't commit client names, account IDs, screenshots or exports.
