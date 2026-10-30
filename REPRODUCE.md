# How this repository was made (Zambia)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| ZambiaLII (Southern African Institute for Policy and Research, on the Laws.Africa Peachjam platform) | <https://zambialii.org> | 2026-10-28 | CC BY-NC 4.0, crediting ZambiaLII as the source (https://zambialii.org/terms-of-use/) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | Archived copies of ZambiaLII pages; the content licence is ZambiaLII's |
| ZambiaLII (Southern African Institute for Policy and Research, on the Laws.Africa Peachjam platform) | <https://zambialii.org> | 2026-10-30 | CC BY-NC 4.0, crediting ZambiaLII as the source (https://zambialii.org/terms-of-use/) |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | Constitution of Zambia Act, 1991 | 4 | 1996-12-31 to 2025-12-18 |
| `data-protection` | Data Protection Act, 2021 | 1 | 2021-04-01 to 2021-04-01 |
| `lands` | Lands Act | 3 | 1996-12-31 to 2016-01-01 |
| `anti-terrorism` | Anti-Terrorism and Non-Proliferation Act, 2018 | 3 | 2018-07-31 to 2024-12-26 |
| `marriage` | Marriage Act, 1918 | 2 | 1996-12-31 to 2023-12-26 |
| `public-health` | Public Health Act, 1930 | 2 | 1996-12-31 to 2020-03-06 |
| `local-courts` | Local Courts Act, 1966 | 3 | 1996-12-31 to 2008-09-26 |
| `education` | Education Act, 2011 | 2 | 2011-04-18 to 2026-06-12 |
| `landlord-and-tenant-business-premises` | Landlord and Tenant (Business Premises) Act, 1971 | 2 | 1996-12-31 to 2020-10-26 |
| `rent` | Rent Act, 1972 | 2 | 1996-12-31 to 2018-04-11 |
| `law-association` | Law Association of Zambia Act, 1973 | 2 | 1996-12-31 to 2006-05-19 |
| `small-claims-courts` | Small Claims Courts Act, 1992 | 3 | 1996-12-31 to 2025-12-30 |
| `copyright` | Copyright and Performance Rights Act, 1994 | 2 | 1996-12-31 to 2010-08-16 |
| `money-laundering` | Prohibition and Prevention of Money Laundering Act, 2001 | 2 | 2001-11-09 to 2010-11-29 |
| `matrimonial-causes` | Matrimonial Causes Act, 2007 | 2 | 2007-09-12 to 2024-08-16 |
| `anti-human-trafficking` | Anti-Human Trafficking Act, 2008 | 2 | 2008-09-26 to 2022-11-16 |
| `immigration-and-deportation` | Immigration and Deportation Act, 2010 | 2 | 2010-09-17 to 2016-06-07 |
| `electoral-commission` | Electoral Commission of Zambia Act, 2016 | 2 | 2016-06-07 to 2019-04-11 |
| `public-procurement` | Public Procurement Act, 2020 | 2 | 2021-04-16 to 2023-12-26 |
| `cyber-security-and-cyber-crimes` | Cyber Security and Cyber Crimes Act, 2021 | 1 | 2021-04-01 to 2021-04-01 |
| `electronic-communications` | Electronic Communications and Transactions Act, 2021 | 1 | 2021-04-01 to 2021-04-01 |
| `investment-trade-business` | Investment, Trade and Business Development Act, 2022 | 2 | 2023-01-13 to 2024-04-18 |
| `firearms` | Firearms Act, 1969 | 1 | 1996-12-31 to 1996-12-31 |
| `judgments` | Judgments Act | 2 | 1996-12-31 to 1997-11-14 |
| `fees-and-fines` | Fees and Fines Act, 1994 | 2 | 1996-12-31 to 2013-12-19 |
| `referendum` | Referendum Act, 1967 | 2 | 1996-12-31 to 2015-08-14 |
| `correctional-service` | Zambia Correctional Service Act, 2021 | 1 | 2022-01-21 to 2022-01-21 |

The build made 55 commits:

| Commits | Kind |
| ---: | --- |
| 27 | first version of an act |
| 28 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-30.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 41 laws in the record.
- 96 tags.

## Dates

Each commit is dated at noon (Africa/Lusaka) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Not applied: every version is dated by ZambiaLII's own expression date, the day the amendment it incorporates took effect as Laws.Africa records it. No date is computed from a default rule. https://zambialii.org/legislation/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `d702581f96167c9a814670e57e5b2517bff7804ee26a48aacb825b9eb4627f03` (2841242 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

55 versions of 27 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

A second build from the same corpus into an empty folder gave identical hashes for all 55 history commits and 96 tags (history tip `1998e45ca01fdb46fdf17b9f2f739692643255b9`).

## Decisions made by hand

