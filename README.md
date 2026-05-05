# FamilySync PWA

A family calendar Progressive Web App with Google Calendar integration.

## Family members
- **Rudi** — Owner/Editor (can create & edit events)
- **Tesha** — Owner/Editor (can create & edit events)
- **Cassie** — Participant/Viewer (receives reminders, read-only)
- **Tyler** — Participant/Viewer (receives reminders, read-only)

## Features
- Month, Week, Day calendar views
- Color-coded events per task
- Multiple family members per event
- Location field
- Recurring events (daily / weekly / monthly)
- Settable reminders per event
- Google Calendar sync (events appear in each member's Google Calendar)
- Works offline (PWA — installable on iPhone home screen)
- Demo mode (no Google account needed to try)

---

## Quick start — Demo mode
1. Open the app URL in any browser
2. Tap **"Try demo mode"** — no sign-in needed
3. Sample events for your family are preloaded

---

## Full setup — Google Calendar integration

### Step 1: Google Cloud Console
1. Go to https://console.cloud.google.com
2. Create a new project (e.g. "FamilySync")
3. Go to **APIs & Services → Enable APIs**
4. Enable **Google Calendar API**

### Step 2: OAuth consent screen
1. Go to **APIs & Services → OAuth consent screen**
2. Choose **External**, click Create
3. Fill in:
   - App name: `FamilySync`
   - User support email: your email
   - Developer contact: your email
4. Click **Save and Continue** through all steps
5. Under **Test users**, add all family members' Google email addresses

### Step 3: Create credentials
1. Go to **APIs & Services → Credentials**
2. Click **Create Credentials → OAuth Client ID**
3. Choose **Web application**
4. Name: `FamilySync Web`
5. Under **Authorized JavaScript origins**, add:
   - `http://localhost` (for local testing)
   - `https://YOURUSERNAME.github.io` (your GitHub Pages URL)
6. Click **Create**
7. Copy the **Client ID** (looks like `123456789.apps.googleusercontent.com`)

### Step 4: Create API Key
1. Go to **APIs & Services → Credentials**
2. Click **Create Credentials → API Key**
3. Copy the API key
4. Click **Edit API key** → Under **API restrictions**, select **Google Calendar API**

### Step 5: Update the app
Open `index.html` and find these two lines near the top of the `<script>` section:

```js
GOOGLE_CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com',
GCAL_API_KEY: 'YOUR_GOOGLE_API_KEY',
```

Replace with your actual values.

---

## Deploy to GitHub Pages

```bash
# 1. Create a new GitHub repository named "familysync"
# 2. Clone it locally
git clone https://github.com/YOURUSERNAME/familysync.git
cd familysync

# 3. Copy these files into the repo
cp /path/to/familysync/* .

# 4. Push
git add .
git commit -m "Initial FamilySync PWA"
git push origin main

# 5. Enable GitHub Pages:
#    Repo → Settings → Pages → Source: Deploy from branch → main → / (root)
```

Your app will be live at: `https://YOURUSERNAME.github.io/familysync`

---

## Install on iPhone (Add to Home Screen)
1. Open your GitHub Pages URL in Safari on iPhone
2. Tap the Share button (box with arrow)
3. Scroll down and tap **"Add to Home Screen"**
4. Tap **Add**

The app icon appears on your home screen and opens without browser chrome, just like a native app.

---

## How Google Calendar sync works
- When an owner creates an event, it is pushed to a **"FamilySync"** calendar in Google Calendar
- All family members who have connected their Google account will see events in their Google Calendar
- Events created directly in Google Calendar also appear in FamilySync (fetched on open)
- Reminders set in FamilySync are mirrored as Google Calendar popup notifications

## Role enforcement
- The FAB (+) button is hidden for Cassie and Tyler (viewer role)
- Edit/Delete buttons only appear for Rudi and Tesha
- Role is determined by which family member account is signed in

---

## Files
```
familysync/
├── index.html      ← Main PWA app (everything in one file)
├── manifest.json   ← PWA metadata (icons, name, theme color)
├── sw.js           ← Service worker (offline support)
└── icons/          ← App icons (add 192x192 and 512x512 PNGs)
    ├── icon-192.png
    └── icon-512.png
```

## App icons
You need two PNG icons. Create them at:
- 192×192 pixels → save as `icons/icon-192.png`
- 512×512 pixels → save as `icons/icon-512.png`

Use any image editor or a free tool like https://favicon.io to generate them from text ("FS" on a green background works well).
