# QA Weekly Report

The QA team's weekly activity: hours per person and project, testing hours, and bug counts.

**Site:** https://dandanica.github.io/qa-weekly-report/

This repo only holds the published site (`index.html`, `data.js`). It is updated by Danica's weekly run and shows numbers only, never task titles.

## For Angelica: send your week (Windows)

Your ESS password stays on your computer. The export only reads ESS (it never adds or changes anything), saves your week to one file, and you send that file to Danica.

You need the file **`qa-weekly-export.zip`**. Ask Danica for it (it is not stored in this public repo).

### One-time setup (about 10 minutes)

1. Unzip it, for example to `C:\Users\<your name>\qa-weekly-export`.
2. Install **Python 3.10 or newer** from https://www.python.org/downloads/. On the first screen tick **"Add python.exe to PATH"**, then Install.
3. Open the unzipped folder in File Explorer, click the address bar, type `cmd` and press Enter. A Command Prompt opens in that folder.
4. Run these two commands, one at a time (the second downloads a browser the tool uses, about 150 MB):
   ```
   py -m pip install playwright
   py -m playwright install chromium
   ```
5. Add your ESS login:
   ```
   copy env.example.txt .env
   notepad .env
   ```
   Type your ESS email after `ESS_EMAIL=` and your password after `ESS_PASSWORD=`. The ESS address is already filled in. Save and close. **Never send or share the `.env` file.**

### Every Friday, after your ESS entries for the week are in

Double-click **`run-weekly.bat`**, or in the Command Prompt run:

```
py export_my_week.py
```

For an earlier week (the date must be a Monday):

```
py export_my_week.py --week-start 2026-11-23
```

When it says "Done", it prints the file to send:

```
output\2026-11-30\angelica.json
```

Send that one file to Danica (company chat or email, not a group channel, because it contains your task titles).

### If something goes wrong

| Message | Fix |
|---|---|
| `py is not recognized` | Reinstall Python and tick "Add python.exe to PATH". |
| `ESS login failed` | Check the email and password in `.env`. |
| `week_start must be a Monday` | Use a Monday date after `--week-start`. |
| Anything else | Send Danica a screenshot. The tool never prints your password. |

## For Danica: add her file and publish

From the tool folder on your Mac:

```
python3 -m qa_report.import_week ~/Downloads/angelica.json   # checks the file, then adds it
./scripts/friday.sh                                           # reads ESS and GitHub, rebuilds, publishes
```

The import refuses anything that is not a valid week export. Angelica's GitHub numbers need nothing from her: her username goes in `config.json` and the Mac reads them.
