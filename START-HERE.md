# Start here: using this pack with Claude Code

## 1. Install Claude Code (from the official quickstart: https://code.claude.com/docs/en/quickstart)
- macOS / Linux:  `curl -fsSL https://claude.ai/install.sh | bash`
- Windows PowerShell:  `irm https://claude.ai/install.ps1 | iex`
- or  `brew install --cask claude-code`  /  `winget install Anthropic.ClaudeCode`
You need a Claude account (Pro, Max, Team or Enterprise) or an Anthropic Console account.

## 2. Open this folder in a terminal and start it
    cd mte-study-hub-claude-code
    claude
Claude Code reads `CLAUDE.md` automatically. It asks your permission before it edits files or runs commands.

## 3. Paste ONE of these prompts

### A. Put it online
> Read CLAUDE.md. Deploy the `site/` folder as a static site. Use Netlify (`npx netlify-cli deploy --prod --dir site`) and walk me through the login. Then open the live link and check: Home, Glossary, Lymph node entry, Module, Procedure, Certification, Practice and Summary all load; the English/Deutsch button works; High contrast works; there are no requests to other domains.

(Other hosts: replace the first sentence with "Deploy it to Vercel with `npx vercel --prod`" or "Create a GitHub repository with the gh CLI, push it, and turn on GitHub Pages". The site needs https.)

### B. Keep improving the prototype
> Read CLAUDE.md and docs/SPEC.md. I want to change: [describe]. Edit the screens in `site/`, keep English and German in step, keep all accessibility rules, serve the site, and run an axe-core accessibility scan on every screen in light, dark, English and German before you tell me it is done.

### C. Rebuild it as a real app
> Read CLAUDE.md, docs/SPEC.md and look at every image in docs/screens/. Rebuild this prototype as a production app with Next.js (App Router), TypeScript and Tailwind CSS, with a shared layout (sidebar, settings bar, Page navigation) and a content layer for English and German. Match the screens pixel-for-pixel, keep every accessibility behaviour in SPEC.md, store session data behind one small interface so a back end can replace localStorage later, and add automated tests (axe + keyboard) to CI.

### D. Move it into Claude Design (experimental)
Connect once:  `claude mcp add --scope user --transport http claude-design https://api.anthropic.com/v1/design/mcp`
Then in Claude Code:
> Use /design to export the `site/` prototype to Claude Design as a live prototype, using the screenshots in docs/screens/ as the reference.
Docs: https://support.claude.com/en/articles/14604416-get-started-with-claude-design
(This creates a separate copy in Claude Design. The editable original stays at https://claude.ai/artifact/25dpwErf7SZ45YLRAw8icM)

## Before real trainees use it
- Test with a screen reader and ideally with Lena (NVDA/JAWS on Windows, VoiceOver on Mac/iPhone).
- Have a native speaker read the German text; have a trainer check the medical wording.
- Decide where reminders, progress and voice notes should be stored. Today they stay in the browser only.
