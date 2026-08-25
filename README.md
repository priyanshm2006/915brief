# Nine Fifteen — site

Five static pages, no build step, no framework. This is the whole website.

| File | What it is |
|---|---|
| `index.html` | Homepage — the pitch page: what this is, a sample, email signup |
| `today.html` | Always the latest edition (overwritten each publish) |
| `2026-08-19-am.html` | Today's dated permalink — stays forever, never overwritten |
| `archive.html` | List of every past edition |
| `privacy.html` | The privacy notice linked from the subscribe form's consent checkbox |

The subscribe form calls our own subscriber API — see `/backend` in this repo — rather than a
third-party ESP embed. Until that API is deployed, the form falls back to just sending people to
`today.html` so you can see the flow work end to end. Once you've deployed the Worker (backend
README walks through it, ~15 minutes), paste its URL into `NF_WORKER_URL` near the bottom of
`index.html` and the form goes fully live — subscribing for real, into a database you control.

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

## Clean URLs

Every internal link on the site points to `/today`, `/archive`, `/privacy`, `/2026-08-19-am` and
so on — no `.html` showing in the address bar, same as most real sites. This works automatically
on GitHub Pages: it silently serves `today.html` when someone requests `/today`, no configuration
needed. The files on disk still keep their `.html` names (that's required — GitHub Pages needs
the real filename to serve), so when the daily brief writes a new dated file, keep naming it
`2026-08-20-am.html` etc. as usual, and just link to it as `/2026-08-20-am` everywhere it's
referenced (archive list, "browse past editions", etc.). Old links with `.html` still work too —
nothing that's already been shared or bookmarked breaks.

## Email signup

The subscribe form (on `index.html`) is real and posts to your own subscriber API — see
`/backend` for what that is and how to deploy it. Until you deploy it, the form falls back to a
harmless test flow (click through to today's brief) so the site never looks broken. Once
deployed, one line (`NF_WORKER_URL` at the bottom of `index.html`) turns it on.
