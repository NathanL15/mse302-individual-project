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

## What's unknown

- How the time to get back splits between finding your stuff and rebuilding the mental model.
- How many separate threads a person is juggling in a day and how long they sit before being picked back up or dropped.
- Which signals are enough, like titles and URLs, clipboard, the active document, calendar or the chat thread, and where the line between useful and creepy sits for people.
- How people want a restored context shown to them: a list, a one-line summary, re-opening everything, or a nudge.
- What share of switches cross devices (phone to laptop), which no single-device tool sees.
- What exactly people objected to with Recall: the capture, the storage, the searchability, or Microsoft, and each one implies a different design.
- Whether existing session managers fail because they can't do it or because nobody adopts them.

