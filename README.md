# Tom & Ben Skate!

Trick, goal and run tracker for Tom and Ben. Runs on GitHub Pages, stores data in Firebase, and needs a login to see or change anything.

Files:

- `index.html` – the app
- `config.js` – your Firebase settings
- `icon.png` – home screen icon
- `firestore.rules` – database security rules (copy into Firebase)
- `skate-log-backup.json` – the data from the Claude version, ready to import

Setup takes about 15 minutes. Everything below is free.

## 1. Create the Firebase project

1. Go to https://console.firebase.google.com and sign in with a Google account.
2. Click **Create a project**, name it `skate-log`, and turn off Google Analytics (not needed).
3. On the project home page click the **</>** (Web) icon to add a web app. Name it `Tom & Ben Skate!`. Leave "Firebase Hosting" unticked.
4. Firebase shows a block of code containing `const firebaseConfig = { ... }`. Copy just that `{ ... }` object.
5. Put it in `config.js` (already done for this repository).

## 2. Turn on the login

1. In the Firebase console's left menu, open **Security → Authentication** and click **Get started** if it asks.
2. Under **Sign-in method**, enable **Email/Password** (leave "Email link" off).
3. Go to the **Users** tab → **Add user**. Enter the email and password the family will use to sign in.

## 3. Turn on the database

1. In the left menu, open **Databases & Storage → Firestore** and click **Create database**. If it asks for an edition, choose **Standard**.
2. Pick a location close to you (for Australia, `australia-southeast1` is Sydney or `australia-southeast2` is Melbourne) and start in **production mode**.
3. Open the **Rules** tab, delete what's there, and paste in the contents of `firestore.rules`.
4. Change `family-login@example.com` to the email you created in step 2.3, then click **Publish**.

Only that login can read or write the data. To let a second login in (for example one for each of the boys), add its email to the list: `['one@example.com', 'two@example.com']`.

## 4. Put it on GitHub Pages

1. Sign in at https://github.com and create a **new repository** called `skate-log`. It can be public. The Firebase settings in `index.html` are safe to publish, because the rules and the login protect the data.
2. In the new repository click **Add file → Upload files** and drag in `index.html`, `icon.png` and `README.md`. Click **Commit changes**. (Leave `skate-log-backup.json` out of the repository, since it contains the boys' photos.)
3. Go to **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Click **Save**.
4. After a minute the page shows your address, something like `https://yourname.github.io/skate-log/`.

## 5. Allow the login on that address

1. Back in Firebase: **Security → Authentication → Settings → Authorized domains → Add domain**.
2. Add `yourname.github.io` (your GitHub username, without the `/skate-log` part).

## 6. Sign in and bring your data across

1. Open your GitHub Pages address and sign in with the family login.
2. Tap the highlighted skater at the top, then **Import backup**, and choose `skate-log-backup.json`.
3. Tom and Ben's tricks, runs, locations, names and photos appear.

## 7. Add it to the iPhone home screen

Open the address in Safari, tap **Share → Add to Home Screen**. It opens full screen with its own icon and stays signed in.

## Everyday notes

- The app keeps working without signal at the skatepark. Changes sync when the phone is back online.
- **Export backup** (tap the highlighted skater) saves everything to a file. Do this now and then.
- To change the app later, ask Claude: changes are pushed to this repository and GitHub Pages updates within a minute or two. Leave `config.js` as it is.
