---
slug: noisy-alerts-on-call-fatigue
title: "Monitoring floods on-call with non-actionable alerts, and real incidents get lost in the noise"
who: "SREs, on-call engineers, DevOps/platform engineers"
vertical: dev-tools
summary: "Teams running Prometheus, Grafana, and PagerDuty report being flooded with alerts, most of which need no action, leading to alert fatigue and on-call burnout. Engineers describe reviewing a week of pages and finding most required nothing, while constant Slack and pager pings desensitize responders until genuine incidents get missed. The recurring ask: tune thresholds and route non-urgent alerts so on-call only wakes for real customer impact."
evidence:
  - url: "https://www.reddit.com/r/devops/comments/1fjmgb3/monitoring_and_alert_fatigue/"
    source: "r/devops (Reddit)"
    date: "2024-09"
    note: "Prometheus + Grafana setup 'generates too many alerts, which sometimes causes alert fatigue'; top comments call this a 20-year-unsolved problem"
  - url: "https://news.ycombinator.com/item?id=32162038"
    source: "Hacker News"
    date: "2022-07"
    note: "'Being on call sucks' — large discussion of alert noise driving burnout and over-automation"
  - url: "https://www.reddit.com/r/devops/comments/lh3wkw/what_are_your_best_tips_for_avoiding_alert_fatigue/"
    source: "r/devops (Reddit)"
    date: "2021-02"
    note: "Manager describes weekly PagerDuty reviews where most pages needed no action; skepticism that AI-dedup tools work ('It doesn't work.')"
current_workarounds: "Weekly manual reviews of the previous week's pages; hand-tuning alert thresholds; routing non-urgent alerts to lower-priority channels; over-investing in automation to reduce pages; following Google SRE alerting philosophy; trying AI alert-dedup products that some report don't deliver."
why_unsolved: "Alert relevance is org- and service-specific, so generic thresholds and dedup heuristics either suppress real signals or leave noise. Tuning is continuous manual toil no tool fully automates — commenters note the problem is essentially unchanged in 20 years despite better tooling."
signals:
  - "290 points on the Hacker News on-call thread (observed 2026-07)"
  - "50 points / 26 comments on the 2024 r/devops thread (observed 2026-07)"
status: curated
date_curated: 2026-07-24
---
