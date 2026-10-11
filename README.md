# Changelog — the free self-hosted "What's new" tool

[![MIT License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/docker-ready-blue.svg)](docker-compose.yml)
[![No tracking](https://img.shields.io/badge/tracking-none-brightgreen.svg)](#)

**Your product ships updates. Your users should see them.** A free, self-hosted changelog page + "What's new" widget + email digests — the open-source alternative to Beamer ($49–119/mo).

One command, your own server, your data. No subscriptions, no per-viewer pricing, no tracking pixels phoning home.

![The public changelog page](screenshots/changelog-page.png)

---

## The problem

Beamer charges **$49–119/month** for a changelog widget. LaunchNotes charges $29/user/month. That's rent on your own product updates.

A changelog is a solved problem: a list of dated entries, a widget, an RSS feed. It doesn't need a SaaS.

## The solution

This project exists so indie hackers never pay a monthly tax for telling their users what's new. **Free forever for self-hosting** — MIT licensed, SQLite, one Docker container.

---

## Features

- 📝 **Beautiful changelog page** — clean, fast, mobile-friendly. Version tags, dates, markdown entries, tag filters.
- 🔔 **"What's new" widget** — one `<script>` tag adds a notification bell with an unread badge to your site. No third parties, no cookies.

![The "What's new" widget embedded on a site](screenshots/widget.png)

- 📧 **Email digests** — collect subscribers, send a styled digest when you ship (bring your own SMTP).
- 📡 **RSS feed** — automatic, at `/feed.xml`.
- 🐙 **GitHub import** — point it at any public repo, get changelog entries from its releases in one click.
- 🔒 **Password-protected admin** — manage entries, subscribers, and branding from `/admin`.
- 🎨 **Branding controls** — product name, accent color, widget position, all in Settings.

| | This project | Beamer |
|---|---|---|
| Changelog page | ✅ | ✅ |
| "What's new" widget | ✅ | ✅ |
| Email digests | ✅ (own SMTP) | ✅ |
| RSS feed | ✅ | ❌ |
| GitHub release import | ✅ | ❌ |
| Self-hosted | ✅ | ❌ |
| Price | **$0** | $49–119/mo |

---

## Quickstart

```bash
git clone https://github.com/gursidhu528-lang/changelog.git && cd changelog
cp .env.example .env        # set ADMIN_PASSWORD
docker compose up -d        # done. open http://localhost:3000
```

Then:
1. Open `http://localhost:3000/admin`, sign in with your `ADMIN_PASSWORD`.
2. Run `npm run seed` (or `docker compose exec changelog node seed.js`) for demo data — or click **Import** and pull releases from your GitHub repo.
3. Paste the widget snippet (shown in **Settings**) onto your site:

```html
<script src="https://YOUR-DOMAIN/widget.js" async></script>
```

Optional overrides: `data-position="bottom-left"`, `data-accent="#2563eb"`. The widget fetches from your own domain — no third parties, no cookies, fails silently if your server is down (it never breaks your page).

### Without Docker

```bash
npm install
cp .env.example .env        # set ADMIN_PASSWORD
npm run seed                # optional demo data
npm run build && npm start  # http://localhost:3000
```

## Configuration

All via environment variables (see `.env.example`):

| Variable | Required | What |
|---|---|---|
| `ADMIN_PASSWORD` | ✅ | Password for `/admin` |
| `DATA_DIR` | — | SQLite location (default `./data`; `/data` in Docker) |
| `GITHUB_TOKEN` | — | Raises GitHub import rate limit (60 → 5,000/hr) |
| `SMTP_HOST/PORT/USER/PASS/FROM` | — | Enables one-click digest sending |
| `NEXT_PUBLIC_SITE_URL` | — | Canonical URL for RSS (auto-detected otherwise) |

## Roadmap

- [ ] Multi-user admin (currently single password)
- [ ] Scheduled digest sending (currently manual)
- [ ] Webhooks on new publish (Discord/Slack)
- [ ] Scheduled GitHub re-imports
- [ ] Hosted cloud option (separate, paid — core stays free)

## Contributing

PRs welcome. Keep it dependency-light, keep the UI clean, keep it boring in the best way. See open issues for the roadmap.

## License

MIT — do whatever you want. If it saves you $49/month, consider starring the repo.
