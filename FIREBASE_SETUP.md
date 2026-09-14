# Whisper Court: Firebase setup

The game is still hosted as static files on GitHub Pages, but Firebase Realtime Database carries multiplayer traffic between networks.

1. Create a Firebase project and register a Web app.
2. In **Authentication**, enable the **Anonymous** sign-in provider.
3. Create a **Realtime Database**.
4. Open its **Rules** tab, paste the complete contents of `firebase-rules.json`, and publish the rules.
5. Copy the Web app configuration values into the `FIREBASE_CONFIG` object near the top of `index.html`.
6. Put `index.html` in the root of the GitHub Pages repository and publish it. Keep `firebase-rules.json` in the repository for version control; the browser does not load it.

Both the host and guests must use the deployed HTTPS page. The Firebase project configuration embedded in a web page is public by design; access control comes from Authentication and the database rules.

## Required Realtime Database structure

The page creates this automatically:

- `rooms/{code}/meta`: public room metadata for signed-in players
- `rooms/{code}/hostState`: full authoritative state, readable only by the host
- `rooms/{code}/views/{uid}`: one private filtered view per player
- `rooms/{code}/commands`: authenticated guest actions consumed by the host
- `rooms/{code}/mail/{uid}`: private action prompts and reveals
- `rooms/{code}/presence/{uid}`: connection presence

Do not replace the supplied rules with Firebase's public test-mode rules. Test mode would expose hidden cards.
