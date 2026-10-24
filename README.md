# Campus Bestie

A Cubbie Skill that searches all of ASU from one iMessage. Classes with live seat counts, campus events, faculty directory, and university news.

Built for [Cubbie Hackathon 2026](https://hackathon.cubbie.ai/) — Track 1.

## What it does

Text Cubbie a question about ASU and get an instant answer:

- **Classes** — "Any seats open in CSE 310?" → live seat counts, sections, times, locations
- **Faculty** — "Prof Berisha's email?" → name, title, department, email, profile link
- **Events** — "What's happening on campus?" → upcoming events with dates and locations
- **News** — "Latest ASU news" → recent stories with summaries

All data is public.

## Files

```
SKILL.md              — Cubbie reads this to know when and how to use the skill
scripts/asu_search.py — Pure stdlib Python script that queries ASU public APIs
```

## Try it

Text Cubbie this repo's GitHub link to install, then ask about ASU.

## Local testing

```bash
python3 scripts/asu_search.py classes --subject CSE --number 310
python3 scripts/asu_search.py people --query "machine learning"
python3 scripts/asu_search.py events
python3 scripts/asu_search.py news --keywords "research"
```

## How it works

The script hits four public ASU endpoints (no auth required — the class API literally accepts `Authorization: Bearer null`):

| Data | Source |
|------|--------|
| Classes | ASU Course Catalog API |
| People | ASU Web Directory API |
| Events | asuevents.asu.edu (HTML) |
| News | news.asu.edu (HTML) |

Cubbie runs the script in its sandbox and formats the JSON response as a plain-text iMessage reply.
