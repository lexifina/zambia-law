# Zambia: law history in git

The law of Zambia as a git history: one file per section or article, one commit per version on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every paragraph; `git log` lists every change to a provision; picking a date gives the text in force that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is Zambia's national law, which global-law reads at `zambia/national/acts/`.

**What is in it now:** the Constitution and 26 other Acts from ZambiaLII, among them the Lands Act, the Marriage Act, the Public Procurement Act 2020 and the Data Protection Act 2021, with 55 versions from 31 December 1996 to 12 June 2026. [`REPRODUCE.md`](REPRODUCE.md) lists every act with its versions; [`data/laws.csv`](data/laws.csv) lists the 41 Acts the history names (13 acts as enacted and 28 amending Acts), with their dates.

Each act is a folder named after its short title, with one file per section, article or schedule, plus `long-title.md` and a `README.md` listing its provisions and their changes. In `constitution/` the Constitution of Zambia Act's own sections are `sec-<number>.md` and the Constitution, its Schedule, is `art-<number>.md` (`constitution/art-047.md` is Article 47, on electoral systems).

The text is in English, as ZambiaLII publishes it; its editorial notes (kept only where a provision has no other text) and the Part and Chapter headings are left out.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every change to Article 47 of the Constitution | `git log -p --word-diff -- constitution/art-047.md` |
| Which law wrote each line of Article 47? | `git blame constitution/art-047.md` |
| Every version of the Constitution, with the day each took effect | `git log --format="%h %(trailers:key=In-force,valueonly,separator=) %an" -- constitution ':!constitution/README.md'` |
| Article 47 as in force on 1 January 2020 | `python tools/on.py 2020-01-01 constitution art-047` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about Zambian law](https://global-law.lexifina.com/v1/try_claude?country=zambia)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=zambia)**: the same question in ChatGPT.
- **[Call the API in your browser](https://global-law.lexifina.com/v1/search_law?query=bail&jurisdictions=zambia)**: a search of Zambian law for "bail", returned as JSON. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in English.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add zambia/national/acts
python3 tools/law.py show 2026-01-01 zambia/national/acts/constitution/art-047.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, Africa/Lusaka, on the day the version took effect, and carries it in its `In-force:` trailer. The day is ZambiaLII's, the date of its point-in-time version (expression):

- for an amendment, the day it came into force, as ZambiaLII's amendment list gives it ("[Amended by <Act> on <date>]");
- for the 1996 Revised Edition of the Laws of Zambia, the first version of 14 acts, the day the edition is as at: 31 December 1996;
- for an act as enacted, its Gazette publication, or the commencement day ZambiaLII states where it gives one (the Public Procurement Act 2020, published on 23 November 2020, is dated 16 April 2021, as are six other acts by their commencement orders).

Each change is credited to the Act ZambiaLII's History names (`Act 2 of 2016`, `Act 13 of 2025`); each of the 28 amendments names one, so no change is left to the publisher. The first version of 13 acts is the act as enacted, credited to the act itself; for the other 14 it is the "oldest version available", credited to ZambiaLII.

## How it is checked

- `tools/check_repo.py` reads every version back from git on the day it took effect and on the day before, and compares it with the corpus: 55 versions of 27 acts, 0 mismatches (see [`REPRODUCE.md`](REPRODUCE.md)).
- Every version is parsed from an archived copy of its own dated expression page, whose sha256 is recorded with it; the newest version of each act is the one ZambiaLII's own listing named as current when it was read.
- A second build from the same corpus gave identical hashes for all 55 history commits and 96 tags.
- History is append-only: no merge commits and no commit date that goes backwards.

## What it does not show

- **Most Zambian law.** Only these 27 acts: no statutory instruments and no case law. Acts with a listed version that could not be read are left out, among them the Penal Code and the High Court Act; the Companies Act 2017, the Employment Code Act 2019 and the Income Tax Act are on ZambiaLII only as PDFs, and no OCR is used.
- **Changes before ZambiaLII's oldest version.** 14 acts, the Constitution among them, start at the 1996 Revised Edition, which already holds the earlier amendments.
- **One article across the 2016 amendment.** The Constitution of Zambia (Amendment) Act 2016 replaced most of the Constitution with new articles, and files are named by number, so on 5 January 2016 a file can change from one provision to another (`constitution/art-047.md` was on Deputy Ministers before); use `git log -p` around that day.
- **Changes within a line.** Each paragraph is one line, so blame credits a whole paragraph; use `git log -p --word-diff` for the words.

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| [ZambiaLII](https://zambialii.org) (Southern African Institute for Policy and Research, on the Laws.Africa Peachjam platform) | Legal information institute: consolidated acts | yes, each dated point-in-time version | The text, the day each version took effect, the History and amendment lists, and editorial notes naming the amending laws |
| [Internet Archive](https://web.archive.org) | Archived copies of ZambiaLII's pages | as archived | Every page was read from an archived copy |

## Licence

See [`LICENSE`](LICENSE). The texts are ZambiaLII's, under CC BY-NC 4.0 with ZambiaLII credited as the source, so they may be used only for non-commercial purposes; neither ZambiaLII nor Laws.Africa endorses this repository. Lexifina's arrangement, commit messages, tables and tools are CC0 1.0.

No AI model wrote, translated or corrected legal text, and none runs at build time; the scripts were written, and the acts chosen, by an AI model (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published
