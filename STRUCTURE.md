# Structure

How this repository is laid out. Folder names are in English, the language of Zambian law. No folder holds more than 1,000 entries.

| Folder | What it holds | Path pattern | Example |
| --- | --- | --- | --- |
| `constitution/` | The Constitution of Zambia Act, 1991 and the Constitution (its Schedule), as amended | `sec-<n>.md` (the Act), `art-<nnn>.md` (the Constitution) | `constitution/art-047.md` |
| `acts/` | Acts of Parliament, by the year and number of the Act as enacted. A folder holds the Act as passed, or (for the acts taken from ZambiaLII) every dated version of it | `acts/<year>/<nnn>-<short-title>/` | `acts/2017/010-companies-act/` |
| `chapters/` | Chapters of the Laws of Zambia (the Revised Edition) whose Act number is not known here: the consolidated text, by chapter number | `chapters/cap-<nnn>-<short-title>/` | `chapters/cap-087-penal-code/` |
| `subsidiary/` | Statutory instruments and other subsidiary legislation, by year and S.I. number; instruments without an S.I. number go by year and title; consolidated instruments of the Revised Edition by chapter | `subsidiary/<year>/<nnn>-<title>/`, `subsidiary/<year>/<title>/`, `subsidiary/cap-<nnn>/<title>/` | `subsidiary/2012/027-high-court-amendment-rules-2012/` |
| `data/` | Tables about the record (laws, versions, charts) | | `data/laws.csv` |
| `tools/` | Scripts to read the record (`on.py`: a provision on a date) | | `tools/on.py` |
| `visualisations/`, `vulnerabilities/` | Charts and drafting-mistake reports (placeholders) | | |

Inside each act, chapter or instrument folder: one file per section (`sec-<nnn>.md`, with a letter suffix for inserted sections such as `sec-009a.md`), `schedule-<nn>.md` per schedule, `preamble.md` (long title and enacting words), and a `README.md` listing the provisions. An Act whose sections could not be read apart from its PDF is one `text.md`, and its commit says `Layout: whole text`.

Case law is kept in a separate private repository (`zambia-law-caselaw`): `<court>/<year>/<date>-<title>-p<id>.md`.

Each commit is one version on the day it took effect (noon, Africa/Lusaka), with `In-force:` and `In-force-basis:` trailers. Versions before 1970 carry the 1970-01-01 git date (git cannot store earlier days); the real day is in the subject and the `In-force:` trailer. Copies taken from a secondary publisher carry `Source-status: secondary copy (...)`.

Regional law binding on Zambia as a member State (2026-11-27 (second pass)): `sadc/<treaty|protocols|agreements|charters>/<year>/<title>/`
(SADC instruments, dated by signature) and `comesa/gazette/<year>/<vol-nn-no-n>/` (Official Gazette of COMESA, by issue).
