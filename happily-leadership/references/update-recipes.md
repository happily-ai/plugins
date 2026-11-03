# Update recipes for key results

An update recipe is plain text in a key result's `description`. It tells anyone, person or assistant, how the key result's number is found and refreshed. Keep it short and specific enough that two people following it get the same number. Add a new worked example below whenever a new kind of source is set up.

## Format

```
How this is updated
Source: <app and object, e.g. HubSpot deals>
What counts: <filters, in plain words, including the time window>
Value: <the field and how it's combined, with unit and currency>
Owners: <how each owner's number is found, for key results split by owner>
Cadence: <weekly / monthly / quarterly, and the day>
Note: <what the update note says, key fact first>
Hold when: <situations where an update is left out and why>
```

Leave out lines that don't apply. The description is limited to 2,000 characters.

## Choosing a cadence

Match the cadence to how often the source changes and how often people act on it:

- **Weekly:** sales pipeline, leads, tickets, deploys and other numbers that move most days.
- **Monthly:** revenue booked, monthly traffic, churn, survey results reported monthly.
- **Quarterly or at the end of the cycle:** totals that are only meaningful once a period closes.

A refresh with no change still counts as checked. Skip the update rather than logging the same number with no news, unless the recipe says otherwise.

## Worked example: weighted active pipeline from HubSpot

Key result: "Hold THB 1,168,000 weighted active pipeline" (Happily.ai, Q4 2026). Each of five owners has their own target, and each owner's number is the weighted value of their own active deals.

```
How this is updated
Source: HubSpot deals.
What counts: open deals (not closed won or closed lost) whose last activity date is within the last 60 days.
Value: sum of "Weighted amount in company currency" (THB; USD deals are converted by HubSpot).
Owners: each person's number is the deals they own in HubSpot.
Cadence: weekly, Monday morning (Asia/Bangkok).
Note: "HubSpot: THB <total> weighted across <n> active deals (activity in the last 60 days, since <date>). Largest: <deal> <value>, …; +<k> more."
Hold when: a person's active deals have no amount, so their weighted value is 0 only because the data is missing. Ask them to add amounts.
```

How it was pulled (HubSpot connector, `query_crm_data`):

```sql
SELECT hubspot_owner_id, COUNT(*), SUM(hs_projected_amount_in_home_currency)
FROM DEAL
WHERE hs_is_closed = 'false' AND notes_last_updated >= '<today minus 60 days>'
GROUP BY hubspot_owner_id
```

Then one query per owner, `ORDER BY hs_projected_amount_in_home_currency DESC`, to list the largest deals for the note.

Lessons from setting it up:

- **Count with `COUNT(*)`.** `COUNT(hs_object_id)` adds up record ids rather than counting records.
- **Use home-currency fields.** `amount` is in each deal's own currency; `_in_home_currency` fields are converted.
- **"Active" means last activity, not creation.** `notes_last_updated` is the last logged call, email, meeting, note or task. Creation date drops older deals that are still alive. Modified date counts automated edits.
- **Map owners deliberately.** HubSpot owners are matched to Happily people by name and email (`get_organization_details` with TEAMS, or `search_owners`). Write the mapping into the recipe if names differ.
- **Weighted pipeline is a balance, not a total.** Each update records the current value, which can go down, not an amount added that week.
- **Watch data gaps.** Deals with no amount, close dates in the past and long-untouched open deals all distort the number. Say so in the note or hold the update rather than logging a misleading value.
