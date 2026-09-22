TMI CASEWORK HUB — SETUP GUIDE
================================

WHAT'S IN THIS FOLDER
----------------------
index.html          The app itself — this is the only file you actually need
manifest.json        Used only if you ever host it (see optional section below)
service-worker.js    Used only if you ever host it (see optional section below)
icons/                App icon, built from your TMI monogram (used if hosted)

For everyday use on your phone, you only need index.html.


HOW TO INSTALL IT ON YOUR ANDROID PHONE — NO HOSTING NEEDED
----------------------------------------------------------------
  1. Copy index.html onto your phone (e.g. into your Downloads folder, or
     a folder you make called "TMI"), via USB, Drive, WhatsApp-to-self,
     or however you normally get files onto your phone. Do this ONCE —
     don't keep re-sending it to yourself, see the warning below.

  2. Open your phone's Files app, find that exact index.html, and tap it
     to open it in Chrome.

  3. In Chrome, tap the vertical-dots menu (top right) → "Add to Home
     screen" → confirm. You'll now have a TMI icon on your home screen
     that opens straight into the Hub, like any other app.

That's it — no computer, no account, no Netlify, no GitHub, nothing to
sign up for. Everything runs on your phone.

THE ONE THING THAT ACTUALLY MATTERS FOR YOUR DATA TO STICK:
Always open the Hub the same way — via that home-screen icon, or by
opening that same saved file from your Files app. Don't re-open it by
tapping a fresh WhatsApp attachment, a new email attachment, or a new
Drive "open with Chrome" link each time — depending on the app, that
can hand Chrome a new temporary copy of the file each time, which looks
empty because, as far as the browser is concerned, it IS a different
file. Save it once to a real folder on your phone, and always launch it
from there (or from the home-screen icon you made in step 3).

If you ever need to move to a new phone: use the "Export Full Case
Archive (.zip)" button in Settings first, copy the new index.html and
that .zip to the new phone, install as above, then use "Restore from
backup" in Settings to load the .zip's data.json back in.


BACKING UP YOUR DATA
------------------------
In Settings:
  - "Export Full Case Archive (.zip)" — everything: all case records
    AND every uploaded document/photo, organised into folders by case.
    This is the one to use regularly.
  - "Export Records Only (.json)" — faster, records only, no files.

Keep a copy of that zip somewhere off the phone occasionally (email it
to yourself, save it to Drive manually, copy it to a computer) — that's
your real safety net if the phone is ever lost, damaged, or reset.


OPTIONAL, LATER: HOSTING IT AT A WEB ADDRESS
-------------------------------------------------
You don't need this. Skip it unless you specifically want either of
these two extras:
  - True offline app-shell caching via a service worker
  - The optional Google Drive connection (see below) — Google's sign-in
    simply refuses to work from a local file, that's a Google rule, not
    something this app controls

If you ever do want either of those, the only extra step is putting
this folder somewhere with a real https:// address instead of opening
it as a local file — for example a free static host like Netlify Drop
or GitHub Pages. Nothing else changes; your data still lives only on
your own phone either way. This is entirely optional and the app is
fully usable without it.


OPTIONAL, LATER: CONNECTING GOOGLE DRIVE
---------------------------------------------
Only relevant if you've hosted the Hub as above. It lets the Hub
automatically create a Drive folder for every case (with sub-folders by
document type) and push copies of uploaded documents there. The Hub
never gets access to your existing Drive files — only files/folders it
creates itself.

Steps, once hosted:
  1. https://console.cloud.google.com/ -> create a new project.
  2. APIs & Services -> Library -> search "Google Drive API" -> Enable.
  3. APIs & Services -> OAuth consent screen -> "External" -> fill in an
     app name and your email -> save through the defaults. Leave it in
     "Testing" mode and add your own Google account under "Test users".
  4. APIs & Services -> Credentials -> + Create Credentials -> OAuth
     client ID -> Application type: "Web application".
  5. Under "Authorized JavaScript origins", add the exact https address
     you're hosting the Hub at (no trailing slash).
  6. Click Create, copy the Client ID (ends in .apps.googleusercontent.com).
  7. Come back and ask for the Drive "Connect" button to be switched
     back on in Settings — it's already built into the code, just kept
     out of your way until you actually have a hosted address to use it
     with.


