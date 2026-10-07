<div align="center">

<picture><source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/lifishard/wickrunAI/main/public/brand/logo-dark.svg"><img src="https://raw.githubusercontent.com/lifishard/wickrunAI/main/public/brand/logo.svg" width="96" alt="wickrunAI"></picture>

# wickrunAI · 灯芯AI

**Every AI model you own, in one app — and when one fails, the next one takes over mid-task.**

Open or closed, paid or free. Bring your own keys; cloud sync is optional, and sharing never transfers your credentials.

[![Version](https://img.shields.io/badge/version-4.10.0-1f6feb)](https://github.com/lifishard/wickrunAI-releases/releases)
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
