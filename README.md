# User Manual Kit

A starter template for building your personal "Working with Me" page using Claude Code. Fork it, fill it in with AI, deploy to GitHub Pages.

## What is this?

A single-page website that tells your teammates how to work with you — your communication style, values, schedule, personality quirks, and more. Claude Code helps you fill it in by reading your Slack profile and asking you questions.

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- A GitHub account (for deployment)
- A Slack workspace you belong to (for auto-populating your profile)

## Getting Started

### 1. Fork this repo

Click **Fork** on GitHub to create your own copy.

### 2. Clone and open in Claude Code

```bash
git clone https://github.com/YOUR_USERNAME/user-manual-kit.git
cd user-manual-kit
claude
```

### 3. Install plugins

Inside Claude Code, install the following plugins:

#### Slack (required)

Pulls your name, title, timezone, and messages to populate the template.

```
/plugin install slack@claude-plugins-official
```

After installing, you'll be prompted to authenticate via your browser. Sign in to your Slack workspace and authorize access.

#### Figma (optional)

If you want to customize the design using Figma.

```
/plugin install figma@claude-plugins-official
```

After installing, you'll be prompted to authenticate via your browser. Sign in to your Figma account and authorize access.

#### GitHub CLI (required for deployment)

The `gh` CLI is used to push your site and manage GitHub Pages. Install it on your system:

```bash
# macOS
brew install gh

# Linux
sudo apt install gh

# Windows
winget install GitHub.cli
```

Then authenticate:

```bash
gh auth login
```

Follow the browser flow to sign in to your GitHub account.

### 4. Fill in your manual

Once plugins are installed, copy and paste the following prompt into Claude Code:

```
You are building a personal user manual for me.

First, read my Slack profile to get my name, title, and timezone. Then read
the current index.html and designs/editorial.md in this repo to understand the
template structure, design philosophy, sections, and placeholder content.

Step 1 — Research
Use the Slack MCP to gather information about me. Specifically:
- Search for messages from me across public channels (look at at least 50–100 messages)
- Look at threads I've participated in — what topics do I engage with deeply?
- Check recent activity: what channels am I active in? What am I working on?
- Note recurring phrases, words, or emoji I use
- Identify projects, initiatives, or topics I mention frequently
- Look for how I give feedback — tone, directness, format
- Note how I communicate asynchronously vs. synchronously
- Look for values or principles I seem to care about based on what I write
- Collect raw notes. Don't synthesize yet.

Step 2 — Synthesize
From your research, infer and draft content for the following sections:
- Who I am — short punchy bio/intro in first person
- My traits — 4–6 personality/work traits with evidence from messages
- How I communicate — async vs sync preferences, response style, tone
- How to work with me well — green flags (what gets a great response from me)
- What slows me down — friction points, anti-patterns
- What I'm working on — current projects and focus areas
- What I care about — recurring themes, values, principles I reference
- My vocabulary — words, phrases, or concepts I use a lot
- Fun facts / quirks — anything interesting, surprising, or delightful

Step 3 — Build the site
Rewrite index.html with the synthesized content. Use the existing index.html as
your structural template and designs/editorial.md as the style guide. Replace all
[bracketed placeholder] text with real content from your research. Preserve the
HTML structure and CSS design system. Make it something I'd actually want to
share with teammates.
```

Claude will read your Slack profile, research your messages, synthesize what it finds, and fill in the template.

### 5. Preview locally

```bash
python3 -m http.server 8000
# Open http://localhost:8000
```

No build step, no dependencies, no npm.

## Deploying to GitHub Pages

### Enable GitHub Pages

1. Go to your repo on GitHub
2. Navigate to **Settings** > **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Set Branch to **main** and folder to **/ (root)**
5. Click **Save**

Your site will be live at `https://YOUR_USERNAME.github.io/user-manual-kit/` within a few minutes.

### Push your changes

Once you're happy with your manual, tell Claude to commit and push:

> "Commit and push my changes"

Or do it manually:

```bash
git add index.html
git commit -m "Fill in my user manual"
git push origin main
```

### Verify deployment

You can check the status of your GitHub Pages deployment with:

```bash
gh api repos/YOUR_USERNAME/user-manual-kit/pages
```

### Custom domain (optional)

If you want to use a custom domain:

1. Go to **Settings** > **Pages** > **Custom domain**
2. Enter your domain (e.g., `manual.yourdomain.com`)
3. Add a CNAME record with your DNS provider pointing to `YOUR_USERNAME.github.io`
4. Wait for DNS propagation and HTTPS provisioning (can take up to 24 hours)

### Troubleshooting Pages

- **404 after enabling Pages?** Make sure the branch is `main` and folder is `/ (root)`. The `index.html` must be at the repo root.
- **Changes not showing up?** GitHub Pages can take 1-2 minutes to rebuild. Check the **Actions** tab for deployment status.
- **Pages option not visible?** Make sure the repo is public, or that you have GitHub Pro/Team (private repo Pages requires a paid plan).

## Switching Styles

The template ships with the **Editorial** style — a warm, light, magazine-inspired design. Two additional styles are available as Figma designs:

- **Monopo** — Dark, bold, typographic (agency-inspired)
- **Lottie** — Clean, playful, teal accents

To apply an alternative style, install the Figma plugin and tell Claude:

> "Restyle my page to match the Monopo design from this Figma: https://www.figma.com/design/AyUuvVdN3dTKaCtaUSSBZ2/Personal-User-Manual-Templates"

Claude will use the Figma MCP to read the design tokens, colors, typography, and layout from the Figma file and rewrite the CSS in your `index.html` to match.

You can also create your own custom designs in Figma and use the same workflow to apply them.

## Customizing

Everything is in one file: `index.html`. No build tools, no dependencies.

- Want to add a section? Ask Claude.
- Want a completely different visual style? Point Claude at a Figma file.
- Want to remove a section? Just delete it from the HTML.
