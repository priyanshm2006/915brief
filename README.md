# Nine Fifteen — site

Four static pages, no build step, no framework. This is the whole website.

| File | What it is |
|---|---|
| `index.html` | Homepage — the pitch page: what this is, a sample, email signup |
| `today.html` | Always the latest edition (overwritten each publish) |
| `2026-08-19-am.html` | Today's dated permalink — stays forever, never overwritten |
| `archive.html` | List of every past edition |

The "Subscribe free" button on the homepage currently just sends people to `today.html` so you can click through and see the flow work. Once you connect beehiiv or Substack, swap in their embed and turn on its "redirect after subscribe" setting pointed at `/today.html` — the button keeps doing the same thing, except now it actually subscribes them first.

## One-time setup (you do this — about 20 minutes total)

1. **Buy a domain.** Namecheap or GoDaddy, `.in` or `.com`. See name suggestions in chat.
2. **Create a free GitHub account** at github.com if you don't have one.
3. **Create a new repository** — public, name it anything (e.g. `nine-fifteen-site`). Upload these four files to it (drag-and-drop on github.com works, no command line needed).
4. **Turn on GitHub Pages** — in the repo, go to Settings → Pages → set source to the `main` branch → Save. GitHub gives you a `yourname.github.io/repo` URL immediately; this proves it's live.
5. **Point your domain at it** — in the repo's Pages settings, enter your custom domain. Then at your domain registrar, add the DNS records GitHub's Pages docs specify (a `CNAME` record for a subdomain like `www`, or `A` records for the root domain — GitHub's Pages settings page shows you exactly which once you type in your domain). Takes a few minutes to a few hours to propagate.
6. **Come back and tell me the repo URL.** I'll wire the daily scheduled briefs to publish straight into it automatically, so you never touch this again.

## What happens after step 6

Each morning and afternoon, the scheduled brief:
1. Writes a new dated file (`2026-08-20-am.html`, etc.)
2. Overwrites `index.html` with that file's content, so the homepage always shows the latest
3. Adds a line to `archive.html`
4. Commits and pushes — GitHub Pages redeploys automatically within about a minute

You'll still get the file sent to you in chat first to skim, exactly like today. If a number's wrong, tell me and I fix it and republish — nothing is locked once it's live.

## Email signup

The "Subscribe" button on `about.html` is a placeholder form right now. Once you've created a beehiiv or Substack account, replace the `<form>...</form>` block in `about.html` with the embed code they give you — that's a one-paragraph copy-paste, I can do it the moment you have it.
