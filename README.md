<div align="center">

<picture><source media="(prefers-color-scheme: dark)" srcset="https://wickrunai.com/brand/logo-dark.svg"><img src="https://wickrunai.com/brand/logo.svg" width="96" alt="wickrunAI"></picture>

# wickrunAI · 灯芯AI

**Every AI model you own, in one app — and when one fails, the next one takes over mid-task.**

Open or closed, paid or free. Bring your own keys; cloud sync is optional, and sharing never transfers your credentials.

[![Version](https://img.shields.io/badge/version-4.18.1-1f6feb)](https://github.com/lifishard/wickrunAI-releases/releases)
[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-lightgrey.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux%20%7C%20Android-lightgrey)](https://github.com/lifishard/wickrunAI-releases/releases/latest)

[Download](https://wickrunai.com/download) · [Docs](https://github.com/lifishard/wickrunAI/blob/main/docs/README.md) · [Configuration](https://github.com/lifishard/wickrunAI/blob/main/docs/CONFIGURATION.md) · [Security](https://github.com/lifishard/wickrunAI/blob/main/SECURITY.md)

**English** · [简体中文](README.zh-CN.md)

</div>

<!-- releases-readme:installer -->

Official installers for wickrunAI. In-app updates and [wickrunai.com/download](https://wickrunai.com/download) read from this repository. **[Download the latest version →](https://github.com/lifishard/wickrunAI-releases/releases/latest)**

| System | Which file |
| --- | --- |
| Windows | `…-win-x64-setup.exe` (installer, updates automatically); no install: `…-win-x64-portable.exe` |
| macOS | Apple silicon: `…-mac-arm64.dmg`; Intel: `…-mac-x64.dmg` |
| Linux | `…-linux-x64.AppImage` (updates automatically) or `…-linux-x64.deb` |
| Android | `…-android-preview.apk` (preview; before upgrading from 3.x, read the backup note in the release notes) |

The `.yml` and `.blockmap` files are for automatic updates. Installers are not code-signed yet, so Windows and macOS warn about an unknown publisher; download only from here or wickrunai.com.

<!-- /releases-readme:installer -->

---

## 4.18.0 — A focused shared conversation; a theme / font size / language capsule; a collapsible sidebar header; whole Claude Code sessions

A shared conversation now shows only the thread and one composer, with discussion, access and history opened on demand; the item list collapses. The same quick capsule for theme, font size and language sits in chat, the shared space and the Agent team. The sidebar header folds away to show more conversations.

- **Focused conversation.** The shared conversation page reads like a messenger: title row, thread, one composer; extras open on demand.
- **Quick capsule.** Light / dark, A− / A+ font size, 简 / 繁 / EN; the full options stay in Settings.
- **Sidebar header ⌃.** Folds the project picker, workspace switch, Butler card and navigation; remembered in Settings.
- **Copy to my workspace.** A shared conversation becomes a plain conversation in "Recent", with an "Open" button in the notice; no extra project is created.
- **Claude Code sessions.** The session page is a virtualized list; the import now scrolls through it screen by screen and extends its deadline while reading.

See the [4.18.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.18.0.md).

## 4.17.0 — Check roles before saving an import; the composer's model picker in the shared thread; an action menu on shared items

Pages without role markers, such as Codex tasks, came in with some turns reversed; an import whose roles were inferred now opens a review panel first. The shared thread's "send as" is no longer a dropdown with hundreds of entries but the same picker as the composer. Every shared item has a ⋯ menu.

- **Roles are checked before saving.** An import whose roles were inferred from the order opens "Check the roles, then save": each turn can be set to user / assistant, "Swap all" flips them, and nothing is saved until confirmed; roles cannot change once saved.
- **The composer's picker.** "Chat, no AI" or "Let a model reply"; the latter uses the same credential → model picker as the composer (searchable, chat models only by default), including the official route once it is registered.
- **Actions on shared items.** Copy to my workspace, copy into a project…, save as file (Markdown or wickrunAI JSON), access, delete (owner, with confirmation).
- **Claude Code session pages.** The diagnosis now names the address, the whole page's text size, iframe count and the first few words; after sign-in the page gets 90 seconds; same-origin iframes are read too. Real error text is still needed to adapt to the page.

See the [4.17.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.17.0.md).

## 4.16.0 — Claude, ChatGPT and Codex links go into the shared space; private pages ask you to sign in

Paste a Claude or ChatGPT / Codex link into **Groups & sharing → Open sharing link** and the conversation is read back and saved as a shared conversation in the current space, ready for comments, annotations and AI replies. Links that are not public pages, such as a Claude Code session (`claude.ai/code/session_…`), open a sign-in window on the desktop once; the sign-in is kept for later links.

- **Shared space accepts share links.** `claude.ai/share/…`, `chatgpt.com/share/…`, `chatgpt.com/s/…` (conversation and Codex task short links) and `claude.ai/code/session_…`; the composer accepts the same set.
- **Sign in once for private pages.** When a page redirects to a login, the desktop shows the import window so you can sign in; the import then returns to the link and reads it. The web and Android lines say plainly that such links need the desktop.
- **A diagnosis instead of a bare timeout.** When a page loads but no message block is recognised, the error names the page and what it did find, so the structure can be reported and supported.
- Not verified against live pages yet: Codex task share pages and Claude Code session pages (this environment cannot reach them); please report what the error says.

See the [4.16.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.16.0.md).

## 4.15.0 — Instant updates while the app is open; one document editor with tables, charts and annotations

Shared items and cloud sync now update the moment something changes, and every document surface uses the same editor.

- **Live updates.** The server pushes "something changed" over a server-sent event channel; shared conversations, comments, hand-offs and boards refresh at once, and other devices sync right away instead of up to a minute later. Polling stays only as a 30-second fallback.
- **One editor.** Markdown artifacts, shared text files and project docs share a block editor: tables, task lists, images, code and echarts charts (a small JSON block the model can read and write). The composer still recognises Markdown as before.
- **Annotate for the model.** Select text, write what should change, and send all annotations to the model in one request; in shared files an annotation becomes a comment anchored to the text.
- **Co-editing without losing work.** When someone else saves a shared text file while you are editing, their blocks merge into your draft; only the same block changed by both is marked as a conflict. Merging happens on your device before the end-to-end encrypted upload.

See the [4.15.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.15.0.md).

## 4.14.0 — Open Claude and ChatGPT / Codex share links; fewer dead ends in Agent teams

Paste a share link from Claude or ChatGPT (conversation or Codex task) into the composer and it opens as a local conversation you can continue with your own model. Agent teams lose three places where a first-time user used to get stuck.

- **Share links open as conversations.** `claude.ai/share/…`, `chatgpt.com/share/…` and `chatgpt.com/s/…` are read back with their user and assistant turns, titled after the share, with the original link kept at the top. The desktop reads the page in a hidden browser window so it passes the sites' bot checks; the web and Android lines ask the server and say so when the site refuses a server. This release has not yet been verified against real pages; please report what fails.
- **Acceptance is optional.** A delivery task saved without "what does good look like" gets a plain default and is still accepted by you.
- **An assigned owner works with quick setup.** The owner becomes the executor; only the discussion or review partner is added.
- **Running saves the version.** A flow without a saved version runs from its draft; the designer saves a new version when the draft moved on.

See the [4.14.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.14.0.md).

## 4.13.0 — Long tasks keep going; bookkeeping stops costing rounds

A task that writes a quiz page from four textbook chapters used to be cut off after 60 minutes with "stage time budget reached" and a stage summary of 0 of 4 conditions, while the model had spent its first rounds filling in milestone forms. This release treats stage budgets as checkpoints and makes the bookkeeping tools forgiving, so the rounds go to the task itself.

- **Stage budgets are checkpoints, not stops.** When the minutes, tokens or tool rounds of a stage run out, the executor checks whether the stage did real work (files written, commands run, pages read). If it did, the next stage opens on its own and the task continues; only a stage with no new real operation pauses, with the reason spelled out. Streaming answers and pending tool calls are never cut off. Team members, ad-hoc subagents and the Butler keep their budgets as hard limits.
- **Bookkeeping is forgiving.** Missing evidence on a milestone, a completion note or a model review is filled in by the executor from its own record of successful steps; a milestone without a linked check can complete; a milestone whose check has not passed is quietly marked for verification instead of rejected. What still stops a run: claiming completion with no operation at all, answering with only a plan, skipping a requested test or push, or a registered program check that fails.
- **The stage summary shows real work.** It now says how many operations completed and how many files were written, across how many automatically opened stages, instead of only the checklist count.

See the [4.13.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.13.0.md).

## 4.12.0 — Android rebuilt on the desktop code

The Android app had been a separate copy of the code since around 4.0, so most of what shipped after 4.4 never reached phones. From this release the Android line is the desktop code plus a thin mobile layer, so phones carry the same features and fixes as desktop and web.

- **Same code as desktop.** The Android line now starts from the desktop source and adds back only what is mobile: account-scoped storage, the system keystore, the phone file picker, the phone layout and the phone-side Butler collector. The native Android and iOS projects are unchanged.
- **What phones gain.** Agent-team tasks synced from your computer with acceptance on the phone, team claims seen both ways, Claudex remote view and decisions, the cloud file library, the credit panel, smart search, result versions and human acceptance, 4.10.0's parallel chats and scanned-PDF import, and 4.11.0's offline previews and approval rules. Work that needs the computer's own tools still says it runs on the desktop, as on the web.
- **Butler control always checks the account.** A control call can no longer skip the signed-in account and session check, on every platform.
- **License texts inside the app.** The Android build ships the license, the notice and the full third-party license text.

See the [4.12.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.12.0.md).

## 4.11.0 — Previews stay offline; team claims seen both ways; web and Android ask like the desktop

This update closes gaps listed as unfinished in earlier release notes. A generated HTML preview can no longer reach the network, two computers running the same team project now see each other's running task, and the web and Android apps decide which actions to ask about with the same rules as the desktop.

- **Previews stay offline.** Model-generated HTML and SVG previews run with no sandbox permissions and a content policy that allows only embedded resources, so a remote image address can no longer carry what the model has read out of the app. The desktop also blocks the preview frame from navigating anywhere.
- **Team claims both ways.** When the same project is restored on two computers, the one that does not host it now publishes its running tasks too, so neither starts a task the other is running, and phones show which computer is running it.
- **Web and Android ask like the desktop.** "Auto-approve edits" lets only file edits and clicks through; the first visit to a new website after reading local files asks first; writes to files that git, npm or CI run automatically always ask. The web's own team store now also waits for the human acceptance of a predecessor task.
- **Butler limits keep the newest records.** After a sync, the caps on goals, briefs, skills, jobs and feedback drop the oldest entries instead of whichever the server listed last, and the account window lists which items conflict, not only how many.
- **Android catches up.** The Android line carries 4.10.0's parallel chats, scanned-PDF import and denser conversation, plus this release's fixes.

See the [4.11.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.11.0.md).

## 4.10.0 — Parallel chats stop waiting on each other; any PDF can be read

Three things a person hit daily. A chat no longer queues behind another chat that happens to work in the same folder: each runs on its own route and model, and only the moment of writing a file takes turns. A PDF is never refused for lacking a text layer: scanned and slide-image PDFs come in as page images that a vision model reads directly. And the conversation shows more per screen.

- **Chats run in parallel in the same folder.** The run-wide workspace lock is gone, along with "waiting for … to release the workspace". File-writing tool calls (write, edit, delete, write document) on overlapping folders take turns one call at a time across chats; reading, thinking, commands and other tools stay parallel.
- **Every PDF comes in.** Extractable text is attached as before; pages without a text layer (up to 20) are rendered to images and attached, in the desktop picker, drag and drop, paste, the web and the phone. Rendering is an enhancement: if it fails, the text and the local path still arrive.
- **Optional marker conversion.** `read_document` uses [marker](https://github.com/datalab-to/marker) for layout analysis and OCR when the built-in extraction finds no text and marker is installed on this computer (`pip install marker-pdf`). It is never bundled, never downloaded, and never blocks anything: missing, failed or timed-out runs fall back to the built-in result.
- **A denser conversation.** Answer text and spacing are tighter, the input box is one line with smaller controls, and stream/effort sit in the bottom bar instead of a row of their own.

See the [4.10.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.10.0.md).

## 4.9.0 — Team tasks across devices and accounts; uploads signed with type and size

This update closes the gap left by 4.8.0: Agent-team tasks are now visible, stoppable and acceptable from your other devices, and a team project can be published to a shared board so someone on another account can complete the independent acceptance. Upload links now carry the file's type and size in the signature, so the storage bucket itself refuses a mismatched upload.

- **Your other devices.** Project summaries, tasks, result versions, acceptance records and claims sync end-to-end encrypted to your phone and the web; there you can accept, return, start or stop, and the executing computer applies each decision once, in order, rejecting an acceptance whose version has changed. A task running on another computer is never started twice.
- **Acceptance across accounts.** A team project can be published, by hand, to a shared board: members see tasks and result versions under Groups & sharing and accept there; the server enforces by account that the producer cannot accept their own version, that a rejection needs a reason, and that versions are append-only; the executing computer pulls those acceptances back. Before publishing you are told what becomes plaintext on the server (titles, summaries, digests, names); files, run transcripts and materials are never uploaded.
- **Dependencies wait for a person.** In team projects a dependent task starts only after its predecessor's current version has been accepted by a person (off by default for personal projects; a project setting).
- **Signed uploads.** Single-PUT upload links sign Content-Type and Content-Length, so the bucket refuses an upload that differs from what was declared; older clients sign length only and keep working. The real R2 acceptance (5 GiB transfer, CORS, multipart complete and abort) passed in full and the script was updated.
- **The installers repository's README** now syncs the product story from this page on every release.

See the [4.9.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.9.0.md).

## 4.8.0 — Claudex implement-and-check, result versions and human acceptance

Claudex moves from read-only review to "implement in an isolated copy, have the other party check it independently, you accept and merge", and team-task results become digested versions that human acceptance is bound to.

- **Implement and check independently.** Pick an accepted plan version and a Git project, confirm the write grant, and the coordinator creates an isolated worktree from the current commit. The implementer can write only there: Codex runs in a sandbox limited to that directory with shell and network off; Claude Code gets only Read / Grep / Glob / Edit / Write scoped to the directory (no Bash, which cannot be confined). Any write outside refuses the whole request and is recorded. The checker reads the full change in a new session. The fingerprint covers the diff and untracked files; you accept a fingerprint, and any later change voids it. Merging into your checkout happens only after acceptance and on a clean tree; a patch can be copied instead. A second start never runs twice; stopping goes through the execution registry.
- **Result versions and human acceptance.** Every delivery is recorded as a digested version; acceptance is bound to a version and is void once the result changes, sending the task back to "awaiting acceptance". AI verdicts remain references; only a person's acceptance completes a task, and the overview counts only those. Personal projects: the owner accepts; team projects: the acceptor must be a different signed-in account from whoever started the run.
- **Known limit.** Two-person acceptance in a team project can only be completed within the same local data today: team tasks are not yet synced across devices or accounts, so the second person does not see the task on their own device. The data model is ready; the sync is the next step.

See the [4.8.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.8.0.md).

## 4.7.0 — Official hosted route and a billing interface (no collection), Claudex hosted mode

This update adds an optional official hosted route and a billing interface that keeps accounts but collects no money. It is one more route you may pick, never selected for you; the Butler never buys credits or changes plans.

- **Official route.** Once signed in, add "Official route" under API credentials: no key to paste, models come from the server catalog with context length and credit prices. Requests go through the server's OpenAI-compatible endpoint; upstream keys stay on the server; each request reserves credits first, settles on the usage the upstream reports, and releases on failure. When credits run short you are told what is left and what the call needs, with two ways out (another route, or the next period) and no retry loop.
- **Credits page.** Settings gains "Credits": plan, remaining / reserved / used this period, period end and the last 50 ledger rows (purpose, model). When the server has no payment set up it says so in one line and shows no payment entry.
- **Claudex hosted mode.** Either party can use an official-route model, shown as "hosted credits"; every round reserves before it runs, and a round the budget cannot cover does not start.
- **Server.** A provider adapter (OpenRouter first, every call with `require_parameters` so silently ignored parameters are refused; another provider is one adapter plus `HOSTED_PROVIDER`); three ledgers (upstream cost, user credits, collections); plan fields and entitlements for 2.99 / 4.99 / 19.99 USD per month; payment callbacks idempotent by event id. Not in this version: real collection, enterprise seats, annual plans.

See the [4.7.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.7.0.md).

## 4.6.0 — Execution registry, device receipts, and a capability notice before upload

This update finishes the remaining phase-one reliability work: stopping no longer relies on guesswork, every execution is registered and its exit recorded; each device reports stop progress with signed receipts; and before a file is uploaded you are told whether it can be stored, previewed, and handed to the current model.

- **Every execution is registered.** Model requests, tools, local clients (Codex, Claude Code, Kimi, Grok), Work, subagents, hooks and collectors persist their ownership (account, device, stop epoch) before they start; a stop closes every entry point first, then waits for registered executions to actually exit and records how each one ended. Sending a kill is not an exit; executions left over from before a restart are marked "unknown" and listed in the Butler panel and the activity log. Late collectors and hooks cannot start after a stop.
- **Device receipts.** Each executing computer signs receipts with a device key independent of the end-to-end encryption identity: received → dispatch banned → ending → confirmed exited. The server verifies signatures, rejects replays, forgeries and a stale resume overriding a newer pause, and aggregates per device; offline, outdated and restart-leftover devices show as "unknown". The interface says "stopped across devices" only when the server enables it and every device has confirmed.
- **Capability notice before upload.** After picking a file you see four lines: store, preview, edit, hand to the current model, with limits taken from the server's real response; an older server without those fields shows "unknown" and asks the admin to update instead of guessing.
- **Real cloud acceptance tooling.** `scripts/r2-acceptance.mjs` runs only against an isolated bucket whose name contains `-acceptance` or `-test`, covering conditional signing, URLs after multipart completion and abort, CORS and an optional real 5 GiB transfer, and writes a Markdown report; the real-device gap list lives in `docs/acceptance/real-device-gaps.md`.

See the [4.6.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.6.0.md).

## 4.5.0 — Claudex co-refinement, role rotation, API-route parties and cross-device decisions

Claudex can now start from a goal instead of a finished plan; either party can be a local Codex / Claude Code subscription or one of your own API routes; and your phone and the web can follow a run and decide.

- **Co-refine mode.** You give the goal and materials; the author drafts version 1 and the reviewer checks it item by item. Every later round rotates: last round's reviewer revises, last round's author reviews. The side that wrote a version never reviews it, enforced in code. An unchanged plan stops the run as "no new evidence".
- **An API route can be a party.** Choose "API route" from your own credentials and model list; keys never leave the local keystore. The vendor family is judged from the actual model, and two parties from the same family are refused. Each round records the requested model, the model the upstream actually returned, and where the usage figures came from (API, client report, or unknown).
- **A failing party never degrades the run to one model.** Only with "allow same-model failover" ticked does it retry once on another route of the same family, recording the actual provider; otherwise it stops and says which side failed and how to fix it.
- **See, stop and decide from your phone or the web.** Run summaries (version digests, finding counts, pending decisions) sync end-to-end encrypted; from another device you can stop a run, return it with a reason, or accept a version. Acceptance is bound to that version's digest, so a desktop that sees the plan has changed rejects it and tells you. Execution stays on the desktop.

A same-budget "single model vs Claudex" comparison is in `scripts/run-team-strategy-comparison.cjs`. See the [4.5.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.5.0.md).

## 4.4.0 — Today's Butler on its own, feedback that changes the inbox, Claudex up front

This update separates Today's Butler from the Agent team, makes your feedback on each brief item change what the Butler does next, and puts Claudex where you can see it.

- **Today's Butler is a third top-level entry.** The sidebar switch is now Chat / Agent team / Today's Butler, and the Butler opens as a full page instead of a dialog. The chat sidebar keeps a collapsible summary card: whether today's brief exists and how many suggestions await your decision. The Agent team's intake page, formerly called "Butler", is now "Start a task", and every navigation item has its own icon.
- **Feedback changes the inbox.** Mark a brief item "wrong" and say why, and the Butler treats it as a correction of that need: the inbox suggestion shows your own words and "waiting for the Butler to rewrite", with "Do it" disabled; once the need is rewritten or split from your words, old suggestions are replaced by new ones. "Not my need" withdraws the need and its suggestions.
- **Feedback reaches the next brief.** Everything you said since the previous brief goes into the next morning or evening brief, which acknowledges each correction up front and stops re-proposing the old framing. Needs you already answered do not reappear unless there is new progress; unanswered ones are marked "reminder". Every brief item can be collapsed.
- **Claudex up front.** "Claudex · two-model review" is second in the Agent team navigation; a card at the top of the overview starts a review in one click when Codex and Claude Code are both signed in, and says exactly which step is missing otherwise. The chat sidebar and the web "About wickrunAI" page link to it too.

The Cloud files tab in Settings now explains its state and the next step instead of showing nothing. See the [4.4.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.4.0.md).

## 4.3.0 — A Butler you can correct, and smart search

This update makes Today's Butler easier to correct and better at seeing what you actually need, and lets in-app search understand questions like "the feature we talked about yesterday".

- **Corrections always save.** Each goal has one box, "Correct or add to this need". Saving needs no model budget, takes effect at once and is still there when you reopen; the next analysis rewrites the goal from your own words and splits it if you named several needs. A cloud sync could previously overwrite a correction you had just saved; that is fixed.
- **Needs reasoned from first principles.** The Butler asks what result you are after before looking at the object you touched. Looking at one fund becomes "find investment for the project", and research covers comparable options in your city, province, country and North America.
- **Urgent and important, told apart.** Every goal shows urgency and importance, and the inbox and goal list are ordered by them. You can set them by hand; the Butler learns from your settings and from how quickly you accept or set aside its suggestions.
- **Smart search.** Press Enter in the sidebar search box, or click Smart search. "Yesterday", "last week" and "last 3 days" are read in local time, and asked before 5 a.m. "yesterday" also covers the day before. The model chosen for the Butler turns the topic into the words your records may use and ranks the most relevant conversations, workflow runs and task discussions. These calls do not count toward the Butler's daily budget; with no model chosen, search still matches the words typed and the time.

The web app gains About wickrunAI and About the author pages. See the [4.3.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.3.0.md).

## 4.2.0 — Two-model review

This update adds Two-model review to the collaboration space: two models from different vendors take turns reviewing and revising an important plan, and you decide which version to accept. The daily Butler never starts it on its own.

- **One reviews, one revises.** Write the goal, acceptance criteria and plan, then pick the author and the reviewer (Codex or Claude Code signed in on this computer). The reviewer raises findings; the author accepts, rebuts, or hands each one to you, and each revision is saved as a new version.
- **Every point needs a source.** Quotes must appear word for word in the plan or material, or they count only as assumptions. A verdict that is not about the current version is discarded.
- **No endless debate.** It stops for you on approval, a blocker, a decision only you can make, a round with nothing new, or when rounds or time run out. Two models from the same vendor cannot start a review.
- **Your acceptance is tied to one version.** If the plan changes again, the earlier acceptance no longer counts. Both sides are read-only, never edit your files, and never switch a subscription to a paid API.

This version covers plan review only; implementation with independent inspection comes later. See the [4.2.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.2.0.md).

## 4.1.0 — Project spaces and a Butler that asks first

This update turns the collaboration space into project spaces where people and AI move a goal forward together, makes Today's Butler ask for consent and suggest quietly, and fixes the repeated blank window on machines with a lot of data.

- **Project spaces.** Write a goal, break it into tasks, and give each task an assignee, a reviewer, and a due date. AI can judge a delivery against the acceptance criteria, but a task is done only when its assignee confirms and a different person approves. Every verdict records who gave it, when, and with which model.
- **Consent before the Butler starts.** A notice says what it uses, where that goes, and what it never does; until you agree, nothing is collected, analyzed, or run. "What Butler remembers" lets you delete items one by one, clear everything, download your data, or withdraw consent, and deletions sync to all your devices.
- **A suggestions inbox.** The Butler no longer starts work on its own by default. It puts what it would do in an inbox and starts only when you choose "Do it"; accepted work uses file tools only, in an isolated folder.
- **AI-written briefs and a first-open greeting.** Your chosen model writes the morning and evening briefs and a short greeting. The first time you open the app each day, a dismissible card appears at the top instead of a dialog. The Butler can also learn your usage habits on the device, keeping only a one-sentence summary, and you can turn this off.
- **No more repeated blank windows.** Full cloud syncs run only when something changed, Butler sync reads a small dedicated record, and unchanged records are not rewritten. On the affected machine, the window went from crashing about every 4 minutes to running for over an hour without a crash, and a question sent during a sync no longer disappears under an older copy.

Payments, transfers, trades, and negotiation stay fully blocked, and project boards are not end-to-end encrypted. Sidebar titles now use the full row and show their actions on hover. See the [4.1.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.1.0.md).

## 4.0.0 — Cross-account collaboration

This major update adds a shared workspace for people using different wickrunAI accounts. Share files and folders, join the same conversation, maintain project instructions together, or jointly edit a workflow and inspect its published execution history.

- **Choose who can do what.** Grant viewer, commenter, or editor access through a link, verified email invitations, or personal and company spaces. Children inherit their parent’s access. Guests can view public links; guest comments require the owner to enable them. Changes, versions, and messages retain their author and time.
- **Work together with your own models.** Human messages appear on the left and AI replies on the right with the generating account and model. Private and shared annotations stay outside AI requests and memory. Concurrent messages are preserved; conflicting edits keep your draft.
- **Transfer files up to 100 MB.** Shared uploads and downloads use bounded chunks and store file versions by reference. Document attachments also accept 100 MB; large extracted text shows a clearly marked preview instead of putting the whole file into a model request. Image and media inputs retain their separate model limits.
- **Change simple settings beside your message.** Click native AI effort levels and the Streaming / Non-streaming control directly in the composer. Adjust mapping opens the current conversation’s thinking settings. The right panel groups response and thinking options together.
- **Connect independent teams and Agents.** Both sides accept a connection before handing over a goal, summary, and explicitly selected text files. Each side keeps its own workflow, tools, and model settings. Received work opens as a draft; copied Agents and routines start disabled.
- **Keep personal data personal.** Personal Butler goals, memory, signals, tasks, logs, and derived conversations cannot enter sharing. Company administrators only manage their shared space. Sharing excludes credentials and tool permissions.
- **Keep this computer’s history when signing in.** The first desktop account continues the existing local conversations, project memory, model setup, and workflows. Later accounts remain isolated. The empty-workspace first-login issue in 3.0.1 recovers when the original data remains and the new local account has no work to overwrite.

Personal and company spaces are currently free, with individual monthly and company seat billing reserved for future use. Google sign-in is available; the common wickrunAI identity model supports other providers, while Apple setup is still pending. This release requires matching Windows, macOS, Linux, and Android preview packages. See [sharing and handoffs](https://github.com/lifishard/wickrunAI/blob/main/docs/SHARING_COLLABORATION.md) and the [4.0.0 release notes](https://github.com/lifishard/wickrunAI/blob/main/docs/releases/v4.0.0.md).

**Android 3.0.0 migration:** its temporary signing key was not retained, so 4.0.0 cannot install over that preview. Back up the data you need before uninstalling and reinstalling; uninstalling deletes data that has not been backed up. The application ID remains the same. Future releases require the fixed 4.0.0 signing certificate.

**When a route dies mid-task, the task does not.** This is the notice you get, verbatim, and the run continues from where it stopped:

```
This account is out of quota. Handed to glm-5.2 from your failover order;
the saved progress carries over.

This account is out of quota. Handed to kimi-k3 from your failover order;
the saved progress carries over.
```

Three routes, two handovers, one task, nobody watching. The order is a list **you** wrote — the program walks it, it does not decide for you which of your routes is the cheap one. [How it decides](https://github.com/lifishard/wickrunAI/blob/main/docs/llm-failover.md).

## 60 seconds to your first answer

1. **Download.** Open the [download chooser](https://wickrunai.com/download), select your system and configuration, and install. No account, no sign-up.
2. **Add one key.** Settings → API credentials → paste a Base URL and an API key, press **Test connection**. Pick the OpenRouter preset if you want a free route to start with. The key is encrypted into your OS keystore — Windows DPAPI, macOS Keychain, Linux libsecret.
3. **Send a message.** Choose a model next to the composer and ask something. That is the whole setup.

Then, when you want more: add a second key and put both routes in the failover list, add a working directory for file tools, or configure a search service. See [Configuration](https://github.com/lifishard/wickrunAI/blob/main/docs/CONFIGURATION.md).

## How it compares

wickrunAI is one of many bring-your-own-key clients. What is specific to it is what happens when a model stops working in the middle of a task.

Only the wickrunAI column is a claim about this repository, verified against the source. For the other products, a cell says **—** wherever this table's authors have not verified the answer; **— does not mean the product lacks the feature.** Correct any of it by opening an issue.

| | wickrunAI | Chatbox | LobeChat | Cherry Studio | Open WebUI |
|---|---|---|---|---|---|
| Bring your own API key | Yes | Yes | Yes | Yes | Yes |
| Runs as a desktop application | Yes (Electron) | Yes | — | Yes | No — self-hosted web server |
| Automatic handover to the next route mid-task, carrying saved progress | Yes | — | — | — | — |
| Failover list scoped session → project → app, each level able to inherit or override | Yes | — | — | — | — |
| Route ranking computed from your own finished tasks | Yes | — | — | — | — |
| Keys encrypted into the OS keystore | Yes | — | — | — | — |
| Phone relays tool calls to your desktop over the LAN | Yes | — | — | — | — |
| Calls subscription CLIs installed on your machine (Claude Code, Codex, Kimi Code) | Yes | — | — | — | — |
| License | Proprietary, free to use | — | — | — | — |

The four rows in the middle are the ones worth reading the code for:

- **[LLM failover](https://github.com/lifishard/wickrunAI/blob/main/docs/llm-failover.md)** — which errors trigger a handover, and which three deliberately do not, because switching models cannot fix a malformed request, a behavioural loop, or a cause nobody identified.
- **[Multi-model router](https://github.com/lifishard/wickrunAI/blob/main/docs/multi-model-router.md)** — done rates computed per hashed route alias, an eight-sample floor before any number is shown, and a reorder button you have to click, because the program does not know which of your routes is the free one.
- **[BYOK](https://github.com/lifishard/wickrunAI/blob/main/docs/byok-ai-client.md)** — where the key goes and what never leaves the machine.
- **[Mobile remote bridge](https://github.com/lifishard/wickrunAI/blob/main/docs/mobile-remote-bridge.md)** — how a phone with no file access still gets file, browser and CLI tools.

Full documentation index: **[docs/README.md](https://github.com/lifishard/wickrunAI/blob/main/docs/README.md)**.

## What it is

wickrunAI is an open-source AI client for Windows, macOS, and Linux. Connect any service that uses the OpenAI-compatible API and use it to research topics, work through documents, read and write files, drive Chrome, or call the Claude Code installed on your machine.

On a long task you can have one model gather the material, pause, then hand the work to another model to organize or check it. wickrunAI keeps your requirements, the run journal, and the original evidence. Press Continue and the new model resumes from the saved position. You still need to check the result, above all citations, arithmetic, and generated files. See [Model handoff](https://github.com/lifishard/wickrunAI/blob/main/docs/MODEL_HANDOFF.md) for how the relay works.

Use an API key from a model provider, or connect an official client you already run on your machine from the desktop model picker. Accounts, subscriptions, and API charges stay with the provider. An Android client connects to your computer over the local network; it has not been verified on a physical device yet.

The interface reads in Simplified Chinese, Traditional Chinese, and English, switchable from the top right. Most reference documents under `docs/` are in Chinese; the concept pages linked above are in English.

## What it can do

| Job | How |
|---|---|
| Research | Configure Tavily, Brave, or SearXNG, then read the source links in the answer |
| Work with files | Add a working directory, then have the model read material and produce documents or spreadsheets; open the result from its file card |
| Continue a long task | Pause, restart the app, or switch models, then resume from the saved run journal |
| Drive a browser | Launch the dedicated Chrome instance, sign in to the sites you need, then authorize the model |
| Code and repository work | Read GitHub repositories, search code, or call an installed Claude Code; run commands under your permission setting |
| Organize projects | Save shared instructions, reference documents, and prompts for a group of conversations |
| Use skills | Import a `SKILL.md` skill and call it with `/name` in a conversation |
| Run on a schedule | Set an interval, daily, weekly, or cron task; it needs the relevant device and services available when it fires |
| Inspect calls | Review connections, usage, and failures; on a rate limit it waits and retries under the recovery policy |

Models differ in what they support for tool calls, images, and reasoning parameters. On a new endpoint, test the connection first, then try a small task.

## Permissions and data

Tool permissions are set per conversation, and file tools only reach the working directories you name. Command-line and browser tools act on your computer or on websites, so check the task and the target before you authorize them.

On desktop, API keys go into the operating system's encrypted storage where it is available. Configuration, conversations, and task material stay on your machine; when you call a model or a tool, the relevant content goes to the service you configured. Key storage, remote connections, and permission limits are in [Security](https://github.com/lifishard/wickrunAI/blob/main/SECURITY.md).

## Disclaimer

wickrunAI is an independent service and is not affiliated with, endorsed by, or owned by Anthropic, OpenAI, Google, xAI, SenseTime, Moonshot AI, OpenRouter, or any other model provider or service named in this repository. Product names, logos and trademarks are the property of their respective owners and are used here only to describe what this client can connect to.

Connecting to a provider requires your own account and credentials with that provider, and your use of their service is governed by their terms, not by this project's. Accounts, subscriptions, quotas and charges stay with the provider. wickrunAI does not resell access to any of them. The web version relays your requests to the provider you chose, with your own key, and does not store them.

## Google account and cloud sync

Desktop and web keep separate repositories and share one backend. Chats, projects, skills and task history can follow the same Google account. Model API keys stay on each device unless you turn on key sync in the account window. [Setup, import and limits](https://github.com/lifishard/wickrunAI/blob/main/docs/cloud-accounts.md).

Changes and the supported scope of that version: [2.20.5 upgrade notes](https://github.com/lifishard/wickrunAI/blob/main/docs/UPGRADE-2.20.5.md).

## Meeting rooms

The team workspace now includes human-chaired meetings: shared material, referenced replies, constructive disagreement, explicit questions to the user, and confirmed minutes. Meetings never replace independent quality review. Native ChatGPT participation requires separate MCP connection setup and account/client validation; ordinary chats are not automatically awakened. See [meeting room setup and limits](https://github.com/lifishard/wickrunAI/blob/main/docs/MEETING_ROOM.md).

---

<!-- releases-readme:footer -->

## Feedback

Report problems in [Issues](https://github.com/lifishard/wickrunAI-releases/issues); report security issues privately to admin@wickrunai.com.

## License

wickrunAI 4.1.1 and later are proprietary software, free to use under the [wickrunAI Software License](LICENSE). This repository contains installers only, not source code. Versions 4.1.0 and earlier were released under the Apache License 2.0. Open-source components keep their own licenses, listed in `THIRD_PARTY_LICENSES.txt` inside the app.

<!-- /releases-readme:footer -->
