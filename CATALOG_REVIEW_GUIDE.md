# Catalog App Review

What we check before an app goes in the Cloud in a Bottle catalog. For each app,
confirm the points below; where it falls short, fix it, fix the score, or leave
it out.

## What a review checks

1. **The score is accurate.** Each app has an integration score from 1 to 5
   (see below) for how well it fits the platform. Check the number against how
   the app actually behaves — don't just trust it.

2. **Sign-in works as described.** Try it yourself:
   - The **owner** is signed in automatically. Barring an unusual circumstance,
     the owner should never have to make an account or enter a password to use an
     OpenHost app — no login screen, no hunting for a password.
   - **Everyone else** is handled right: sent to the login page for a private
     app, or shown shared/public content without being signed in as the owner.
   - **No onboarding flow.** Wherever the platform allows it, an app should have
     no signup or first-boot setup — we handle auth for you, so there's no
     account to create. Configuration should be pre-determined and baked into the
     app or wrapper repo based on what makes sense for a bottle user, rather than
     asking a bunch of questions on first boot. Ideally apps come up and are
     immediately usable.

3. **The app works — all of it.** It does the thing it's for — not just "the
   container starts." Add the feed, record the video, play the game. If the main
   feature is broken, it's not ready, however clean the rest is. No part of the
   app should be broken by the integration into Cloud in a Bottle. Things like
   share-link generation should be tested and adapted to work properly within the
   platform. If something genuinely can't work, make that
   clear in-product rather than leaving it non-obviously broken.

4. **Data survives a restart.** Anything the user creates is kept when the app is
   redeployed — not lost with the container.

5. **The README explains the app.** A reader should learn what it is, who it's
   for, and how to start; a wrapper should link the project it packages. A small
   wrapper's README should focus on Cloud in a Bottle; a larger project should
   at least mention and link it (a separate Cloud in a Bottle page is fine).

6. **The repo has a LICENSE.** A wrapper keeps a license compatible with what it
   packages (a GPL/AGPL app stays GPL/AGPL); original code can use a permissive
   one.

7. **Resource limits are accurate.** Memory and CPU limits should match what the
   app really uses — measured, not guessed. Some apps need more memory to build
   than to run; when so, give the build a higher limit of its own.

8. **The app is reasonably secure.** No obvious security holes — for example, it
   must not leak passwords, keys, or tokens into its logs. It also shouldn't
   request any permissions or privileges that aren't necessary for the purpose of
   the app.

## The integration score (1–5)

The score is about how well the app fits the platform — mainly single sign-on
and how it treats the owner and guests — not how good the underlying app is. A
great project with a clunky fit scores low; a simple app that fits perfectly
scores high. Unscored apps leave the field blank.

| Score | Criteria |
|-------|----------|
| **1 — Deployable only** | Starts and loads, but the fit is rough — manual setup, broken conventions, or a worse experience than running it on its own. |
| **2 — Minimal** | Works and saves data, but no single sign-on — the owner logs in through the app's own login form. |
| **3 — Solid, with rough edges** | The owner is signed in automatically, but with rough edges — e.g. other people need their own account in the app, or sign-in only works from some links. |
| **4 — Near-native** | The owner is signed in automatically and conventions are followed, but one thing is missing or rough — e.g. other users still need app accounts, or shared links aren't public. |
| **5 — Fully native** | The owner is signed in automatically, guests and shared links just work, and the app is genuinely built into the platform (real sign-in integration, sharing between instances) — nothing feels bolted on. |

**Hard cap:** if the app leaves a usable password or secret on disk where other
apps could read it, it can't score above **3**.

**Don't penalize what doesn't apply.** A public, account-free service has no
guests to sign in and no secrets to leak — it can still score 5. Account systems
that are external to the app or used for encryption are fine.

Each scored app also gets a one-sentence, plain-language explanation of its
score.
