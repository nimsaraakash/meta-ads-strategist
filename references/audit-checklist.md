# Meta ad account audit checklist

Work through in order. Record the period, the account timezone and currency at the top of the audit.

## 1. Money by what Meta was told to optimise for

Build this table first; it usually explains most of the account.

| Optimisation goal | Spend | Share | Purchases / leads / calls | Cost per result |
|---|---|---|---|---|
| Awareness (reach / impressions) | | | | |
| ThruPlay / video views | | | | |
| Traffic (link clicks / landing page views) | | | | |
| Sales (purchase / add-to-cart) | | | | |
| Engagement / messages / calls / profile visits | | | | |

Red flags:
- Most of the budget on reach/ThruPlay while a small sales/traffic slice produces most purchases.
- Campaign **names** that don't match the actual objective (e.g. "awareness" that is really sales, "traffic" that is really reach). Check the objective, not the name.
- Campaigns whose Results column shows "—" despite real spend (common for message campaigns). Either results aren't being counted or the metric was renamed (e.g. "Messaging contacts"). Add the alternative column and check the inbox before calling it zero.
- Link CTR above ~10% on any ad set is almost always Audience Network or accidental taps, not interest. Break it down by placement.
- Sales campaigns optimised for add-to-cart when purchase volume would allow purchase optimisation (or vice versa: purchase optimisation with <10 purchases/week, where ATC may be the better signal).

## 2. Tracking and measurement

- Is **purchase value and currency** passed on the Purchase event? Without it, ROAS and value optimisation are impossible.
- Is the **Conversions API** connected? If both browser pixel and CAPI send, check **deduplication** (event_id). Symptom: Meta Purchase count > back-end orders.
- Event match quality per event (aim 6+ for upper funnel, 8+ for Purchase).
- Pixel purchases vs Meta-attributed purchases vs store orders for the same window. Report all three.
- Attribution setting (default 7-day click / 1-day view). Click attribution now counts link clicks only.
- Account **timezone** vs business timezone — daily reports and schedules shift. Changing it on an existing account has consequences; flag, don't change.
- Catalogue connected? Needed for dynamic/Advantage+ catalogue ads at larger budgets.
- Bot/data-centre traffic in store analytics (unexpected US cities, e.g. data-centre towns) deflates conversion rate.

## 3. Structure

- Number of campaigns launched in the period; average spend per campaign.
- Ads per ad set. One-ad ad sets (often boosted posts) = nothing is tested and Creative Diversity will be Low.
- Ad sets that can never exit learning (need ~50 optimisation events/week). At small budgets "learning limited" is normal; judge on results.
- Duplicate/overlapping ad sets with the same interests/geo competing against each other; per-ad-set frequency caps don't protect a person from being hit by several ad sets.
- Finished campaigns still switched Active — clutters the account and hides what is really running.
- Campaigns with daily budgets and no end date that belong to a past occasion.

## 4. Delivery breakdowns

Pull each with spend, results and cost per result:
- **Age and gender** — where do results come from vs where spend goes? Reach/awareness optimisation drifts to the cheapest demographic.
- **Placement** — Audience Network (esp. rewarded video in games), in-stream, Reels with static images, Threads. Feed vs Reels connect rates for call ads (accidental taps).
- **Geography** — cheap CPM countries/regions with zero downstream results; markets the offer can't serve.
- **Frequency** — any ad set above ~4–5 on one creative with weak results.
- Link CTR and landing page view rate (LPV / link clicks). Below ~60% suggests slow mobile pages or junk placements.

## 5. Creative

- Count genuinely distinct concepts (different message *and* different visual world). Template variants count as one.
- Aspect ratios: 4:5 for feed, 9:16 for Stories/Reels. 2:3 or 1:1 artwork gets cropped.
- Is there a way to buy? Boosted posts with "Message / Call / See details" and no link produce near-zero link CTR.
- Offer, price, delivery promise, CTA present? Language matches the audience?
- Meta quality / engagement / conversion rankings per ad.
- AI-generated product renders that may not match what the customer receives.
- Format mix: static vs video vs carousel; is video actually getting delivery?

## 6. Audiences

- Custom audiences that exist vs are used. Website visitors, add-to-cart, purchasers, page/IG engagers, video viewers, customer list.
- Duplicates and audiences too small to use (<1,000).
- Are purchasers excluded from prospecting where appropriate?
- Lookalike eligibility (100+ source people from one country).

## 7. Organic page (if in scope)

- Followers, engagement per post as % of followers (benchmark ~0.1–0.2% median for Facebook pages), boosted vs unboosted medians.
- Format mix vs what earns engagement (video vs photo).
- Captions: questions asked? prices? shop link? walls of abstract adjectives?
- Posting volume vs quality; real people / events / creators / behind-the-scenes present?

## 8. Website / conversion path (zero-cost fixes)

- Placeholder policy pages (shipping, refund), theme leftovers (size guide, compare, pickup errors).
- Product facts missing (weight, pieces, dimensions, delivery time).
- Shipping cost as % of a typical order; free-shipping threshold set just above typical AOV and announced.
- Reviews/social proof visible on product pages.
- Abandoned-checkout email on? Email capture?
- Mobile share of sessions and mobile page speed.
- Bundles or kits to lift AOV.

## 9. Account settings to check

- Advertising settings: any switch letting Meta show AI-generated landing pages or rewrite text — usually off.
- Advantage+ creative enhancements (text rewrites, image touch-ups, music) — decide per ad, set brand restricted words.
- Pending terms or tax dialogs — the business owner should accept, not the operator.

## Output

Use `templates/audit-report.md`. Group findings by theme, numbered, each with the number that proves it. End with "What to fix first" ordered by impact, then "Not checked" and sources.
