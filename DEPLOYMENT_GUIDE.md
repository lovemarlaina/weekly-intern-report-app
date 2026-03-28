# Catalyst Bridge — Weekly Intern Report
## Deployment Guide (Step-by-Step)

---

## What You're Setting Up

You're deploying the Weekly Intern Report form as a Google Apps Script web app. When complete, you'll have:

- **A shareable URL** that interns open to fill out the form
- **A Google Sheet** that automatically captures every submission
- **A Google Drive folder** that stores uploaded progress report files
- **Automatic emails** — a copy to the intern (if requested) and a notification to the program lead and program staff on every submission
- **HTTPS encryption** — built into Google Apps Script automatically

---

## What You Need Before Starting

- Access to a Google account with Catalyst Bridge's Google Workspace (any @catalystbridge.org account)
- About 20–30 minutes

---

## Step 1: Create the Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com)
2. Click **+ Blank** to create a new spreadsheet
3. Rename it: **"Intern Weekly Reports — Submissions"**
4. Copy the **Sheet ID** from the URL — it's the long string between `/d/` and `/edit`
   - Example URL: `docs.google.com/spreadsheets/d/`**`1aBcDeFgHiJkLmNoPqRsTuVwXyZ`**`/edit`
   - Your Sheet ID: `1aBcDeFgHiJkLmNoPqRsTuVwXyZ`
5. **Write down your Sheet ID** — you'll need it in Step 4

---

## Step 2: Create the Google Drive Folder

