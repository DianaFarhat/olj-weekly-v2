# OLJ / OT analytics reports

| File | What it is |
|---|---|
| `weekly_report.ipynb` | Weekly brief, OLJ + OT (CMS, GA4, Matomo, Search Console) |
| `monthly_report_matomo.ipynb` | Monthly report, OLJ + OT (Matomo, CMS, GA4) |
| `.github/workflows/weekly_brief.yml` | **Weekly brief · part 1**: Mondays 11:25 Beirut, emails you the Claude.ai file, sends no briefs |
| `.github/workflows/weekly_brief_part2.yml` | **Weekly brief · part 2**: run by hand with Claude's answer, builds and sends the briefs |
| `.github/workflows/monthly_report_matomo.yml` | **Monthly report · Matomo**: the 1st of each month 09:00 Beirut, builds and sends last month's report |

## Weekly routine
1. Monday, part 1 runs by itself and emails you `Claude_translations_<week>.txt`.
2. Attach it in claude.ai and send. Copy Claude's answer (the JSON line at the end is enough).
3. Actions -> **Weekly brief · part 2** -> Run workflow -> paste the answer -> Run. Do it by Sunday.

Who gets the briefs is set by `SEND_TO` in the notebook's ⚙️ Settings: `"test"` = `TEST_RECIPIENTS` only,
`"everyone"` = each brand's list.

## Setup (Settings -> Secrets and variables -> Actions)
**Secrets** (used by all three workflows)
- `CMS_API_KEY`
- `MATOMO_TOKEN`
- `GSHEET_SA_KEY`: the whole service-account JSON (GA4, the acquisitions sheet, Search Console)
- `GMAIL_ADDRESS`, `GMAIL_APP_PASSWORD` (a Gmail App Password, not the normal password)

**Variables** (optional; comma-separated emails that replace the lists in the notebooks)
- `BRIEF_RECIPIENTS_OLJ`, `BRIEF_RECIPIENTS_OT`: weekly, used only when `SEND_TO = "everyone"`
- `MONTHLY_RECIPIENTS_OLJ`, `MONTHLY_RECIPIENTS_OT`: monthly, scheduled run only

## Outputs
Every run keeps its files as a download on the run page (Artifacts): the executed notebook, the Word files, and
the Claude.ai file / Excel files. Nothing is committed back to the repo.

## Running in Colab instead
Add the same names as Colab 🔑 secrets (`CMS_API_KEY`, `MATOMO_TOKEN`, `GA4_SA_KEY` with the service-account JSON,
Notebook access on) and run top to bottom. Emails ask y/N before sending.
