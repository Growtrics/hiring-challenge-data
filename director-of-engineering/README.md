# Take-home data pack

All data in this pack is synthetic. The product, the company, the customers and the people are fictional, and any resemblance to real ones is coincidence.

The fictional company, Kestrel Labs, sells an AI testing service. Its AI agents run customers' mobile apps on a rented device farm and send the customers bug reports.

## Files

| File | What it contains |
|---|---|
| `system_note.md` | How the testing pipeline works today, with a diagram |
| `cost_log.csv` | Every test run in August 2026: model spend, device minutes, retries, reports sent and reports the customer accepted |
| `bug_reports.csv` | A sample of 60 of the 3,618 reports sent in August, each with a category, a summary and the customer's verdict |
| `team.csv` | The six engineers, their role (tech lead or engineer), their skills and their leave days per sprint |
| `leave_calendar.csv` | The dates of that leave |
| `commitments.md` | Work already agreed for the next two sprints |
| `constraints.md` | Limits that apply this quarter |

## Dates

- The next two sprints run from 2026-10-05 to 2026-10-30. Each sprint is two weeks, ten working days.
- Costs are in US dollars.

## Column notes for `cost_log.csv`

- `explorer_model_usd` and `reporter_model_usd`: model spend on the first attempt of the run.
- `device_minutes` and `device_usd`: device farm time on the first attempt.
- `retries`: how many times the run was retried.
- `retry_model_usd`, `retry_device_minutes` and `retry_device_usd`: spend on those retries.
- `total_usd`: everything above, summed.
- `reports_sent`: bug reports sent to the customer from this run.
- `reports_accepted_by_customer`: reports the customer marked as a real bug.