1. Go to [drive.google.com](https://drive.google.com)
2. Click **+ New** → **Folder**
3. Name it: **"Intern Reports — Uploaded Files"**
4. Open the folder
5. Copy the **Folder ID** from the URL — it's the string after `/folders/`
   - Example URL: `drive.google.com/drive/folders/`**`1xYzAbCdEfGhIjKlMnOp`**
   - Your Folder ID: `1xYzAbCdEfGhIjKlMnOp`
6. **Write down your Folder ID** — you'll need it in Step 4

---

## Step 3: Create the Apps Script Project

1. Go to [script.google.com](https://script.google.com)
2. Click **+ New project**
3. Click "Untitled project" at the top and rename it to: **"Catalyst Bridge Intern Report"**

### Add the backend code (Code.gs):
4. You should see a file called `Code.gs` already open
5. **Delete everything** in the editor
6. Open the **Code.gs** file provided to you
7. **Copy and paste the entire contents** into the editor

### Add the form (Form.html):
8. Click the **+** button next to "Files" in the left panel
9. Select **HTML**
10. Name the file: **Form** (not Form.html — Google adds .html automatically)
11. **Delete everything** in the new file
12. Open the **index.html** file provided to you
13. **Copy and paste the entire contents** into the editor

You should now have two files in the left panel:
- `Code.gs`
- `Form.html`

---

## Step 4: Configure Your Settings

1. Click on **Code.gs** in the left panel
2. Find the `CONFIG` section near the top (around line 17)
3. Replace the placeholder values:

```
SHEET_ID: 'PASTE_YOUR_GOOGLE_SHEET_ID_HERE',
↓ change to ↓
SHEET_ID: '1aBcDeFgHiJkLmNoPqRsTuVwXyZ',    ← your Sheet ID from Step 1
```

```
DRIVE_FOLDER_ID: 'PASTE_YOUR_DRIVE_FOLDER_ID_HERE',
↓ change to ↓
DRIVE_FOLDER_ID: '1xYzAbCdEfGhIjKlMnOp',     ← your Folder ID from Step 2
```

```
'staff@catalystbridge.org'      // Update with program staff's actual email
↓ change to ↓
'sarah.sorderberg@catalystbridge.org'    ← use program staff's real email address
```

4. Click **Save** (Ctrl+S or Cmd+S)

---

## Step 5: Test Your Configuration

1. In Code.gs, click anywhere inside the `testSetup` function
2. At the top of the editor, click **Run** (the ▶ play button)
3. Google will ask you to **authorize permissions** — this is normal:
   - Click "Review permissions"
   - Choose your Catalyst Bridge Google account
   - If you see "Google hasn't verified this app" click **Advanced** → **Go to Catalyst Bridge Intern Report (unsafe)** — this is safe because YOU created it
   - Click **Allow**
4. Check the **Execution log** at the bottom. You should see:
   ```
   ✅ Sheet found: Intern Weekly Reports — Submissions
   ✅ Drive folder found: Intern Reports — Uploaded Files
   ✅ Email quota remaining: 100
   🎉 All systems go! You can deploy.
   ```
5. If you see ❌ errors, double-check your Sheet ID and Folder ID

---

## Step 6: Deploy as a Web App

1. Click **Deploy** (blue button, top right) → **New deployment**
2. Click the **gear icon** next to "Select type" → choose **Web app**
3. Fill in the settings:
   - **Description**: "Weekly Intern Report v1"
   - **Execute as**: **Me** (your email)
   - **Who has access**: **Anyone** (this means anyone with the link can submit — the form itself has the authorized-use disclaimer)
4. Click **Deploy**
5. Google may ask you to authorize again — follow the same steps as Step 5
6. You'll see a **Web app URL** — this is your form link!
   - It looks like: `https://script.google.com/macros/s/LONG_STRING/exec`
7. **Copy this URL** — this is what you'll share with interns

---

## Step 7: Test the Live Form

1. Open your Web app URL in a browser
2. Fill out the form with test data
3. Click Submit
4. Check that:
   - ✅ The success screen appears
   - ✅ A new row appears in your Google Sheet
   - ✅ You receive a notification email
   - ✅ If you uploaded a file, it appears in your Drive folder

---

## Sharing with Interns

Once testing is complete, share the Web app URL with interns via:
- Slack message
- Email from the program lead
- Add to the Internship Kickoff materials

The URL is long, so you may want to create a short link:
1. Go to [bitly.com](https://bitly.com) (free)
2. Paste your web app URL
3. Create a short link like: `bit.ly/CatalystBridgeReport`

---

## Updating the Form Later

If you need to make changes to the form or backend:

1. Go to [script.google.com](https://script.google.com)
2. Open your **"Catalyst Bridge Intern Report"** project
3. Make your changes
4. Click **Deploy** → **Manage deployments**
5. Click the **pencil icon** on your deployment
6. Change the **Version** to **New version**
7. Click **Deploy**
8. The same URL will now serve the updated form

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "nextStep is not defined" error | Make sure the entire HTML file was pasted into Form.html — it may have been cut off. Scroll to the bottom and verify you see `</html>` |
| Permissions error on submit | Re-run testSetup and re-authorize |
| Emails not sending | Check MailApp quota: Google Workspace allows 1,500 emails/day |
| File upload fails | Verify the Drive folder ID is correct and you have edit access |
| Form loads blank | Make sure the HTML file is named exactly `Form` (not `Form.html`) |
| Sheet not updating | Verify the Sheet ID and that the sheet isn't in trash |

---

## Security & Privacy Notes

**What's built in:**
- All data transmits over HTTPS/TLS (Google enforces this automatically)
- Data is stored in your Google Workspace, governed by your org's Google policies
- File uploads go to a specific Drive folder you control
- The form includes an authorized-use-only disclaimer and legal footer
- No data is shared with third parties — it stays in your Google account

**Recommended next steps:**
- Restrict the Drive folder and Sheet to only Catalyst Bridge staff (right-click → Share)
- If you have a Catalyst Bridge privacy policy, update the footer link in the HTML
- Review submissions regularly and delete data after the program ends per your retention policy
- If you need to revoke access, go to Deploy → Manage deployments → Archive

---

## File Reference

| File | Purpose |
|------|---------|
| `index.html` | The form (rename to Form.html in Apps Script) |
| `Code.gs` | The backend logic (paste into Code.gs in Apps Script) |
| This guide | Step-by-step setup instructions |

---

**Questions?** Contact the Catalyst Bridge team or refer back to this guide anytime.
