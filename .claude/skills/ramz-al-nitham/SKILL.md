---
name: ramz-al-nitham
description: Full context for the owner's company «رمز النظام لتقنية المعلومات» (RAMZ AL-NITHAM IT, Tabuk, Saudi Arabia), its product «سمّ» (a Saudi-voiced AI receptionist for online stores and websites), and the «مركز قيادة رمز النظام» command-centre dashboard built for it on claude.ai. Read this skill first, before answering or editing anything, whenever the user mentions رمز النظام, Ramz, «سمّ», the company charter (الدستور), the dashboard or command centre (الداشبورد، مركز القيادة، المقر الحي), its employees (سلطان، روان، يوسف، سهيل، لولوة…), the Excel/OneDrive country files, the search-skill (مهارة البحث), or says "نكمل على المشروع", "نرجع للمشروع", "طوّر الداشبورد" — even if they don't name the company. It holds the links, where the data lives, the owner's decisions, and the safe way to edit the dashboard without losing data.
---

# رمز النظام لتقنية المعلومات: سياق المشروع

The owner is **سهل**, chairman of the board (رئيس مجلس الإدارة). He writes in Saudi Arabic and wants replies in clear Arabic. He is not a programmer: explain outcomes, not code, and keep jargon out unless he asks.

Read this file fully, then open the reference that matches the task:

| When the task is about | Read |
|---|---|
| What the company sells, «سمّ», pricing, free trial, what employees must follow | `references/charter.md` |
| Changing the dashboard: code, sections, data, publishing | `references/dashboard-guide.md` |
| Employees, teams, renaming or hiring | `references/team.md` |
| What was already decided or built, and what is pending | `references/history.md` |

## The company in one paragraph

رمز النظام is a Saudi IT company in **Tabuk**. Its main product is **«سمّ»**: a Saudi-voiced AI receptionist for websites and online stores (سلة، زد، and external sites). The visitor taps a floating mic **once**, the chat window opens and the voice greeting starts immediately, with no second tap; it keeps talking by voice and goes quiet only if the visitor switches to typing. Revenue is per **voice minute**: the company earns **one riyal profit per voice minute**. The free trial is **at most 10 minutes**. The company now has two technical-solution projects for businesses and individuals; «سمّ» is one, and the second has not been described yet, so ask before assuming.

## Where everything lives

- **Command centre (the dashboard):** https://claude.ai/artifact/CjWSErrZtGqWASBT1QBQ2S. One HTML file, private to the owner. Login user `SAHAL` (owner).
- **Project archive** (notes, charter copy, dashboard source backup, search-skill v1.1): https://claude.ai/artifact/K6ZWQhkSj5oStvVoKHL7EK. Read it with the Artifact tool (`action: "read"`, and `path` for its files) when you need the latest source or notes.
- **Dashboard data:** the artifact's database, collection `ramz`, documents `state`, `org`, `acct`, `auth`, `pdata`; leads in `leads/meta` and `leads/c000…`. Each document holds one field `json` (a JSON string).
- **Excel country files:** OneDrive folder «رمز النظام», one file per country named «رمز النظام - <الدولة>.xlsx», reached through the owner's Microsoft 365 connector.
- **Search skill v1.1** (SEO / Google AI answers checker with Arabic report): a single setup file stored in the archive as `search-skill-v1.1.md`; not yet uploaded to replace v1.0 in the owner's skills.

## Decisions the owner made (keep them)

- Do **not** rename the main project or the company in the dashboard; «رمز النظام» is the parent name over its projects.
- The hiring rule stays: 10+ years and level «خبير» or «كبير خبراء».
- The 40% resale clause was a mistake and was removed from the charter; never reintroduce it.
- Company email is not bought yet: do not connect any mailbox to the «الصادر والوارد» section until he says so.
- Women employees wear عباءة وحجاب in the live HQ; attire is set per employee (field `attire`: `thobe` / `abaya` / `formal`), defaulting from the grammatical gender of the job title, never guessed from the name.
- The live HQ must look like a real, human office (wood floors, furniture, people in Saudi dress), not neon schematics.

## Working safely on the dashboard

The dashboard keeps its own data and may be open in the owner's browser while you work, so careless edits lose data. The short version (details in `references/dashboard-guide.md`):

1. **Code changes:** get the current source (archive file `dashboard-source.html.txt`, or `Artifact read` of the dashboard URL), edit a local copy with small exact replacements, run `node --check` on the extracted `<script>`, then publish to the same URL. Before the first publish in a new session you must have read the live version, or the publish is refused.
2. **Data changes** (names, employees, charter text): read the document with `ArtifactData get`, change the parsed JSON, write it back with `set` and `if_version` equal to the version you read. Never retype the whole document by hand.
3. After either, tell the owner to press **«↻ تحديث»** in the dashboard (or close old tabs), because an old tab can hold stale data.
4. Keep the charter in two places in sync: the stored `org.company.charter` and the `CHARTER_DEFAULT` constant in the code.
5. After meaningful changes, refresh the archive: copy the new source to `dashboard-source.html.txt`, update `project-notes.md`, bump the version number on the archive page, and republish it.

## Things to remind the owner about when relevant

- His owner password is still the first one, which was sent in a chat: suggest changing it from «لوحة التحكم ← الشركة والأمان».
- Never ask for or accept passwords or API keys in chat; real platform keys belong on a server, not in the page.
- The dashboard cannot call Salla, Zid, Shopify or GA4 directly (no server); those numbers are simulated. Real data needs a small server or imported export files.