- Acts were chosen by what the archived source supports: every expression ZambiaLII lists for the Constitution (4), the Data Protection Act 2021 (1), the Lands Act (3) and the Anti-Terrorism and Non-Proliferation Act 2018 (3) has an Internet Archive copy, so each version is read from its own dated expression.
- The Penal Code (Cap. 87) was not taken: ZambiaLII lists 11 expressions (1996 to 2023), but the Internet Archive holds only 2 (1996-12-31 and 2023-12-26), so nine amending Acts from 2000 to 2023 could only be dated 2023-12-26. It also lists the Penal Code (Amendment) Act 2026 (Act 75 of 2026) as an amendment not yet applied.
- The Companies Act 2017 and the Employment Code Act 2019 were not taken: their archived ZambiaLII pages carry no Akoma Ntoso text (the LII shows only the source PDF), and no OCR is used.
- The Insurance Premium Levy Act 2015 was tried and dropped: 2 of its 5 expressions (2018-01-01, 2022-01-01) have no usable archived copy, so two Acts' changes could only be dated a year late.
- In the Constitution of Zambia Act, the Constitution itself is the Schedule (att_1); its articles are filed as art-NNN beside the Act's own sections (sec-NNN).
- Licence: ZambiaLII licenses its content CC BY-NC 4.0 with attribution; CC BY-NC allows only non-commercial use. Every version is read from the Internet Archive's copy, for the configured acts only. No legal text was given to a model.
- Version dates are ZambiaLII's expression dates. Laws.Africa's terminology guide (https://docs.laws.africa/getting-started/terminology-guide) says "Amendments to Principal works come into force on the Commencement date of the Amending work" and that the first point in time is "the work as originally published"; so an amendment's expression is dated by its commencement (in force), and an act's original expression by its publication, which is replaced by the commencement date the page states.
- Credits: a version whose History names exactly one amending law (and no consolidation) between it and the previous version is credited to that law for every provision that changed. Otherwise a provision is credited only to laws that ZambiaLII's editorial note inside that provision links to; the rest are unexplained (publisher).
- Editorial notes (akn-remark) are left out of the text and used only as credit evidence, except where a provision has no other text (repealed or spent), where the note is the provision's whole printed content.
- Part, Chapter and Division headings are left out; each provision file starts with its own number and heading. Every other text of each version is in a provision file: this is checked per version (verification.json, fidelity).
- DPA 2021: the first version is dated 2021-04-01, the commencement date ZambiaLII states ("Commenced on 1 April 2021 by Data Protection Act (Commencement) Order, 2021"), not 2021-03-24, the date of its expression (Gazette publication).
- Batch 2 acts were chosen among the principal national Acts for which every point-in-time version ZambiaLII lists is available: Marriage Act, Public Health Act, Local Courts Act, Education Act, 2011, Landlord and Tenant (Business Premises) Act, Rent Act, Law Association of Zambia Act, Small Claims Courts Act, Copyright and Performance Rights Act, Prohibition and Prevention of Money Laundering Act, 2001, Matrimonial Causes Act, 2007, Anti-Human Trafficking Act, 2008, Immigration and Deportation Act, 2010, Electoral Commission of Zambia Act, 2016, Public Procurement Act, 2020, Cyber Security and Cyber Crimes Act, 2021, Electronic Communications and Transactions Act, 2021, Investment, Trade and Business Development Act, 2022, Firearms Act, Judgments Act, Fees and Fines Act, Referendum Act, Zambia Correctional Service Act, 2021.
- Batch 2 left out, because one or more versions ZambiaLII lists was not available: the Penal Code (9 versions), the High Court Act (2), the Legal Practitioners Act (2), the Investment Act 1993 (1), the Companies Act 1994 (2), the National Pension Scheme Act (6), the Health Professions Act 2009 (1), the Competition and Consumer Protection Act 2010 (2), the Registration of Business Names Act 2011 (1), the Insurance Premium Levy Act (2) and the Judiciary Administration Act 2016 (1). The Companies Act 2017, the Employment Code Act 2019 and the Income Tax Act have no structured text on ZambiaLII (source PDF only), and no OCR is used.
- Many batch 2 histories start with the 1996 Revised Edition of the Laws of Zambia (expression 1996-12-31), the oldest version ZambiaLII publishes for those Acts; that version is the publisher's consolidation, not the Act as enacted.
- The Criminal Procedure Code and the Mines and Minerals Development Act 2015 were left out of batch 2: ZambiaLII's newest available page of the Code says amendments from 1997 to 2023 have not been applied to its text, and the Mines and Minerals Development Act's History lists a change of 2025-06-13 whose version was not available.
- Immigration and Deportation Act: the first version is dated 2010-09-17, the commencement date ZambiaLII states ("Commenced on 17 September 2010 by Immigration and Deportation Act (Commencement) Order, 2010"), not 2010-04-16, the date of its expression (Gazette publication).
- Public Procurement Act: the first version is dated 2021-04-16, the commencement date ZambiaLII states ("Commenced on 16 April 2021 by Public Procurement Act (Commencement) Order, 2021"), not 2020-11-23, the date of its expression (Gazette publication).
- Cyber Security and Cyber Crimes Act: the first version is dated 2021-04-01, the commencement date ZambiaLII states ("Commenced on 1 April 2021 by Cyber Security and Cyber Crimes Act (Commencement) Order, 2021"), not 2021-03-24, the date of its expression (Gazette publication).
- Electronic Communications and Transactions Act: the first version is dated 2021-04-01, the commencement date ZambiaLII states ("Commenced on 1 April 2021 by Electronic Communications and Transactions (Commencement) Order, 2021"), not 2021-03-24, the date of its expression (Gazette publication).
- Investment, Trade and Business Development Act: the first version is dated 2023-01-13, the commencement date ZambiaLII states ("Commenced on 13 January 2023 by Investment, Trade and Business Development Act, (Commencement) Order, 2023"), not 2022-11-16, the date of its expression (Gazette publication).
- Zambia Correctional Service Act: the first version is dated 2022-01-21, the commencement date ZambiaLII states ("Commenced on 21 January 2022 by Zambia Correctional Services Act (Commencement) Order, 2021"), not 2021-05-20, the date of its expression (Gazette publication).

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the adapter and configuration and chose the acts. No model wrote, summarised or transformed legal text: the text is parsed by deterministic code.
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the adapter and configuration and chose the acts. No model wrote, summarised or transformed legal text: Lexifina's code is deterministic code.
