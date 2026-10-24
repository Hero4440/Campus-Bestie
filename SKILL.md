---
name: asu-campus-scout
description: Search ASU classes, campus events, faculty and news from a text. Use when the student asks about ASU class seats, course schedules, professors, campus events or university news.
---

# ASU Campus Scout

One text, every public ASU system: class search with live seat counts, campus events, faculty directory and university news. No sign-in needed — all data is public.

## When to use

- "Any seats open in CSE 310?"
- "Who teaches machine learning at ASU?"
- "What events are happening this week on campus?"
- "Latest ASU news"
- "Find me a MWF class after 10 AM"
- "Tell me about robotics at ASU"
- "What 3-credit CSE classes have open seats?"
- "Prof Yang's email?"

Do not use for Canvas assignments, grades, course files or anything that needs the student's Canvas login — Cubbie handles those directly.

## Setup (first time only)

No packages needed. The script uses only Python standard library.

## Steps

### 1. Figure out what the student wants

Read the student's message and decide which search to run. A single message may need more than one.

| Student is asking about | Run |
| --- | --- |
| A specific course ("CSE 310", "CSE 240") | `scripts/asu_search.py classes --subject <SUBJ> --number <NUM>` |
| Courses by topic ("AI classes", "data structures courses") | `scripts/asu_search.py classes --keywords "<topic>"` |
| Courses by instructor ("classes by Dr. Yang") | `scripts/asu_search.py classes --instructor "<name>"` |
| Open seats only ("open sections of CSE 310") | add `--open-only` to any classes search |
| Campus or day filter ("MWF classes", "Tempe campus") | add `--campus <CAMPUS>` or pass days in keywords |
| A professor or researcher ("who teaches ML", "Prof Berisha's email") | `scripts/asu_search.py people --query "<name or topic>"` |
| Campus events ("career fair", "events this week") | `scripts/asu_search.py events --keywords "<topic>"` |
| Upcoming events (no filter) | `scripts/asu_search.py events` |
| ASU news ("latest news", "research news") | `scripts/asu_search.py news --keywords "<topic>"` |
| Latest news (no filter) | `scripts/asu_search.py news` |
| A broad topic ("robotics at ASU", "tell me about sustainability") | Run classes, people, events and news searches for the topic |

Run the command from this Skill's folder.

### 2. Read the script output

The script prints JSON. Pick the fields the student needs.

**Classes output:**
- `total_found`: total matching sections
- `classes[]`: each has `course`, `title`, `section`, `days`, `time`, `location`, `campus`, `instructors`, `seats_total`, `seats_taken`, `seats_open`, `units`, `enrollment_status`

**People output:**
- `people[]`: each has `name`, `title`, `department`, `email`, `phone`, `campus`, `profile` (link to ASU directory)

**Events output:**
- `events[]`: each has `title`, `date`, `time`, `location`, `url`

**News output:**
- `stories[]`: each has `title`, `date`, `summary`, `url`


### 3. Reply to the student

Follow the reply rules below.

## Replies

Keep each reply to a few short lines, plain text, no Markdown formatting. Lead with the most useful answer.

For classes, lead with seats:
```
CSE 310 - Data Structures and Algorithms
Spring 2027, 8 sections

Open seats:
- Sec 1001: MW 9-10:15am, Tempe, 79/150 open
- Sec 1002: TuTh 1:30-2:45pm, Tempe, 45/120 open
- Sec 2101: Online/Async, 59/100 open

3 more sections available.
Want a daily seat check for a specific section?
```

For people, lead with name and contact:
```
Visar Berisha - Professor
Fulton Schools of Engineering
visar@asu.edu | 480/747-6455
https://search.asu.edu/profile/226165
```

For events, lead with date:
```
3 upcoming events:
- Oct 25: Sun Devil Football vs Kansas State (Tempe)
- Oct 28: AI Upskilling Workshop (Tempe)
- Nov 1: Fall Career Fair (Downtown)

Tap for details:
https://asuevents.asu.edu/event/...
```

For broad topics, group by type and keep it short. If more than 5 items in any category, name the top 3 and say how many more.

Put links on their own line so the phone shows a preview.

If nothing matches, say so in one line and suggest a broader search.

## Recurring check-ins

When the student asks about class seats, offer a daily seat-count check-in:
"Want me to check CSE 310 seats every morning at 8 am and text you if anything opens up?"

Create the check-in only after the student says yes. Word it so it makes sense days later:
"ASU Campus Scout: check CSE 310 (class 11198) seat count for Spring 2027 and text the student if open seats changed since yesterday."

Let the student pick the time and course. One check-in per course.

## When something fails

| Problem | What to say |
| --- | --- |
| Script exits with error | "ASU's systems aren't responding right now. Try again in a minute." |
| No classes match | "No sections found for that search. Try a broader keyword or check the subject code." |
| No events match | "Nothing on the ASU calendar for that. Try a broader word like 'career' or 'workshop'." |
| No people match | "Nobody in the ASU directory matched that. Try a last name or a broader topic." |
| No news match | "No ASU news stories for that topic." |
| Student asks about a non-ASU school | "This only searches Arizona State University. It won't work for other schools." |
