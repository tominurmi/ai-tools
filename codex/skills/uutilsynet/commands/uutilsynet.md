---
description: Run a WCAG/Uutilsynet accessibility audit against the current screen or flow
disable-model-invocation: true
---

Run a periodic accessibility control check using the Uutilsynet/WCAG
checklist. There are two sources for each of the 48 requirements:

- **Live (default):** the requirement's own page on uutilsynet.no, at
  the `kilde` URL in that requirement's local file's frontmatter (the
  overview of all 48 is
  https://www.uutilsynet.no/veiledning/losningsforslag-krav/1366).
- **Local fallback:** the bundled copy in
  `skills/uutilsynet/references/uutilsynet/` — 48 `.md` files, one per
  requirement, each with `kilde` (source URL) and `sist_oppdatert`
  (last-updated date) in its frontmatter.

For the finished screen or flow the user has in mind (ask which one if
not obvious from context):

1. First read each local `references/uutilsynet/*.md` file to get its
   `krav_id`, `kilde` URL, and `sist_oppdatert` date.
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

Do not treat this as a step to repeat on every small edit — it's a
release/pre-release gate the user is asking for explicitly right now.
