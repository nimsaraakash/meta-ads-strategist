# Working in Ads Manager and Events Manager

## Safety rules

- Read-only unless the user explicitly asks for changes. Report every change made.
- New ads/campaigns are left as **drafts** for the user to review and publish unless told otherwise.
- Status toggles (pause/activate) and budget edits apply live — confirm first.
- Never accept terms, tax/ABN/GST/VAT dialogs, or billing prompts; those belong to the business owner.
- Editing a live ad set re-triggers review; ads may show "Processing"/"inactive" briefly. Check it returns to Active.

## Navigation

- Ads Manager may open on a different (personal) ad account. Append `?act=<AD_ACCOUNT_ID>` to the URL to land on the right one.
- If several browser profiles exist (one signed in to the store, another to Meta), switch profile per task.
- Ad Library (facebook.com/ads/library) is the competitor-research tool: filter by country, active ads, keyword.

## Reading data efficiently (tested)

- URL parameters work and are faster than menus:
  - `&date=YYYY-MM-DD_YYYY-MM-DD` sets the date range.
  - `&impression_breakdown=device_platform,platform_position,publisher_platform` gives the placement breakdown; `&impression_breakdown=age` gives age (others likely follow the same pattern, e.g. `gender`, `country`).
  - `&column_preset=<id>` reapplies a saved column set (the id appears in the URL after saving columns).
  - Swap `/campaigns` for `/adsets` or `/ads` to change level.
- Set the browser viewport very wide and tall (e.g. 4200×2600, or taller for breakdowns) so the virtualised table renders all columns and rows. Then read cells by position: column header x-ranges plus row y (anchor rows on the "Amount spent" cell). `get_page_text` alone loses which "—" belongs to which column.
- Age labels may use an en dash (`25–34`); match `\d\d\D\d\d`.
- Very long tables still virtualise vertically. Filter or narrow the date range rather than scrolling.
- Customising columns saves a new column preset (e.g. "Copy of Performance"). It's harmless, but tell the user.
- Dropdown menus (Columns, Breakdown) close between separate tool calls. Open and choose in **one** batched call, using coordinates found from a screenshot.
- Do **not** try to lift the session access token from the page to call the Graph API. Read through the UI or ask the user for an export.
- Opening an ad set's Edit view can show "Discard Draft" / "Publish". Leave by navigating away; never click either.
- Reset the viewport to desktop when done.

## UI quirks

- The reporting table is **virtualised**: off-screen columns only render after scrolling the horizontal bar. Prefer Breakdown menus and exports, or read via screenshot.
- Breakdowns to use: Age, Gender, Placement (platform + position), Country/Region, Time.
- The Upload button's file input only appears in the DOM after the button is clicked; capture it at click time before attaching a file.
- In bulk "edit copies" views, URL and headline fields may only save after pressing Tab.
- When creating a Page/Instagram engager audience, the Page selector may default to an unrelated page — always check.
- Audience size estimates ignore Advantage+ expansion; adding small custom audience suggestions can make the estimate read "Below 1,000" without limiting delivery.
- Lookalike creation silently fails if the source audience is still populating — retry once it shows 100+.
- Meta AI enhancements (image/video touch-ups, text rewrites, catalogue carousel variant) are often on by default per ad; check each.

## Events Manager

- Check pixel + Conversions API both connected and **deduplicated** (compare Purchase count with store orders).
- Event match quality per event; Purchase must carry value and currency.
- Store-platform integrations (Shopify, WooCommerce) usually send CAPI automatically.

## Naming convention (suggested)

`<Objective> | <Budget type> | <Market> – <Theme/Offer> | <MMM YY>` for campaigns, `<Audience/geo> | <Note>` for ad sets, `<Concept> | <Format> | <MMM YY>` for ads, `<Prefix> | <Audience type> | <Window>` for custom audiences (e.g. `XX | Website visitors | 180d`). Names must say what the campaign actually optimises for.

## Timezones

Convert offer start/end from local time to the **account** timezone when scheduling; write both in the plan.

## After building

Record in the project's CLAUDE.md: IDs, what was created, what is live vs draft, settings left on, and open follow-ups.
