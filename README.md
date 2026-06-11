# Grunter beta revive

This folder is the small test version of Grunter.

It is still a simple static web app:

- `index.html` is the app.
- `supabase-setup.sql` recreates the Supabase database, storage bucket, permissions, and real-time setup.

## Recommended free setup

Use:

- GitHub repository for the code.
- GitHub Pages for the live website.
- Supabase Free for database, audio storage, and real-time updates.

This is the closest match to the old app and needs the least rewriting.

## Current Supabase backend

This revive package is now connected to:

```text
Project: grunter-beta
Project URL: https://ltdpnvruowaixlrvrpzv.supabase.co
Browser key type: publishable key
```

Do not put any Supabase `sb_secret_...` key into `index.html`.

## Current test status

Checked locally:

- Database tables were created.
- The `grunts` storage bucket was created.
- The app reads from Supabase.
- A tiny test audio file was uploaded successfully.
- A test grunt appears in the feed.
- A test comment and reaction were inserted successfully.
- Real-time refresh worked when a comment was added outside the app.
- Public audio URL returned `audio/wav`.

There is currently one visible test item in the feed called `Codex Test Grunt`.

## Step 1: Create a new Supabase project

1. Go to `https://supabase.com`.
2. Sign in or create a free account.
3. Click **New project**.
4. Choose your organization.
5. Project name: `grunter-beta`.
6. Database password: create one and keep it somewhere safe.
7. Region: choose the closest region to you.
8. Click **Create new project**.

How you know it worked:

- Supabase opens a project dashboard.
- You can see a left menu with **Table Editor**, **SQL Editor**, **Storage**, and **Project Settings**.

If it fails:

- Try a shorter project name.
- Check that you are on the Free plan.
- Do not enter payment details unless Supabase specifically requires it for your account.

## Step 2: Run the database setup script

1. In Supabase, open your project.
2. Click **SQL Editor** in the left menu.
3. Click **New query**.
4. Open `supabase-setup.sql` from this folder.
5. Copy the whole file.
6. Paste it into the Supabase SQL Editor.
7. Click **Run**.

How you know it worked:

- Supabase shows **Success. No rows returned** or similar.
- In **Table Editor**, you should see:
  - `users`
  - `grunts`
  - `comments`
  - `reactions`
  - `battles`
  - `battle_votes`
- In **Storage**, you should see a bucket called `grunts`.

If it fails:

- Copy the exact red error message.
- Paste it back into Codex.
- Do not keep clicking random settings.

## Step 3: Copy your Supabase app keys

1. In Supabase, click **Project Settings**.
2. Click **API**.
3. Copy the **Project URL**.
4. Copy the **publishable** key.
5. Do not use any secret key in `index.html`.

How you know it worked:

- The URL should look like `https://something.supabase.co`.
- The key should say publishable or look safe for browser use.

## Step 4: Paste the keys into the app

Open `index.html` and find:

```js
const SUPABASE_URL = "__PASTE_SUPABASE_PROJECT_URL_HERE__";
const SUPABASE_PUBLISHABLE_KEY = "__PASTE_SUPABASE_PUBLISHABLE_KEY_HERE__";
```

Replace those two values with your new Supabase values.

How you know it worked:

- The app will stop using local-only demo mode.
- It will connect to the new shared Supabase project.

If it fails:

- Make sure you used the Project URL, not the website URL.
- Make sure you used the publishable key, not a secret key.
- Make sure both values stay inside quotation marks.

## Step 5: Create a GitHub repository

Because Git is not currently installed on this computer, the easiest first upload is through the GitHub website.

1. Go to `https://github.com`.
2. Sign in or create a free account.
3. Click **+** in the top-right.
4. Click **New repository**.
5. Repository name: `grunter`.
6. Choose **Private** if you want only you to see the code.
7. Click **Create repository**.
8. Click **uploading an existing file**.
9. Upload:
   - `index.html`
   - `supabase-setup.sql`
   - `README.md`
10. Click **Commit changes**.

How you know it worked:

- You can see the three files listed in the GitHub repository.

## Step 6: Turn on GitHub Pages

If the repository is public:

1. In GitHub, open the repository.
2. Click **Settings**.
3. Click **Pages**.
4. Under **Build and deployment**, choose:
   - Source: **Deploy from a branch**
   - Branch: `main`
   - Folder: `/root`
5. Click **Save**.

How you know it worked:

- GitHub shows a Pages link after a minute or two.
- The link usually looks like `https://yourname.github.io/grunter/`.

If the repository is private:

- GitHub Pages may require a paid GitHub plan for private repositories.
- Cheapest option: make the repository public but avoid putting anything secret in it.
- The Supabase publishable key is okay to be public.
- The Supabase secret key must never go in the app.

## Step 7: Phone test

1. Open the GitHub Pages link on your phone.
2. Enter a name and emoji when asked.
3. Hold the record button.
4. Allow microphone access.
5. Release to upload.
6. Check that the new grunt appears in the feed.
7. Open the same link on another phone and check that the feed updates.

How you know it worked:

- Audio uploads.
- Audio plays back.
- Comments and reactions appear.
- A second phone sees changes without manually refreshing.

If it fails:

- If mic access fails, make sure the app is opened with `https://`, not a plain file.
- If upload fails, check the Supabase URL/key and the `grunts` bucket.
- If real-time does not update, refresh once and tell Codex what happened.

## Phone home screen shortcut

On iPhone:

1. Open the app link in Safari.
2. Tap the share button.
3. Tap **Add to Home Screen**.
4. Tap **Add**.

On Android Chrome:

1. Open the app link in Chrome.
2. Tap the three dots menu.
3. Tap **Add to Home screen** or **Install app**.
4. Tap **Add**.
