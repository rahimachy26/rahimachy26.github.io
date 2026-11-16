# Colour by Sums: Kids Maths – how to put it on Google Play

The app is a web app. GitHub Pages hosts it for free. PWABuilder then wraps it into
an Android App Bundle (.aab), which is the file Google Play accepts.

## What's in this folder

| File | What it does |
|---|---|
| index.html | The game |
| manifest.webmanifest | The app's name, colours and icons |
| sw.js | Lets the game work offline after it has opened once |
| privacy.html | Privacy policy (Google Play needs a link to one) |
| icons/ | App icons (192, 512 and a "maskable" 512 for Android) |

## Step 1 – GitHub Pages (already done)

The game is in the `colour-by-sums` folder of your `rahimachy26.github.io`
repository. It's live at **https://rahimachy26.github.io/colour-by-sums/**
Open that link in Chrome on an Android phone and check that it works.

## Step 2 – Make the Android file with PWABuilder

1. Go to **https://www.pwabuilder.com** and paste in your GitHub Pages link.
2. Click **Package for stores**, then **Android**, then **Generate Package**.
3. In the options, set:
   - **Package ID:** something unique that you never change, for example
     `uk.co.rahimachowdhury.colourbysums`
   - **App name:** Colour by Sums: Kids Maths
   - **Signing key:** "Create new"
4. Download the zip. It contains:
   - the **.aab** file, which you upload to Google Play
   - the **signing key** (`signing.keystore`) and its passwords.
     **Keep these somewhere safe.** You need them for every update.
   - **assetlinks.json**

## Step 3 – Hide the browser bar (assetlinks.json)

Your `rahimachy26.github.io` repository already has `.well-known/assetlinks.json`
for Iqra. **Don't replace that file, or Iqra will break.** Ask Claude to add the
Colour by Sums entry from PWABuilder's assetlinks.json to it. Or add it yourself:
the file is a list `[ {...Iqra...}, {...Colour by Sums...} ]`, so add a comma after
Iqra's `}` and paste the new `{...}` block after it.

Check that https://rahimachy26.github.io/.well-known/assetlinks.json shows both apps.

## Step 4 – Google Play Console

1. Click **Create app**. Fill in: name "Colour by Sums: Kids Maths", **App** (not game) or
   **Game** (either is fine), **Free**.
2. Fill in the **App content** section:
   - **Privacy policy:** `https://rahimachy26.github.io/colour-by-sums/privacy.html`
   - **Target audience:** choose ages **5 and under** and/or **6–8**. Because
     the app is for children, Google's **Families policy** applies. The app has
     no ads and collects no data, so it already meets those rules.
   - **Ads:** No
   - **Data safety:** "No data collected" and "No data shared"
   - **Content rating:** fill in the questionnaire. It should come out as suitable for everyone.
3. **Store listing:** short description, full description, the 512 icon, a
   feature graphic (1024×500), and at least 2 phone screenshots of the game.
4. **Testing → Closed testing:** create a release and upload the **.aab**.
5. **If your developer account is a personal account created after
   13 November 2023:** at least 12 testers must stay opted in to the closed test
   for 14 days in a row before you can apply for production. Add their Gmail
   addresses as a tester list and send them the opt-in link.
6. After the 14 days, apply for **Production access**, then promote the release.

## Updating the game later

- If you change only the game (index.html), update the file in the colour-by-sums folder on GitHub. The app
  updates by itself and you don't need a new Play release. Also change
  `colour-by-sums-v1` in `sw.js` to `v2` (then `v3` and so on), so phones fetch
  the new version.
- If you change the name, icon or package settings, you need a new .aab from
  PWABuilder, made with the **same signing key**.
