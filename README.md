
Coding revival advice
/
Github repos for GitaVani and news-aggregator: Should it be public (or private currently). I am thinking from a resume/job search perspective.

4:10 PM
Good question, Nikhil. Let me think through this from a job search perspective.

Make them public. Here's the reasoning:

GitaVani — This is a shipped iOS app, which is a strong signal. A public repo lets a hiring committee or technical interviewer see your code quality, architecture decisions, and that you actually build and ship things end-to-end. For a CTO/VP Eng role, demonstrating hands-on technical fluency (especially with Swift/iOS and AI integration) differentiates you from pure-management candidates.

News Aggregator — Same logic. It shows breadth and current technical engagement.

The risk of keeping them private is that they become invisible. Your resume and LinkedIn can mention them, but a public repo turns a bullet point into verifiable evidence. Senior hiring decision-makers (and especially technical co-founders at growth-stage companies) often do click through to GitHub.

A few practical considerations:

Make sure there are no API keys, secrets, or personal data committed in the history. If there are, it's easier to create a fresh public repo with a clean history than to try to scrub an existing one.

Add a solid README to each — not just setup instructions, but a brief "why I built this" and architectural overview. For your audience (hiring managers, not open-source contributors), that narrative context matters more than contribution guidelines.

For Surfaced, I'd keep that private for now since it has potential commercial value and is still in early spike phase. But GitaVani and the news aggregator are portfolio pieces — let them do their job.

The full repo's for both the apps are attached to the project knowledge (gitavani, gitavani-site, news-agggregator). Please do a thorough evaluation of all the files there to ensure privacy but also I do not want to look stupid. Not sure what I am trying to say here, but check once and then maybe we can discuss?

4:12 PM
Let me do a thorough review of all three repos in the project knowledge.


Searched memory

















































































Okay, I've done a thorough review across all three repos. Here's my assessment, Nikhil:

GitaVani (iOS app repo) — ✅ Safe to make public
Privacy/Security: Clean. No API keys, no secrets, no credentials anywhere. The app is fully offline with bundled JSON data. No .env files, no hardcoded keys.

Things to clean up before going public:

CLAUDE.md — Contains personal context: "This app is a gift for my wife", "She's using a crappy app with colored backgrounds...", and "I have zero iOS/Swift experience." The first two are charming and fine. The third one — admitting zero iOS/Swift experience — is the one I'd remove. For a CTO-level candidate, you want the code to speak for itself. The fact that you built a polished, multi-version iOS app with 4 themes, 17 scholars' commentaries, audio, and App Store submission is more impressive if you don't call out it was your first time. Let reviewers be impressed by the quality.
docs/architecture.md — "Primary: Nikhil's wife — English-first reader learning Hindi, part of a Gita study group." This is fine and actually adds nice product context — you built something for a real user with real requirements. I'd leave it.
docs/submission_prep.md — Detailed code quality review with "MUST FIX" items. This is actually a positive — it shows you do thorough code reviews even on personal projects. Leave it.
App Store submission playbook — Great reusable documentation. Another signal of maturity. Leave it.
gitavani-site (website repo) — ✅ Safe to make public
Just static HTML: landing page, privacy policy, support page. Nothing sensitive. Clean.

news-aggregator (ClearNews) — ⚠️ Needs cleanup before going public
Privacy/Security concerns:

