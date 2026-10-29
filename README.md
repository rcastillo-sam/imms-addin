# IMMS SAM — Outlook add-in

Outlook buttons for **IMMS SAM**, the matter and document management system of the ICAO South American (SAM) Regional Office, built on Microsoft 365 (Power Apps, SharePoint and Power Automate).

The add-in adds an **IMMS SAM** group to the Outlook ribbon with three buttons.

| Button | What it does |
|---|---|
| **Save to matter** | Files the open email (and its attachments) into a matter. The user picks the matter from the list and IMMS files it within a few minutes. |
| **Search matters** | Lists the open matters, newest first, with a search box by number or title. Clicking a matter opens its record in the IMMS app. |
| **IMMS Dashboard** | Opens the IMMS SAM matter dashboard in a separate window. |

## How it works

1. **Matters come from SharePoint.** Each matter is a folder in the `SAMMatters2026` library, with two subfolders: `Correspondence` (emails, saved as `.eml`) and `Documents` (attachments and uploaded files).
2. **Each open matter has an Outlook category** `IMMS · <Matter ID> · <title>`. The flow *IMMS - File tagged emails* (every 5 minutes) creates the category for every open or on-hold matter and removes it when the matter is closed. Closed matters stay in SharePoint and in the IMMS app.
3. **Search matters and Save to matter read those categories**, so a new matter appears in the add-in a few minutes after it is created, whoever creates it.
4. **Save to matter tags the email** with the matter's category and with `IMMS queue`. *IMMS - File tagged emails* finds all queued emails with one search and files each one directly in SharePoint: the email in `Correspondence` and its attachments in `Documents`. **The email stays in the Inbox**; its IMMS categories are replaced by `Filed <Matter ID>`. No Outlook folders are created.
5. **No duplicates.** Every filed email is recorded in the `IMMS_FiledEmails` list and is not filed again.

The add-in itself stores no data and no credentials. Every action runs with the signed-in user's own Microsoft 365 account and permissions, so confidential matters stay restricted to the Directorate and the matter team.

## Files

| File | Purpose |
|---|---|
| `manifest.xml` | Add-in definition: buttons, labels, icons and the pages they open. |
| `taskpane.html` | The side panel: matter list, search, *Save to matter* and *Open in IMMS*. |
| `open.html` | Opens the IMMS app in a separate window. It only opens the IMMS SAM app address. |
| `*.png` | Button and add-in icons. |

The files are published with GitHub Pages at `https://rcastillo-sam.github.io/imms-addin/`.

## Current status (pilot)

- During the pilot, the Outlook buttons are used **only by the IMMS administrator**.
- Pilot users do everything **from the IMMS app** (in Microsoft Teams or the browser): *Add emails*, *Add documents*, *Update status*, *Team* and *Close matter*. This keeps one single way of working and avoids emails that look filed but are not.
- Rolling the buttons out to all users will require a service account from ICAO HQ, so that filing does not depend on one person's mailbox.

## Contact

IMMS SAM administrator: Roman Castillo Arce (ICT focal point, ICAO SAM Regional Office).
