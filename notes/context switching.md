# Losing your place when switching apps (problem B)

## Problem statement

Students and knowledge workers spread one task across browser tabs, chat threads, docs, terminals and notes. When they switch, because someone interrupted them or they just wandered off, there isn't really anything that saves where they were. Getting back means finding everything again and re-reading to rebuild the context, some threads never get picked back up, and the tools that try to help either only restore your window layout or record everything and set off a privacy backlash.

## What's known

- Average screen attention before switching went from 2.5 minutes (2004) to 75 seconds (2012) to 47 seconds (since around 2016). It takes about 23 minutes 15 seconds to fully get back to an interrupted task ([Gloria Mark, UC Irvine](https://www.universityofcalifornia.edu/news/cant-pay-attention-youre-not-alone); [Mark et al., CHI 2008](https://doi.org/10.1145/1357054.1357072)).
- A field study of information workers found 57% of their working spheres got interrupted, people interrupted themselves about 11 times a day, and it took 25 minutes on average to get back to an interrupted task, usually through two or more other tasks first ([Mark, Gonzalez and Harris, CHI 2005](https://doi.org/10.1145/1054972.1055017)).
- A field study of task suspension and resumption found people usually went through other apps before returning to what they'd been doing, and proposed recovery aids like reminders and restoring task context ([Iqbal and Horvitz, CHI 2007](https://doi.org/10.1145/1240624.1240730)).
- Attention residue: thinking about the previous task carries over after you switch and hurts performance on the next one ([Leroy, 2009](https://doi.org/10.1016/j.obhdp.2009.04.002)).
- [Microsoft's Work Trend Index (June 2025)](https://www.microsoft.com/en-us/worklab/work-trend-index/breaking-down-infinite-workday) found employees get interrupted every two minutes during core hours, about 275 times a day, by meetings, email and chat pings.
- Windows Recall takes screenshots every few seconds and indexes them with on-device AI. It got delayed from June 2024 after the security backlash, shipped opt-in on Copilot+ PCs in April 2025, still gets flagged by security researchers in 2026, and Microsoft was reported in Jan 2026 to be rethinking it ([Wikipedia](https://en.wikipedia.org/wiki/Windows_Recall); [GeekWire 2026](https://www.geekwire.com/2026/one-year-after-its-rocky-launch-microsofts-windows-recall-still-raises-security-red-flags/)).
- The existing tools (macOS Stage Manager, Windows virtual desktops and snap groups, browser tab groups and session managers like Arc spaces, Workona and Session Buddy, IDE workspace restore) mostly bring back the windows and tabs, and none of them really bring back what you were doing.
- Rewind.ai, the best-known continuous screen-memory startup, pivoted to the Limitless pendant in April 2024, which suggests the desktop version was hard to keep going ([TechCrunch](https://techcrunch.com/2024/04/17/a16z-backed-rewind-pivots-to-build-ai-powered-pendant-to-record-your-conversations/)).

## What's assumed

- Enough task state can be pulled from metadata (window titles, URLs, open files, recent messages) without screen recording.
- People want their context back, and fewer switches would be a different fix since a lot of switching is legitimate anyway.
- A local model can figure out "which task was this" from that metadata, and tasks cluster cleanly.
- Privacy is probably the main reason people wouldn't adopt this, so the Recall backlash is the list of constraints to design against.
- Most of the time spent getting back goes to finding things again, and that part can be automated, but the re-thinking part probably can't.

## What's unknown

- How the time to get back splits between finding your stuff and rebuilding the mental model.
- How many separate threads a person is juggling in a day and how long they sit before being picked back up or dropped.
- Which signals are enough, like titles and URLs, clipboard, the active document, calendar or the chat thread, and where the line between useful and creepy sits for people.
- How people want a restored context shown to them: a list, a one-line summary, re-opening everything, or a nudge.
- What share of switches cross devices (phone to laptop), which no single-device tool sees.
- What exactly people objected to with Recall: the capture, the storage, the searchability, or Microsoft, and each one implies a different design.
- Whether existing session managers fail because they can't do it or because nobody adopts them.

## Breaking it down

Process
1. Working on task A across a few apps.
2. A switch happens: an alert, a message, a meeting, or just your own impulse.
3. You open new stuff for task B. Sometimes B leads to C.
4. You try to go back to A: remember what it was, find its tabs, files and threads, re-read to recover state.
5. You resume A with B still in your head, or you leave A until a deadline forces it.

People
- Students and knowledge workers want to finish things, and the pain is lost threads, redoing work and being drained by the end of the day.
- Teammates and managers are the source of a lot of the interruptions, and they expect a fast reply.
- IT and security tend to block or ban anything that records activity, and they care about compliance.
- Microsoft, Apple and Google own the OS-level signals and set the privacy narrative.
- Tool makers (browsers, IDEs, chat apps) each restore their own state and none of them share it.

Interactions
- With the browser it's tabs as a to-do list, tab groups and session managers.
- With chat (Teams, Slack, Discord) it's threads that hold the task context but are hard to find again.
- With the IDE or terminal, workspaces restore the files and you still have to remember why they were open.
- With notes it's writing down where you were by hand, which is the current workaround and it decays fast.
- Between tools, they don't share state with each other, so you're the one carrying the context between them.

Environment
- Laptop-only vs multi-monitor changes how much you can keep visible.
- Remote and hybrid work means more chat-driven interruptions.
- Company policy often bans activity-recording software, and personal devices are more open.
- On-device accelerators (NPUs) now make continuous local inference realistic without sending anything anywhere.

Analogies
- A near one is git stash and branches, which save your work state with a label and bring it back on demand.
- Another near one is browser session restore and game save states.
- A far one is shift handoff in hospitals (SBAR), a structured summary that moves context from one person to the next.
- Another far one is pilot checklists and surgical timeouts, which cut errors when you pick a procedure back up after a pause.

## Sources to hit

- CHI, CSCW and UIST papers on task switching, interruption and resumption: Mark; Iqbal and Horvitz; Czerwinski, Horvitz and Wilhite (2004 diary study); Leroy on attention residue.
- Microsoft Work Trend Index 2025 (the "infinite workday" report).
- Windows Recall coverage: the Wikipedia timeline, GeekWire (2026), and Microsoft's own Recall docs and privacy statements.
- Product docs and changelogs for Arc, Workona, Session Buddy, Stage Manager, Windows snap groups, VS Code workspaces. Rewind and Limitless announcements.
- What users say: r/productivity, r/ADHD, r/macos, r/windows11, Hacker News threads on Recall and on tab overload.
- Platform docs on what an app can observe: Windows UI Automation and window events, browser extension APIs, macOS accessibility permissions.

People who'd know:
- Students and knowledge workers, especially self-described tab hoarders and people who get interrupted a lot.
- Researchers: Gloria Mark, Shamsi Iqbal, Sophie Leroy.
- The people building session and workspace tools, through their public roadmaps and support forums.
- The security researchers who picked apart Recall, for the privacy constraints.
- For the individual project I'm reaching these through their published work and public posts. Interviews are optional and I'm not planning any.

## Methods

- Literature review on Scopus and ACM DL. Keyword groups: (1) switching: "task switching", "task resumption", "context switch*", interruption*, multitasking; (2) setting: computer*, desktop, "knowledge work*", "information work*"; (3) recovery: resum*, recover*, restor*, "attention residue", "task state". Search string: TITLE-ABS-KEY(("task switching" OR "task resumption" OR "context switch*" OR interruption*) AND (computer* OR desktop OR "knowledge work*" OR "information work*") AND (resum* OR recover* OR restor* OR "attention residue")), which answers what getting back actually costs and which recovery aids have been tried.
- Benchmark: a feature matrix of restore tools on what they capture, how granular, local vs cloud, privacy model, and whether they capture intent at all, which answers whether it's a capability gap or an adoption gap.
- Content analysis of the Recall backlash: code 60 to 80 articles and comments by what people objected to, which gives the privacy constraints a solution has to meet.
- Platform capability audit: what a non-vendor app can observe on Windows, macOS and in browsers with normal permissions, which sets the feasibility boundary.
- Content analysis of Reddit and Hacker News: how people describe losing their place and what workarounds they use.
- Optionally I could log my own switches for a week as a sanity check on the numbers in the literature, but it's not required since the plan is secondary sources.

Scopus string:

```
TITLE-ABS-KEY(("task switching" OR "task resumption" OR "context switch*" OR interruption*) AND (computer* OR desktop OR "knowledge work*" OR "information work*") AND (resum* OR recover* OR restor* OR "attention residue"))
```

## Timeline (M3 is Oct 19)

- [ ] Sep 24 to 30: Literature review. Run the Scopus string, screen down to 10 to 12 papers, annotate in the repo (6 h)
- [ ] Sep 30 to Oct 4: Benchmark restore tools. Feature matrix of 8 to 10 tools including Recall, Rewind/Limitless, Arc, Workona, Stage Manager (4 h)
- [ ] Oct 4 to 7: Recall backlash analysis. Code articles and comments by objection type, pull out the privacy constraints (3 h)
- [ ] Oct 7 to 10: Platform capability audit. Read the Windows, macOS and browser extension docs. Table of observable signals (3 h)
- [ ] Oct 10 to 13: User-voice content analysis. Collect and tag 60 to 80 posts on losing your place and the workarounds (3 h)
- [ ] Oct 13 to 16: Synthesis. Journey map of a switch, stakeholder map, gap list, rewritten problem statement (4 h)
- [ ] Oct 16 to 18: Milestone 3 write-up. Draft and clean up the repo (3 h)

About 26 hours.
