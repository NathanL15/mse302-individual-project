# Notifications (problem A)

## Problem statement

People get anywhere from dozens to a couple hundred notifications a day across their phone and laptop, and every app picks its own priority, so the handful that are actually time-sensitive are mixed in with promos, social updates and the same alert repeated on every device. People tend to deal with it by checking constantly (which makes it pretty hard to focus) or by muting broadly (which means the important stuff gets lost too). The fixes at the OS level are pretty coarse and per-app, and lately they've only been shipping on the newest flagship phones.

## What's known

- A 7-day study that logged 15 people's phones found 63.5 notifications a day on average, mostly messengers and email. People looked at them within minutes even on silent, and more notifications went with more negative mood ([Pielot, Church, de Oliveira, MobileHCI 2014](https://doi.org/10.1145/2628363.2628364)).
- The notification count has been getting worse over time. [Common Sense Media](https://www.commonsensemedia.org/research/constant-companion-a-week-in-the-life-of-a-young-persons-smartphone-use) logged teens' phones for a week in 2023 and found a median of 237 a day, [industry roundups](https://www.mobiloud.com/blog/push-notification-statistics) put the average US adult around 46 push notifications a day, and [one iPhone dataset](https://workplaceinsight.net/people-receive-a-phone-notification-every-ten-minutes-on-average/) had Gen Z at about 181.
- Average screen attention before switching is 47 seconds (median 40), and it takes about 23 minutes to fully get back to a task after an interruption ([Gloria Mark, UC Irvine](https://www.universityofcalifornia.edu/news/cant-pay-attention-youre-not-alone); [Mark et al., CHI 2008](https://doi.org/10.1145/1357054.1357072); [Attention Span, 2023](https://gloriamark.com/attention-span/)).
- Apple shipped Priority Notifications in iOS 18.4 (March 2025). It ranks on-device using who sent it, how time-sensitive it looks and how often you interact with that person or app. It's only on iPhone 15 Pro/Pro Max and the iPhone 16 line so far, and it's off by default ([Apple Support](https://support.apple.com/guide/iphone/summarize-notifications-reduce-interruptions-iph1fbe7d2b9/ios); [TechCrunch](https://techcrunch.com/2025/03/31/apple-rolls-out-priority-notifications-as-apple-intelligence-expands-to-eu/)).
- Google added a notification organizer and on-device AI summaries in Android 16 (Pixel Drop, Dec 2025). The summaries are only on Pixel 9 and 10 so far ([Android Central](https://www.androidcentral.com/phones/google-pixel/how-to-set-up-use-android-ai-notification-summaries); [TechCrunch](https://techcrunch.com/2025/12/02/android-16-adds-ai-notification-summaries-new-customization-options-and-more/)).
- Apple paused its AI news summaries in the iOS 18.3 beta (Jan 2025) after the BBC complained about a made-up headline, so if the triage is wrong people tend to stop trusting it pretty fast ([TechCrunch](https://techcrunch.com/2025/01/16/apple-pauses-ai-notification-summaries-for-news-after-generating-false-alerts/)).
- There are research prototypes too, like PrefMiner, which learned readable rules for which notifications a person accepts ([Mehrotra et al., UbiComp 2016](https://doi.org/10.1145/2971648.2971747)). Attelia detected breakpoints in what you're doing and held alerts until then ([Okoshi et al., PerCom 2015](https://doi.org/10.1109/PERCOM.2015.7146515)). A 24-hours-without-push study found people were less distracted but more anxious about missing things ([Pielot and Rello, 2017](https://arxiv.org/abs/1612.02314)).
- On the sender side, 46% of people opt out of an app's push after 2 to 5 messages in a week (industry survey cited by [MobiLoud](https://www.mobiloud.com/blog/push-notification-statistics)).

## What's assumed

- People can say what counts as important to them, and it's stable enough to learn.
- Sender, recency and how often you interact with them cover most of what makes something important (which is the Apple and Google approach).
- People want fewer notifications, though it could also be that they want the same ones at better times, which is a different problem.
- A small on-device model is fast and cheap enough to score every notification on normal hardware.
- Apps will probably keep sending everything, so any fix has to live at the OS or on the user's side and can't really count on developers cooperating.
- Apple and Google seem to assume it's fine to gate this to new hardware.

## What's unknown

- What fraction of notifications actually get acted on vs dismissed vs ignored, broken down by category and platform.
- How people define "important" for themselves and whether it changes with context (in class, at work, asleep, driving).
- Whether missing one urgent message costs more than all the interruptions it saves, and how people want to override the system when it's wrong.
- What a third-party app can legitimately see and do on each platform (Android has NotificationListenerService, Windows has UserNotificationListener, iOS doesn't really give you anything), and that decides what's buildable.
- How much of the pile is the same event hitting phone + laptop + watch vs genuinely new events.
- How different the desktop problem is from the phone problem, since almost all the research is mobile.
- How people feel about an AI deciding for them, like whether they trust it and whether they can override it.

## Breaking it down

Process
1. An app fires an event and posts a notification with whatever priority flag or channel it picked.
2. The OS delivers it and the device alerts you: sound, vibration, banner, badge, often on more than one device at once.
3. You glance, read the preview, and decide: deal with it now, later, swipe it away, or ignore it.
4. If you deal with it now you leave what you were doing, and then pay the cost of getting back.
5. Every so often you go fix your settings (per-app toggles, Do Not Disturb, Focus modes), usually after a bad week.

People
- Regular users want to be reachable without being pulled around all the time, and the pain is the overload, the anxiety about missing stuff, and settings that are annoying to maintain.
- App developers and growth teams want engagement, and their pain is opt-outs and platform rules that demote them.
- Apple, Google and Microsoft want people happy and want to keep control of the ecosystem, and they own the only privileged signals.
- Senders (family, teammates, employers) expect a fast reply and can't see the receiver's pile.
- Researchers and digital-wellbeing people want a measurable drop in interruption harm.

Interactions
- Between the user and their settings there are per-app switches, schedules and Focus modes, which are all rule-based and rarely revisited.
- Between the user and the people messaging them, the social expectation of replying fast is what pushes you to look at everything.
- Between an app and the OS there are interruption levels, channels and priority flags, and since developers rate their own urgency they're motivated to inflate it.
- Between devices, the same event gets delivered to the phone, the laptop and the watch.

Environment
- Context changes hour to hour (meeting, lecture, driving, sleep) and the right triage changes with it.
- Multi-device people and households multiply the same alerts.
- The newest fixes have only shipped on flagship hardware so far, so most people don't get them.
- Notification content is personal, so anything that reads it has to be private by design, which is why the vendors run it on-device.

Analogies
- A near one is email spam filtering and Gmail's Priority Inbox, which learned importance from what you did and let you correct it.
- Another near one is on-call alert dedup and routing in tools like PagerDuty.
- A far one is alarm fatigue in ICUs, where too many low-value alarms end up making clinicians miss the real ones.
- Another far one is ER triage, where a short structured assessment sets your place in the queue and the two kinds of mistakes cost very different amounts.

## Sources to hit

- ACM Digital Library and Scopus: MobileHCI, CHI and UbiComp/IMWUT papers on notifications, interruptibility and receptivity.
- Gloria Mark's book Attention Span (2023) and her UC Irvine papers on attention and interruptions.
- Common Sense Media, Constant Companion (2023), the teen notification study.
- Apple Support and developer docs on Priority Notifications and Focus. Google's Android developer docs on notification channels and the Android 16 organizer. Microsoft docs on Focus assist and UserNotificationListener.
- Tech press: TechCrunch, Android Central, Tom's Guide, and the coverage of the BBC complaint about Apple's summaries.
- What users say: r/productivity, r/digitalminimalism, r/android, r/ios, Hacker News, and app store reviews of notification managers like BuzzKill, FilterBox and Daywise.
- Push-marketing stats (MobiLoud, Business of Apps) for the sender side.

People who'd know:
- Heavy messaging users: students in group projects, parents, people on call.
- The researchers who've measured this: Pielot, Mehrotra, Mark.
- Developers of third-party notification managers. Their changelogs and support forums show what users keep asking for.
- Accessibility and ADHD communities, where the cost of an interruption is highest.
- For the individual project I'm reaching these through their published work and public posts. Interviews are optional and I'm not planning any.

## Methods

- Literature review on Scopus and ACM DL. Keyword groups: (1) notifications: "push notification*", "mobile notification*", "smartphone notification*", alert*; (2) attention: interrupt*, interruptib*, receptivity, overload, attention; (3) intervention: prioriti*, triage, filter*, defer*, predict*, "machine learning". Search string: TITLE-ABS-KEY(("push notification*" OR "mobile notification*" OR "smartphone notification*") AND (interrupt* OR interruptib* OR receptivity OR overload) AND (prioriti* OR triage OR filter* OR defer* OR predict*)), which answers what's been measured and what's been tried.
- Benchmark existing solutions: a feature matrix of Apple, Google, Microsoft and the third-party managers on what signals they use, where inference runs, hardware gating, override and explanations, which answers where the gap is.
- Platform capability audit from developer docs: which notification signals a non-vendor app can read or act on per OS, which answers what's buildable outside the vendor.
- Content analysis of social media and reviews: collect complaints and workarounds from Reddit, Hacker News and app stores and tag them by cause (volume, timing, duplicates, missed things, distrust of AI), which answers how people describe the pain in their own words.
- Secondary data: look for published notification logs or datasets from the papers above to estimate act-on rates by category.
- Analogous contexts: how priority inbox and the ICU alarm-management literature dealt with the two kinds of error costing different amounts.

Scopus string:

```
TITLE-ABS-KEY(("push notification*" OR "mobile notification*" OR "smartphone notification*") AND (interrupt* OR interruptib* OR receptivity OR overload) AND (prioriti* OR triage OR filter* OR defer* OR predict*))
```

## Timeline (M3 is Oct 19)

- [ ] Sep 24 to 27: Platform capability audit. Read Apple, Google and Microsoft developer docs. Table of what signals and actions are available per OS (4 h)
- [ ] Sep 27 to Oct 2: Literature review. Run the Scopus string, screen down to 10 to 12 papers, annotate findings and methods in the repo (6 h)
- [ ] Oct 2 to 5: Benchmark existing solutions. Feature matrix of the OS features and 6 to 8 third-party managers, note the gaps (4 h)
- [ ] Oct 5 to 9: User-voice content analysis. Collect and tag 80 to 100 posts and reviews, count causes and workarounds (4 h)
- [ ] Oct 9 to 11: Analogous contexts. Short notes on priority inbox and alarm fatigue, what carries over (2 h)
- [ ] Oct 11 to 15: Synthesis. Stakeholder map, journey map, gap list, rewritten problem statement and open questions (4 h)
- [ ] Oct 15 to 18: Milestone 3 write-up. Draft and clean up the repo (4 h)

About 28 hours.
