---
name: uutilsynet
description: WCAG/Uutilsynet accessibility checklist reference. Do not apply this automatically — the user invokes it with /uutilsynet. Only load it when the user explicitly runs /uutilsynet or explicitly asks to check something against the Uutilsynet/WCAG requirements.
metadata:
 trigger: User explicitly runs /uutilsynet, or explicitly names Uutilsynet/WCAG requirements by name
 author: Tomi Nurmi / ElBits
---

# Uutilsynet — WCAG/Uutilsynet checklist

A standalone accessibility checklist: the 48 WCAG success criteria that
Uutilsynet (Tilsynet for universell utforming av IKT) tests Norwegian
websites and apps against. Self-contained — every requirement file lives
in this skill's `references/uutilsynet/` folder. It does not depend on
any particular design system, component library, or codebase.

## How to use this skill

[`references/uutilsynet/`](references/uutilsynet/) holds one `.md` file
per requirement (`01-1.1.1-....md` through `48-4.1.3-....md`), each with
the requirement text, test rules ("Hva er kravet?" / "Hva bør jeg
teste?"), solution guidance ("Løsningsforslag"), and frontmatter with a
`kilde` (source URL on uutilsynet.no) and `sist_oppdatert` (last-updated
date).

By default, fetch each requirement live from its `kilde` URL rather than
relying solely on the local copy — uutilsynet.no can update its
guidance. If a `kilde` URL is unreachable, fall back to that
requirement's local `.md` file and tell the user the live page didn't
load, that the locally saved text was used instead, and that file's
`sist_oppdatert` date.

This isn't meant to be checked on every small change. It's most useful
as a periodic control check — e.g. once a screen or flow is functionally
done, or before a release — where you walk the finished result against
each requirement file and flag anything that isn't met. Treat the folder
as a checklist/validator, not a step in every single edit.

## Audit procedure

For the finished screen or flow the user has in mind (ask which one if
not obvious from context):

1. Read each local `references/uutilsynet/*.md` file to get its
   `krav_id`, `kilde` URL, and `sist_oppdatert` date. The overview of
   all 48 is https://www.uutilsynet.no/veiledning/losningsforslag-krav/1366.
2. For each requirement, try fetching its `kilde` URL live. If it loads,
   use that live content as the source of truth for the requirement text,
   test rules, and solution guidance.
3. If a `kilde` URL fails to load (network error, timeout, 404, or the
   page structure is unreadable), fall back to that requirement's local
   `.md` file content instead, and record it as a fallback (requirement
   number + its `sist_oppdatert` date).
4. Check whether the current implementation meets each requirement,
   using the requirement's "Hva er kravet?" / "Hva bør jeg teste?" test
   rules (live or local, per step 2/3).
5. Report back only the requirements that are NOT met (or are unclear),
   each with: the requirement number/title, what's wrong, and the
   relevant "Løsningsforslag" guidance for fixing it.
6. If everything passes, say so plainly rather than listing all 48 as OK.
7. **Always end with a source-fallback note**, even when nothing failed:
   - If every `kilde` URL was reachable: say so briefly (e.g. "All 48
     requirements were checked against uutilsynet.no live.").
   - If any failed: say uutilsynet.no was unreachable for those specific
     requirements, that the locally saved text was used instead, and list
     each one's `sist_oppdatert` date, e.g. "Uutilsynet.no's page for
     1.4.3 Kontrast (minimum) didn't load, so I used the locally saved
     copy instead (last updated 2026-09-25)."

## What's in this skill

- `references/uutilsynet/` — all 48 WCAG requirements Uutilsynet tests
  against, plus a `README.md` explaining the file format and sourcing
