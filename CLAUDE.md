# MTE Study Hub (prototype)

A static, no-build prototype of an accessible learning hub for Medical Tactile Examiner (MTE/MTU) trainees.
Primary user: Lena, a trainee who lost most of her sight and works with a screen reader. Every decision serves her first.

Read `docs/SPEC.md` for how every screen behaves and `docs/screens/` for how each one must look.

## Layout of this folder
- repo root          the working website, deployed with GitHub Pages
  - `index.html`     redirects to `Main.dc.html`
  - `*.dc.html`      one file per screen: Main (Home), Glossary, LymphNode, LymphModule, Procedure, ProcedureGuide, Certification, Practice, Summary
  - `support.js`     the page runtime every `.dc.html` loads. Do not edit or delete it.
  - `fonts/`         self-hosted Inter font + `inter.css`. Keep it: no third-party requests allowed.
- `docs/SPEC.md`     behaviour, content, state and accessibility spec
- `docs/screens/`    reference screenshots (light, dark, German, and key states)
- `START-HERE.md`    install steps and ready-to-paste prompts

## Run locally
    npx serve .           # or: python3 -m http.server 8000
Do not open the files with file:// (saved settings and the microphone need http).

## How each screen file is built
`<style>` block, then the page markup inside `<x-dc>` **twice** (English inside `<sc-if value="{{isEn}}">`, German inside `<sc-if value="{{isDe}}">`),
then a script with `class Component extends DCLogic`. Change both languages together. Text between `{{ }}` is a live value from the script.

## Non-negotiable rules
- Keep WCAG 2.2 AA at minimum: text contrast 4.5:1, borders / focus rings 3:1, visible focus on every control, 44px touch targets, no sideways scrolling down to 320px (also in German with large text).
- Screen readers: landmarks (banner, Main navigation, progress region, settings region, main, Page navigation), one h1, headings in order, each control has a short name plus a hidden description (`aria-describedby` to a `.sr` span), unavailable items read as "not available" and are not focusable.
- Pronunciation text is always marked as pronunciation ("pronounced …", "Sounds like …") and kept apart from the word itself.
- One voice per language for all spoken words (see `pickVoice` / `speakWord` in `LymphNode.dc.html` and `LymphModule.dc.html`).
- Colours (from the registration design): light = white page, black text and borders, blue #1D4ED8; dark = black page, white text and borders, blue #2563EB; focus ring blue 3px.
- No tracking, analytics, CDNs or requests to other domains. Everything stays in the visitor's browser.

## Not real yet, so never present as real
- The practical-training reminder only shows a card on Home; it sends no notification.
- Voice notes live only in the open page. Pronunciation uses the browser's own voice.
- Only the "lymph node" glossary entry and procedure step 1 exist. German text was written by Claude and still needs a native-speaker review.

## Check your work
Run an axe-core scan on every screen in light, dark, English and German; test with keyboard only (Tab, Enter, Esc); confirm the skip link works.
