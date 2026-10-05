# MTE Study Hub: behaviour and content spec

## Goal
Test whether a small, accessible, intent-first learning hub helps trainees find material faster, understand it more clearly,
feel more confident studying alone, and rely less on trainers for simple clarifications.
Persona: Lena Hofmann, 29, Hamburg, MTE candidate in month 2, lost most of her sight; uses a screen reader.

## Study path (sidebar order and Back/Next logic)
1 Home → 2 Glossary (search → lymph node entry) → 3 Learning modules (Lymph nodes) → 4 Procedures (breast examination steps, then guide) → 5 Practice → 6 Certification prep → 7 Task summary.
Back/Next buttons always move one step along this path. Certification prep is also the "choose what to study next" hub: each topic opens its page.

## Screens
| File | Title | What it does |
|---|---|---|
| Main | What would you like to do? | Five equal cards (glossary, procedure, certification, practice, continue where you left off). One click opens the page. Shows today's progress and the practical-training reminder card if one is set. |
| Glossary | Find a term quickly | Live search over 6 terms (lymph node, palpation, tissue, anatomy, axilla, lesion). Only "lymph node" has an entry; the others show "Not available". Each result: word, pronunciation, short meaning. |
| LymphNode | lymph node | Listen / Slowly buttons, plain-language meaning, why it matters, "I still need help" (simpler explanation), "Where to go next" links, "Could you explain this in your own words?" (Yes / Almost / Not yet), quick check (easy to understand? yes/no, what felt unclear?) with typed text and a voice-note recorder. |
| LymphModule | Lymph nodes | Four sections of text. Highlighted words (lymph node, axilla, palpation, lesion) open a "Word help" panel beside the text with meaning, simpler version, pronunciation + Listen, and a jump link. Focus moves into the panel and back to the word on close. |
| Procedure | Breast examination: the steps | Two steps. Step 1 (palpate breast tissue in a set pattern) can be expanded and picked ("I would review this first"); picking it shows the practical-training reminder (time picker + Set reminder). Step 2 is "Available soon" and disabled. |
| ProcedureGuide | Understanding step 1 | What you do / What to notice / Common slips, plus "Words to know" links to the glossary. |
| Certification | What will you study next? | Four topic cards. Completed topics show a tick and "Done" and are no longer links. When all four are done, a message and a "Go to task summary" button appear. |
| Practice | Practice question | One multiple-choice question ("Which medical word means the armpit?"). Check my answer shows feedback and a suggested review link; hint available. |
| Summary | Your task summary | Tasks completed list (ticked / open), progress bar, "Start a new session". |

## Shared interface (identical in every screen)
- Sidebar: logo (banner), Main navigation with 7 links (title + short description), "Today's progress" region with progress bar.
- Settings bar (region): language button (English ⇄ Deutsch), Text size toggle, High contrast toggle (= dark mode).
- Page navigation bar at the bottom of each page (Back / Continue, or Skip to task summary).
- Skip link "Skip to main content" is the first Tab stop.

## Saved state (browser only)
Key `mte-a11y` in localStorage (copied to a cookie and window.name as fallbacks), JSON:
`{ big: boolean, hc: boolean, lang: "en"|"de", done: string[], reminder: { time: "HH:MM", day: "<Date.toDateString()>" } | null, ts: number }`
- `done` holds task ids: lookup, clarify, procedure, certification, practice. It resets after 3 hours without activity or with "Start a new session".
- `reminder` is only valid on the day it was set.
- A 400 ms poll keeps open pages in sync with storage.
Progress rules: lookup = opened the lymph node entry; clarify = opened a highlighted word; procedure = picked step 1; certification = clicked a topic; practice = pressed Check my answer with an answer chosen.

## Language
English and German. German uses "Sie". Names: Untersuchungsablauf (procedure), Prüfungsvorbereitung (certification prep), Aufgabenübersicht (task summary). Glossary search matches German words too (e.g. "achsel").

## Colours
Light: page #FFFFFF, text #000000, secondary #333333, borders #000000 (1px frames, 2px cards, 3px selected), accent #1D4ED8, focus #2563EB, disabled #6B6B6B dashed. Selected = black fill, white text.
Dark: page #000000, text #FFFFFF, secondary #CCCCCC, borders #FFFFFF, accent #2563EB, disabled #9A9A9A dashed. Selected = white fill, black text.
Font: Inter (self-hosted, `site/fonts`). Base 16px (19px with Text size on).

## Audio
Pronunciation uses the browser's speech engine with ONE voice per language, chosen the same way every time, real words (not respellings), rate 0.85 normal / 0.55 slow, pitch 1. Voice notes use the microphone (MediaRecorder); recordings are kept only in the open page; if the microphone is blocked a message says so.

## Accessibility requirements (all verified in the prototype)
- axe-core: 0 findings across all screens and states, light + dark, English + German, with large text.
- Contrast: every text item passes 4.5:1 (lowest 5.2:1); focus ring ≥ 4.1:1; borders ≥ 3:1.
- Keyboard: every control reachable, visible focus, skip link works, completed/unavailable items are not tab stops.
- Screen reader outline per page: banner → Main navigation → Today's progress → Settings → main (named by the h1, described by the intro text) → regions per card → Page navigation.
- Names + descriptions: nav links (title + subtitle), cards (title + text + "Opens …"), toggles (what they do), word-help buttons, record / delete, reminder buttons.
- Reflow: no sideways scrolling from 1440px down to 320px, in both languages and with large text.

## Out of scope in this prototype
Accounts, real notifications, saving data to a server, recorded audio files, more glossary entries, procedure steps 2–7, certification content beyond the four topics.
