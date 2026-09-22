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

## What's unknown

- What fraction of notifications actually get acted on vs dismissed vs ignored, broken down by category and platform.
- How people define "important" for themselves and whether it changes with context (in class, at work, asleep, driving).
- Whether missing one urgent message costs more than all the interruptions it saves, and how people want to override the system when it's wrong.
- What a third-party app can legitimately see and do on each platform (Android has NotificationListenerService, Windows has UserNotificationListener, iOS doesn't really give you anything), and that decides what's buildable.
- How much of the pile is the same event hitting phone + laptop + watch vs genuinely new events.
- How different the desktop problem is from the phone problem, since almost all the research is mobile.
- How people feel about an AI deciding for them, like whether they trust it and whether they can override it.

