# Final Draft — setup

`index.html` runs in **demo mode** until you add a Firebase config. In demo mode everything saves only in that browser, so you can try it right away (student password `demo123`, teacher: any email and password).

## Going live (about 15 minutes)

1. **Firebase project.** Go to console.firebase.google.com. Create a new project (or reuse one), then add a **Web app**. Copy the `firebaseConfig` object.
2. **Authentication.** Open Build → Authentication → Sign-in method and enable **Email/Password**. Then, under Users → Add user, create **your teacher login** (a real email and a password).
3. **Firestore.** Open Build → Firestore Database → Create database. Production mode is fine, and pick a region close to you, such as `southamerica-east1`.
4. **Rules.** Open Firestore → Rules, paste in the contents of `firestore.rules`, change `teacher@example.com` to your teacher email, and click **Publish**.
5. **Config.** At the top of `index.html`, set:
   - `firebase:` → paste your config object in place of `null`
   - `teacherEmail:` → the same teacher email
6. **Host it.** Put `index.html` on Cloudflare Pages, either as its own project or as a folder of your class site, e.g. `/writing/`. Then, in Firebase → Authentication → Settings → Authorized domains, add your Pages domain.
7. **Add your class.** Open the site, click **Teacher sign in**, then go to **Students & passwords** and paste your class list (`Name, password` per line, or just names to get made-up passwords). Use **Print login cards** to make cut-out cards for students.
8. **Create a writing task.** On the **Student work** tab, click **＋ New writing task** and open it for students.

## How it works

- **Student sign-in.** Students tap their name and type their password. Each student is a real Firebase account, and the security rules mean a student can only ever read their own writing.
- **Signing out on shared devices.** A student's sign-in lasts until the browser tab is closed, so on shared iPads or Chromebooks closing the tab signs them out.
- **Saving.** Work saves every 3 seconds while they type, and also when they switch tabs or close the page. If the internet drops, writing is kept on the device and uploads when the connection returns. If they sign in on another device, they continue where they left off.
- **Tasks.** Only one task is "open" at a time. Opening a new task doesn't delete anything, and you can still view and export every older task from the dropdown.
- **Passwords.** Passwords are stored in a teacher-only collection so you can print cards and reset them. That's a convenience trade-off. Use simple class passwords, not anything students use elsewhere.
- **Name list.** The name list is readable without signing in, so use first names (or first name + initial).
- **PDF export.** PDFs are A4 with 2.54 cm margins, 12 pt Helvetica, and double spacing. **PDF of everyone** gives one file with each student starting on a new page.
- **Settings.** In `CONFIG` you can change the font size (`bodySize`), autosave interval, or turn off spellcheck/autocorrect (`spellcheck: false`). Turning it off is handy if you want to see students' own spelling.
