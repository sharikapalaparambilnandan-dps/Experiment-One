# Experiment One – MTE Study Hub (prototype)

A static, no-build prototype of an accessible learning hub for Medical Tactile Examiner (MTE/MTU) trainees, designed with screen-reader users in mind. Exported from Claude Design.

## Live site

https://sharikapalaparambilnandan-dps.github.io/Experiment-One/

## Run locally

    npx serve .           # or: python3 -m http.server 8000

Serve over http; don't open the files with `file://` (saved settings and the microphone need http).

## Structure

- Repo root – the website, served by GitHub Pages. `index.html` redirects to `Main.dc.html`; one `*.dc.html` file per screen; `support.js` is the page runtime; `fonts/` holds self-hosted Inter.
- `docs/SPEC.md` – behaviour, content, state and accessibility spec.
- `docs/screens/` – reference screenshots (light, dark, English, German).
- `CLAUDE.md` / `START-HERE.md` – guidance for working on the project with Claude Code.

## Notes

- Everything stays in the visitor's browser; there is no tracking and there are no third-party requests.
- Prototype limits: reminders send no notifications, voice notes live only in the open page, and only the "lymph node" glossary entry and procedure step 1 exist. German text still needs a native-speaker review.
