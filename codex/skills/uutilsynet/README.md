# Uutilsynet — WCAG/Uutilsynet checklist

A standalone WCAG/Uutilsynet accessibility checklist, packaged as a
Claude Code plugin. Independent of the `elbriks` design system plugin —
install this on its own to run accessibility audits against any
Norwegian website or app.

User-invoked only: run `/uutilsynet` to trigger an audit — it never
runs automatically in the background.

## What it checks

From [uutilsynet.no](https://www.uutilsynet.no/veiledning/losningsforslag-krav/1366):

> Kravene i regelverket gjelder for nettløsninger. Nettløsninger omfatter
> både nettsteder og mange apper til nettbrett og mobil. Kravene er deler
> av standarden Web Content Accessibility Guidelines (WCAG), som uutilsynet har
> delt opp i både prinsipp og tema for å gjøre det lettere å
> finne ut hva man skal gjøre for å oppfylle kravene. Uutilsynet har også laget
> løsningsforslag med eksempler knyttet til de ulike temaene og for hvert
> krav i WCAG-standarden.

This plugin follows uutilsynet.no's "løsningsforslag for å møte hvert av
de 48 kravene i WCAG-standarden."

- [`commands/uutilsynet.md`](commands/uutilsynet.md) — the
  `/uutilsynet` slash command (`disable-model-invocation: true`, so
  Claude can only run it when the user explicitly types the command).
- [`skills/uutilsynet/`](skills/uutilsynet/) — the reference the
  command uses: `SKILL.md`, plus its `references/uutilsynet/` (the 48
  WCAG requirement files sourced from uutilsynet.no).
