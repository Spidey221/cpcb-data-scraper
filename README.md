# CPCB Water Quality Data Scraper

Fetches real-time water-quality data from the CPCB (Central Pollution Control
Board) API and saves it as a timestamped CSV file
(`water_data_YYYY-MM-DD_HH-MM.csv`).

## How it works

- [cpcb_scraper.py](cpcb_scraper.py) hits the CPCB API and writes a new CSV each run.
- [.github/workflows/scraper.yml](.github/workflows/scraper.yml) runs the script every hour
  (`cron: '0 * * * *'`) via GitHub Actions and commits the new CSV back to the repo.
- You can also trigger a run manually from the **Actions** tab
  (`workflow_dispatch`).

## Weekly archive steps (manual)

Since CSVs accumulate every hour, archive and clear them weekly:

1. Pull the latest changes: `git pull`
2. Create/update an archive folder for the week, e.g. `archive/2026-W06/`.
3. Move that week's CSVs into it:
   ```bash
   mkdir -p archive/2026-W06
   mv water_data_*.csv archive/2026-W06/
   ```
4. Commit and push:
   ```bash
   git add archive/
   git commit -m "Archive week 2026-W06 data"
   git push
   ```
5. Repeat weekly, updating the archive folder name.

(Optional: zip/compress each week's archive folder to save space, or move
older archives out of the repo entirely into external storage.)