A HONEST NOTE ON SECURITY
----------------------------
This Hub has no login screen — whoever has your phone unlocked can open
it. You said your phone's own security is enough for now, which is a
reasonable call for a working tool like this. If you ever want to lock
the app itself with its own PIN, that's a further step we can add later.


WHAT WAS FIXED IN THIS VERSION
----------------------------------
- Dashboard now shows Total Cases, Total Clients, Open Cases and
  Documents Stored — so a brand-new case shows up immediately, instead
  of only appearing once its status is moved to "Active".
- Logging a communication can now automatically create a follow-up
  task with a due date, instead of just noting a date nobody chased.
- Added a "Full Case Archive" export that zips up the case data
  together with every uploaded document/photo, organised by case — the
  previous backup only exported the data, not the actual files.
- Added the option to install as a home-screen app directly from the
  downloaded file (see instructions above) — no hosting required for
  this part.

WHAT'S NEW IN THIS UPDATE (built on top of the above, nothing removed)
------------------------------------------------------------------------
- Individual Delete added: clients, cases, enquiries, tasks and
  communications each have their own Delete button (with a confirm
  prompt). Deleting a case cascades to its tasks, communications,
  correspondence and documents (including stored files) — you get a
  clear warning first. Deleting a client is blocked while they still
  have cases linked, so a matter can't be silently orphaned. Deleting
  an already-converted enquiry only removes the enquiry record; the
  case it became stays untouched.
- New Case can now create the client inline: the Client dropdown has
  a "+ Create new client" option that reveals name/phone/email fields
  right there, instead of forcing you to leave and create the client
  first.
- The "Drafts" tab is now labelled "Correspondence" and its
  description makes clear you can type any letter, complaint,
  statement, chronology, case note, research note — or a blank
  document to type freely — directly in the app. This isn't new
  functionality (it already worked) but it was easy to miss; nothing
  here depends on uploading a file.
- New: TMI Operating Manual (T01–T16). A dedicated section (reachable
  from the side menu, and linked from every case) holding sixteen
  fixed, standalone procedure slots. Each has a title, a full text
  body you type or paste in (autosaves), and an optional attached
  reference file. Each procedure is independently printable and
  exportable to Word, and works fully offline — it isn't tied to any
  one case.
- New: Generate Full Case Report, available from every case. Tick
  which chronology events, final correspondence, documents,
  communications and tasks to include, then it assembles a 15-section
  report (summary, client & matter details, background, chronology,
  assessment/issues, research, actions taken, correspondence,
  communications, documents, tasks, outstanding matters, outcome, next
  steps, supporting documents index) as an editable preview you can
  correct before exporting to PDF (print) or Word. This is the
  single-file handover pack for a matter; the Full Case Archive export
  in Settings remains the way to hand over the underlying files
  themselves alongside it.
- Service worker cache version bumped so phones/browsers pick up this
  update instead of serving the old cached shell.

A NOTE ON INSTALLABILITY (Android "Install app" / "Add to Home screen")
----------------------------------------------------------------------
This package's manifest.json and service-worker.js already meet
Chrome's technical installability requirements (icons at the required
sizes, start_url/scope, standalone display, a registered service
worker). If Chrome's menu still doesn't offer "Install app" once this
is hosted, the most common causes are: (1) GitHub Pages not actually
enabled/deployed for the repo yet — check Settings → Pages shows a
published URL with a green check; (2) the manifest or an icon 404ing —
open https://<your-pages-url>/manifest.json directly in the browser
and confirm it loads as JSON, not a 404 page; (3) viewing the app via
a shared link (WhatsApp/email preview) instead of the real hosted
address, which some browsers open in a stripped-down viewer that never
evaluates installability at all. Always test using the exact
https://…github.io/… address directly in Chrome.
