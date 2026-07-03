# Connecting Google Drive backup

Your app can back up its data (rates, transactions, customers, banks) to a private
file in your own Google Drive. Because this is a self-hosted app rather than an
Anthropic or Google product, Google requires you to register it once before it's
allowed to ask for Drive access. This only needs doing once.

## 1. Create a Google Cloud project
1. Go to https://console.cloud.google.com/
2. Top left, click the project dropdown → **New Project**. Give it any name (e.g. "MMK THB Tracker") → Create.

## 2. Enable the Drive API
1. In the search bar, search **"Google Drive API"** → open it → **Enable**.

## 3. Configure the consent screen
1. Left menu → **APIs & Services → OAuth consent screen**.
2. User type: **External** → Create.
3. Fill in app name (e.g. "MMK THB Tracker"), your email for support and developer contact → Save and continue through the remaining steps (you can skip scopes/test users for now, or add your own Google account as a test user).
4. Publishing status can stay in **Testing** — that's fine for personal use, it just means only accounts you add as test users can sign in. Add your own Gmail account under **Test users**.

## 4. Create the OAuth Client ID
1. Left menu → **APIs & Services → Credentials → Create Credentials → OAuth client ID**.
2. Application type: **Web application**.
3. Under **Authorized JavaScript origins**, add the exact address where you hosted the app, e.g.:
   `https://yourname.github.io`
   (just the domain, no trailing path or slash)
4. Click **Create**. Copy the **Client ID** shown (looks like `xxxxxxxxxx.apps.googleusercontent.com`).

## 5. Paste it into the app
1. Open your app → tap the gear icon (top right) → **Settings**.
2. Paste the Client ID into the **Google OAuth Client ID** field.
3. Tap **Connect Google Drive**, sign in with the Google account you added as a test user, and approve access.

From then on, the app syncs automatically in the background a couple of seconds after
any change. On a new phone, install the app, connect the same Google account, and tap
**Restore from Drive** to pull your data back down.

## Notes
- The app only requests the `drive.file` scope, meaning it can only see and edit files it creates itself — not your other Drive files.
- If you ever republish the app at a different address, you'll need to add that address to Authorized JavaScript origins too (step 3).
- If Google shows an "unverified app" warning during sign-in, that's expected for apps in Testing mode — click **Advanced → Go to (app name)** to continue. This is safe since it's your own project.