Hardcoded server IP — 137.184.239.51 appears in multiple deployment files (SETUP_GUIDE.md, DEPLOYMENT_PLAYBOOK.md, stream-logs.sh, docker-compose references). This is your live DigitalOcean droplet IP. Exposing it publicly makes it a target for scanning/attacks.
Hardcoded credentials — The SETUP_GUIDE.md literally contains: nikhil@signalsynthesizer.com / SignalSynthesizer@123 as plaintext login credentials. This is a hard blocker. Even if ScreenTrades is a separate project that somehow bled into this repo's deployment docs, these credentials need to be scrubbed.
Email addresses — thegitavani@gmail.com (fine, it's a support email), support@getclearnews.com (fine), but nikhil@signalsynthesizer.com in deployment docs is more personal.
CLAUDE.md — Contains "What Pisses Me Off" section. This is your development personality and it's actually great — shows you have strong engineering standards. But the phrasing is blunt. Up to you whether you want that public. A hiring manager might find it refreshing; a more corporate reviewer might not.
ScreenTrades / Signal Synthesizer content — There's significant bleed from the ScreenTrades project into the news-aggregator deployment docs (screentrades.ai references, Anthropic API keys in .env.production templates, geo-blocking configs, invite systems). This suggests ScreenTrades deployment docs may be in the same repo or the repos share deployment infrastructure. If you're making news-aggregator public, make sure ScreenTrades content is fully separated.
.env.example and .env.production.example — These are safe (they have placeholder values), but double-check that no actual .env or .env.production file is committed in git history.
"Looking stupid" concerns — the stuff that matters for perception:
GitaVani makes you look great. Zero dependencies, clean architecture, thorough docs, data pipeline, App Store submission, MIT license — this is textbook "CTO who can still build." The architecture doc, submission prep, and changelog show executive-level thinking applied to a personal project.

ClearNews also looks good as an engineering project — 41 sources, 3 clients (web/iOS/API), Docker deployment, proper caching. The main risk is the deployment docs being messy with mixed-project content.

Bottom line recommendations:

For GitaVani: Remove the "I have zero iOS/Swift experience" line from CLAUDE.md. Make public. Everything else is a strength.

For gitavani-site: Make public as-is.

For news-aggregator: Needs a scrub pass before going public — remove hardcoded IPs, remove the plaintext credentials, separate ScreenTrades content, and verify git history is clean of secrets. Either do that cleanup or keep it private. Given the effort required, keeping it private for now and focusing GitaVani as the public portfolio piece might be the pragmatic move.

Want me to help draft the specific edits for the CLAUDE.md cleanup on GitaVani?

Even if I make those changes, anyone can go and look at revision history and find that, right?

4:15 PM
Yes, exactly. Git history preserves everything. Removing a line in a new commit doesn't remove it from the old commits.

You have two options:

Option 1: Don't worry about it. Realistically, almost nobody browsing a GitHub portfolio digs through commit history. Hiring managers and technical reviewers look at the current state of the repo — the README, the code structure, maybe a few source files. The "zero iOS experience" line in an old commit of CLAUDE.md is extremely unlikely to be found. The plaintext credentials in the news-aggregator repo are a different story — that's an actual security risk, not just optics.

Option 2: Fresh repos with clean history. Create new public repos and push only the current state as a single initial commit (or a curated set of commits). You lose the commit history, but for portfolio projects that's not really a loss — nobody's evaluating your commit cadence on a personal Gita app. The code and documentation speak for themselves.

My recommendation: Option 1 for GitaVani (just edit CLAUDE.md and move on — the risk is negligible), and Option 2 for news-aggregator if you decide to make it public (because the credentials and IP addresses in history are an actual security concern, not just cosmetic). But honestly, leading with GitaVani alone as your public portfolio piece is strong enough. ClearNews can stay private.

I am assuming you cannot edit the gitavani files directly to the repo (like claude code does)?

4:16 PM
Correct — I can't push to GitHub from here. I can only create files locally in this environment.

Your options:

Claude Code — Open the GitaVani repo in Claude Code and make the edit there, then commit and push directly.
Manual edit — It's literally one line to remove in CLAUDE.md. Under the ⚠️ Reminders section, delete: - **I have zero iOS/Swift experience** — explain SwiftUI concepts as we build, don't assume knowledge.
I draft the exact edit here — You copy-paste it into the file yourself via GitHub's web editor (pencil icon on the file).
Given it's a single line deletion, option 2 is probably fastest. Takes 30 seconds in GitHub's web editor.

Please check for gitavani using public access - https://github.com/nikhilsi

4:19 PM
Let me check your public GitHub profile to see what's currently visible.


Searched the web

Here's what's publicly visible on your GitHub profile right now:

3 public repos:

resume — "Nikhil Singhal resume"
gitavani — (Swift)
gitavani-site — (HTML)
So GitaVani and gitavani-site are already public. The news-aggregator is private (not showing), which is good given the credentials and IP issues.

A couple of profile observations while we're here:

Your location says Redmond, WA — is that still accurate, or should it be updated? Small thing but hiring people do look.
Your website link points to programminginterviews.info — is that still active/relevant? If it's an old site, it might undercut the senior executive positioning. Might be better to point it to your LinkedIn or leave it blank.
No bio. A one-liner like "CTO | VP Engineering | Building at the intersection of platform engineering and AI" would add context for anyone landing on your profile.
4 followers, 0 following — not a concern, just noting it's a light GitHub presence, which is fine for someone who's been in enterprise roles.
The GitaVani repo is already doing its job as a public portfolio piece. Want me to fetch the actual repo page to check how the README renders publicly?

yes to check the readme.
yes to changing and updating github profile. Lets do that prperly. My resume, etc is already attached to the project knowledge

4:22 PM

Searched the web


Now let me check the GitaVani repo README and also pull your resume details for the profile update.


Searched the web
The GitaVani repo isn't indexed by search yet (common for newer repos), so I can't fetch it directly. But I already have the full README content from project knowledge — it looks clean and well-structured.

Now let me pull your resume details to build the profile properly.


Searched project for “Nikhil Singhal resume summary CTO VP Engineering experience companies”









Okay, good news — I can see your resume repo already has an updated README (the one starting with "CTO — VP Engineering — Builder of products, teams & organizations that ship"). That's much better than the old verbose version. Now let me look at what needs updating.

Here's what I found and my recommendations for your GitHub profile. I'll create the actual files you need:

Issues found:

Resume repo README — Already updated with the strong version. Good.
Resume repo still contains the OLD resume PDF (Nikhil-Singhal-Architect-Resume.pdf) alongside the recommendations PDF. The links in the new README point to nikhilsi.github.io/resume/ which is a GitHub Pages URL — is that actually set up?
Profile has no bio — needs one
Location says Redmond, WA — should be Seattle, WA (matches your resume)
Website link points to programminginterviews.info — outdated
No profile README (the special nikhilsi/nikhilsi repo) — this is a missed opportunity
Let me create the profile README and give you the exact settings to update:


Created 2 files, viewed a file, read a file
Two files for you:

github-profile-README.md — The content for your new nikhilsi/nikhilsi special repo. This will render directly on your GitHub profile page. It's concise, leads with your title, highlights GitaVani and ScreenTrades as recent builds, and includes career metrics. No fluff.

github-profile-update-instructions.md — Step-by-step checklist covering all 6 changes: profile settings (bio, location, website link), creating the profile README repo, pinning repos in the right order, the CLAUDE.md edit, resume repo cleanup, and removing the old programminginterviews.info link.

One thing I noticed: your resume repo README already has links to nikhilsi.github.io/resume/ — you'll want to make sure GitHub Pages is actually enabled on that repo, otherwise those PDF links will 404. Quick check: go to the resume repo → Settings → Pages and verify it's set to deploy from the main branch.

Github profile readme
Document · MD 
Github profile update instructions
Document · MD 
Wait. I am confused. this was too much nfo to process at one go. My biggest concern would be the outdated resume? or the link to t.

can you walk me through the changes one by one please?

4:24 PM
You're right, let me slow down. Let's go one at a time.

Change 1: Profile settings

Go to https://github.com/settings/profile and update three fields:

Bio → CTO | VP Engineering | Building products, teams & organizations that ship
Location → Seattle, WA (currently says Redmond)
Website → https://www.linkedin.com/in/nikhilsinghal/ (currently points to programminginterviews.info which is outdated)
That's it for now. Do those three, and tell me when you're done and we'll move to the next one.

Done. I saw this below. I think we should enable "Include private contributions on my profile"

4:27 PM
Yes, enable that. It fills in your contribution graph with green squares from your private repos (ClearNews, ScreenTrades, Surfaced work) without revealing any details about the repos themselves. A hiring manager glancing at your profile sees consistent activity instead of an empty grid. No downside.

Flip it on, then we'll move to Change 2.

Done. next

4:28 PM
Change 2: Create the profile README

This is the special repo that displays content directly on your GitHub profile page.

Go to https://github.com/new
Repository name: nikhilsi — GitHub will show a message saying "this is a special repository"
Set it to Public
Check "Add a README file"
Click Create repository
Once it's created, open the README.md and replace the default content with the text from the github-profile-README.md file I gave you. Commit it.

Let me know when done.








Claude is AI and can make mistakes. Please double-check responses.
Github profile readme · MD
Copy

# Nikhil Singhal

**CTO | VP Engineering | Head of Product**

Technology executive who builds products, teams, and organizations that ship. 25+ years across PE-backed startups and Fortune 500s including Expedia, T-Mobile, Microsoft, and AT&T.

### Recent work

- **[GitaVani](https://github.com/nikhilsi/gitavani)** — iOS Bhagavad Gita reader app. Swift/SwiftUI, 701 verses, 17 scholars, 4 themes, Sanskrit audio. Built end-to-end and submitted to App Store. [[website](https://gitavani.app)]
- **[ScreenTrades.ai](https://screentrades.ai)** — AI-powered trading analysis platform. React, FastAPI, Claude AI, 20+ real-time data APIs. Shipped 20 iterations in 6 months.

### Career highlights

- **$45M annual savings** — Led VRBO integration into Expedia's lodging platform
- **300% ARR growth** — Scaled Imperative from $1M to $4M ARR as CTO & Head of Product
- **400% operational efficiency** — Built AI-powered travel platform at The Tour Guy
- **200+ engineers led** across Fortune 500 engagements at Hitachi Consulting
- **114 LinkedIn recommendations** from peers, reports, and executives [[PDF](https://github.com/nikhilsi/resume/blob/main/Nikhil-Singhal-LinkedIn-114-Recommendations.pdf)]

### Connect

[LinkedIn](https://www.linkedin.com/in/nikhilsinghal/) · [Resume](https://github.com/nikhilsi/resume) · nikhilsinghal@hotmail.com · Seattle, WA







