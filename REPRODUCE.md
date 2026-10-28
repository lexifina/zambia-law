# How this repository was made (Zambia)

This file is written by the build on 2026-10-28, the day the source data was retrieved. Everything below is enough to rebuild this repository hash for hash.

## Sources

| Source | Address | Retrieved | Requests | Licence |
| --- | --- | --- | ---: | --- |
| ZambiaLII (Southern African Institute for Policy and Research, on the Laws.Africa Peachjam platform) | <https://zambialii.org> | 2026-10-28 | 139 | CC BY-NC 4.0, crediting ZambiaLII as the source (https://zambialii.org/terms-of-use/) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | None | Archived copies of ZambiaLII pages; the content licence is ZambiaLII's |

Every response is cached by the sha256 of its URL, and the table above lists every source with its retrieval date. Lexifina keeps its fetch scripts privately; `tools/parse.py` reads only the cache and writes `corpus.json`, so the same cache always gives the same corpus.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | Constitution of Zambia Act, 1991 | 4 | 1996-12-31 to 2025-12-18 |
| `data-protection` | Data Protection Act, 2021 | 1 | 2021-04-01 to 2021-04-01 |
| `lands` | Lands Act | 3 | 1996-12-31 to 2016-01-01 |
| `anti-terrorism` | Anti-Terrorism and Non-Proliferation Act, 2018 | 3 | 2018-07-31 to 2024-12-26 |

The build made 11 commits:

| Commits | Kind |
| ---: | --- |
| 4 | first version of an act |
| 7 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-28.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 9 laws in the record.
- 20 tags.

## Dates

Each commit is dated at noon (Africa/Lusaka) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Not applied: every version is dated by ZambiaLII's own expression date, the day the amendment it incorporates took effect as Laws.Africa records it. No date is computed from a default rule. https://zambialii.org/legislation/

## Commands, in order

```sh
# fill the cache from the sources listed above (network; Lexifina's fetch scripts are kept privately)
python -X utf8 tools/parse.py                  # cache -> corpus.json (no network)
python -X utf8 tools/build.py <folder> --repo <empty folder> --docs-date 2026-10-28
python -X utf8 tools/check_repo.py <repo> --corpus <folder>/corpus.json --write
python -X utf8 tools/build.py <folder> --repo <another empty folder> --docs-date 2026-10-28 --compare <repo>
```

In the main Lexifina repository these files live as follows:
- `fetch.py`, `parse.py` and `repo/`: in `scripts/zambia-law/`.
- `build.py`, `check_repo.py` (`check.py` there) and `on.py`: in `scripts/gitlaw_common/`, with the corpus format in `SCHEMA.md`.

## Exact inputs

- `corpus.json` sha256 `c94fa89bb462cc6e1d50508b18e2b4e61b3bb89835f2b80cc8c397bb8a01a917` (911223 bytes)
- Script blob hashes (`git hash-object`):

| Script | Blob |
| --- | --- |
| build.py | `833a2433a3ea96fd87477ccc7a2ed47dc9e24b48` |
| check.py | `426d4cfb32ce103715be6a00865c0a7bca81a56a` |
| on.py | `644a6c0857fbcc72562032b58d57aa113fee0641` |
| fetch.py | `4444da8fb9c061f021433b6609f64a92a2b27b5b` |
| parse.py | `eeddcd8b8a0fa748b83d383755eef0da051b280e` |

- Tools:
  - Python 3.14.0
  - git version 2.52.0.windows.1
  - curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP

## Checks

Not yet run for this build.

A second build from the same corpus into an empty folder gave identical hashes for all 11 history commits and 20 tags (history tip `3b0f44b2192f7ad10c9f16d806160a73604dd98f`).

These results are from the check run on the build before this one, from the same corpus.

## Decisions made by hand

- Acts were chosen by what the archived source supports: every expression ZambiaLII lists for the Constitution (4), the Data Protection Act 2021 (1), the Lands Act (3) and the Anti-Terrorism and Non-Proliferation Act 2018 (3) has an Internet Archive copy, so each version is read from its own dated expression.
- The Penal Code (Cap. 87) was not taken: ZambiaLII lists 11 expressions (1996 to 2023), but the Internet Archive holds only 2 (1996-12-31 and 2023-12-26), so nine amending Acts from 2000 to 2023 could only be dated 2023-12-26. It also lists the Penal Code (Amendment) Act 2026 (Act 75 of 2026) as an amendment not yet applied.
- The Companies Act 2017 and the Employment Code Act 2019 were not taken: their archived ZambiaLII pages carry no Akoma Ntoso text (the LII shows only the source PDF), and no OCR is used.
- The Insurance Premium Levy Act 2015 was tried and dropped: 2 of its 5 expressions (2018-01-01, 2022-01-01) have no usable archived copy, so two Acts' changes could only be dated a year late.
- In the Constitution of Zambia Act, the Constitution itself is the Schedule (att_1); its articles are filed as art-NNN beside the Act's own sections (sec-NNN).
- Version dates are ZambiaLII's expression dates. Laws.Africa's terminology guide (https://docs.laws.africa/getting-started/terminology-guide) says "Amendments to Principal works come into force on the Commencement date of the Amending work" and that the first point in time is "the work as originally published"; so an amendment's expression is dated by its commencement (in force), and an act's original expression by its publication, which is replaced by the commencement date the page states.
- Credits: a version whose History names exactly one amending law (and no consolidation) between it and the previous version is credited to that law for every provision that changed. Otherwise a provision is credited only to laws that ZambiaLII's editorial note inside that provision links to; the rest are unexplained (publisher).
- Editorial notes (akn-remark) are left out of the text and used only as credit evidence, except where a provision has no other text (repealed or spent), where the note is the provision's whole printed content.
- Part, Chapter and Division headings are left out; each provision file starts with its own number and heading. Every other text of each version is in a provision file: parse.py checks this per version (verification.json, fidelity).
- DPA 2021: the first version is dated 2021-04-01, the commencement date ZambiaLII states ("Commenced on 1 April 2021 by Data Protection Act (Commencement) Order, 2021"), not 2021-03-24, the date of its expression (Gazette publication).

## What AI did and did not do

The fetch, parse and check scripts were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above, through code that anyone can rerun.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the adapter and configuration and chose the acts. No model wrote, summarised or transformed legal text: parse.py is deterministic code.
