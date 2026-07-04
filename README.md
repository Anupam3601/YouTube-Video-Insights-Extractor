# YouTube Video Insights Extractor

A lightweight Python automation tool that pulls real-time performance data (views, likes, comments, publish date, channel) for a batch of YouTube videos and writes the results directly into a Google Sheet — built to support creator/campaign performance tracking at scale.

## How it works

1. Paste YouTube Video IDs into the `Input` tab of a connected Google Sheet (Column A).
2. Run the script.
3. It batches the IDs (50 at a time, per YouTube API limits), calls the **YouTube Data API v3**, and writes a formatted results table into the `Output` tab — including a status flag for any IDs that couldn't be found.

## Tech stack

- **Python** – requests, gspread
- **Google Sheets API** + **Google Drive API** (via a service account)
- **YouTube Data API v3**
- `python-dotenv` for local secret/config management

## Setup

1. Clone the repo and install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Create a Google Cloud project, enable the **YouTube Data API v3** and **Google Sheets/Drive APIs**, and generate:
   - A YouTube Data API key
   - A service account JSON (shared with edit access on your target Google Sheet)
3. Copy `.env.example` to `.env` and fill in your values:
   ```
   YOUTUBE_API_KEY=your_key_here
   GOOGLE_SERVICE_ACCOUNT_FILE=service_account.json
   SHEET_URL=https://docs.google.com/spreadsheets/d/your_sheet_id/edit
   ```
4. Place your `service_account.json` in the project folder (it's gitignored, so it will never be committed).
5. Run it:
   ```bash
   python yt_insights.py
   ```

## Why this project

Built to remove manual, repetitive lookups when tracking creator/campaign video performance across a large number of YouTube links — turning a slow spreadsheet task into a one-command batch job.

## Notes

- Handles duplicate Video IDs automatically.
- Respects the YouTube API's 50-ID-per-request batch limit.
- Designed to be run ad hoc or wired into a scheduler (e.g. cron, Task Scheduler) for recurring reporting.
