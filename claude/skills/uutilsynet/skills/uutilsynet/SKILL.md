---
name: uutilsynet
description: WCAG/Uutilsynet accessibility checklist reference. Do not apply this automatically — it backs the user-invoked /uutilsynet command. Only load it when the user explicitly runs /uutilsynet or explicitly asks to check something against the Uutilsynet/WCAG requirements.
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

## What's in this skill

- `references/uutilsynet/` — all 48 WCAG requirements Uutilsynet tests
  against, plus a `README.md` explaining the file format and sourcing
