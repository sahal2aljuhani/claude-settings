# Command centre: technical guide

«مركز قيادة رمز النظام» is a single HTML page (about 400 KB) published as a private claude.ai artifact:
https://claude.ai/artifact/CjWSErrZtGqWASBT1QBQ2S

It is plain HTML, CSS and JavaScript with no framework. Libraries: SheetJS (`xlsx` 0.18.5 from cdnjs) for Excel. Canvas 2D draws the live HQ. Web Crypto (PBKDF2-SHA256, 210k iterations) hashes passwords. All UI text is Arabic, right-to-left.

## Contents
1. Runtime capabilities
2. Where data is saved
3. Sections of the page
4. Editing the code
5. Editing the data
6. Testing
7. Known limits

## 1. Runtime capabilities (keep them on every publish)

```json
{"db": {"rules": [{"path": "ramz", "read": "admin", "write": "admin"}, {"path": "leads", "read": "admin", "write": "admin"}]},
 "downloads": {}, "sample": {},
 "mcp": {"servers": [{"server": "Microsoft 365", "tools": ["read_resource", "sharepoint_create_folder", "sharepoint_upload_file", "sharepoint_update_file"]}]}}
```

Omitting `capabilities` on a republish carries these forward. Passing a non-empty object replaces them all, so restate every entry if you ever change one.
- `db`: shared storage. Without it the page falls back to the browser's localStorage.
- `sample`: Claude writes employee replies, reports, the weekly plan and the daily script. Without it the page uses built-in templates.
- `mcp`: Excel on OneDrive.
- `downloads`: file saves.

## 2. Where data is saved

The global object `S` is split into five database documents. Each document has a single field, `json`.

| Document | Keys inside |
|---|---|
| `ramz/state` | simulation, tasks, reports, talk, decisions, commands, rules, content, mail, weekly, `scripts` (daily video scripts), employee live status `emp` |
| `ramz/org` | `org` (teams and sources), `projects`, `ai`, `leadStatus`, `company` (name, `nameEn`, email, logo, `logoSize`, `logoFit`, `charter`), `sec` |
| `ramz/acct` | `acct` (entries, subs, bank, settings), `aiUsage`, `reminders` |
| `ramz/auth` | `auth` (users with password hashes, settings, fails), `audit` |
| `ramz/pdata` | per-project saved data for non-current projects |

Leads (country site lists) live in `leads/meta` plus chunks `leads/c000`, `leads/c001`, and so on.

The page saves changed parts every 8 seconds. Before writing a part it re-reads that document. If someone else changed it (you, from this chat, or another tab), the page adopts the newer copy instead of overwriting it. Tabs opened before that protection existed (version 12) can still overwrite, so ask the owner to close old tabs.

## 3. Sections (ids)

| id | Section |
|---|---|
| `hq` | Live HQ: realistic office on canvas, with server room `srv`, glass meeting room `meet`, lounge, CEO office, merge room |
| `projects` | Projects |
| `charter` | Company charter, plus each team's role |
| `overview` | Unified KPIs |
| `pipeline` | Analysis chains: source → analyst → manager → tasks → quality check |
| `hub` | Merge room |
| `ceo` | CEO office: commands to employees |
| `room` | Discussion room |
| `acct` | Accounting: VAT, zakat, bank reconciliation, subscriptions |
| `rem` | Reminders and renewals (owner employee `yousef`) |
| `leads` | Active Arab sites, with the Excel-on-OneDrive panel |
| `gov` | Governance and rules |
| `security` | Cybersecurity |
| `script` | Daily video script (writer `sultan`), auto-written once a day |
| `content` | Weekly content plan |
| `mail` | Outgoing and incoming mail: manual log, no mailbox connected |
| `office` | Team directory |
| `hr` | Hiring |

The admin panel («لوحة التحكم») is owner only. Its tabs: company and security (logo size and display, Arabic and English names, owner password), charter, teams, employees (including the attire field), analysis chains, projects and tools, tasks, users and permissions, AI agent, data and backup, audit log.

Top bar: «↻ تحديث» saves, re-reads every document, redraws everything and re-runs the security scan and reminder check. Clicking the logo or the company name opens the company settings.

Employee prompts are built by `persona(id)`. It includes the charter (`S.company.charter`, up to 4,000 characters) and `TEAM_FOCUS[teamId]`. Simulated sales price a voice minute at model cost + 1 SAR.

## 4. Editing the code

1. Get the current source. Either `Artifact read` the dashboard URL, which saves a full copy locally and must be read through to the end before a publish is accepted, or read `dashboard-source.html.txt` from the archive with `Artifact read` plus `path`.
2. Copy it to a working file and edit it with exact, unique string replacements (a small Python script that asserts each match count is 1 works well). The file is large: never rewrite it from memory.
3. Extract the last `<script>…</script>` and run `node --check` on it.
4. Publish with `Artifact` using `url` set to the dashboard URL and `file_path` set to the working file. If the publish is refused with a diff, compare it to your changes, then publish again.
5. Optionally render it with Playwright (Chromium is preinstalled). Unhide `#app` and hide `#gate` to look at sections without logging in.
6. Refresh the archive copy afterwards.

## 5. Editing the data

1. `ArtifactData get`, collection `ramz`, `doc_id` the part, with `out_dir` so the large JSON goes to a file.
2. In Python, `o = json.loads(doc["json"])`, change what you need, then dump it back as `{"json": json.dumps(o, ensure_ascii=False, separators=(",", ":"))}` into a file.
3. `ArtifactData set` with `file_path` set to that file and `if_version` set to the version you read.
4. Ask the owner to press «↻ تحديث».

Examples already done this way: renaming خالد to روان (id `khaled`), adding the HR team (`hrteam`, lead `suhail`), adding `yousef` to `exec`, setting the owner name to سهل, rewriting all 51 employees' tasks, and storing the charter.

## 6. Testing

The archive does not keep a test script. To recreate one, use Playwright: seed localStorage with a throwaway owner account (PBKDF2 hash of a test password) via `addInitScript`, log in through the form, then click each `data-act` button and assert on the DOM. A previous run of 42 checks all passed: login, all sections, HQ animation, accounting maths, reminders, daily script, chains, governance, weekly plan, hiring policy, Excel import, every admin tab, refresh, lock, persistence after reload, phone width, zero script errors.

Things only the owner can test inside claude.ai: Claude-written replies, the shared database, and the Excel sync.

## 7. Known limits

- No server, so Salla, Zid, Shopify and GA4 figures are simulated.
- The dashboard cannot send phone or email notifications. Reminders show when it is opened.
- Browsers block audio before a tap. This matters for «سمّ» itself, which starts on the mic tap.
