---
title: "Data"
permalink: /data/
author_profile: true
---

## British Environmental and Economic Protest Event Dataset (BEEPED)

### Description

This dataset records 1,740 events organized or participated in by a collection of 85 environmental and economic protest groups, active in the UK between 2010 and 2020. The dataset is constructed from the groups' own tweets as part of a computer-assisted pipeline. Event attributes (strike, disruption, violence, public invitation, location, etc.) were hand-coded in line with the codebook provided. Events were then linked to news articles to measure the quantity of coverage received across 14 national news outlets in the UK. Full details on the construction of the dataset are provided in the publication:

> Jacobs, Michael, "Breaking into the Public Sphere: How Protest Tactics Shape Media Visibility". *British Journal of Political Science*, forthcoming

Replication files for that publication can be found at:

> Jacobs, Michael, 2026, "Replication Data for: 'Breaking into the Public Sphere: How Protest Tactics Shape Media Visibility'", [https://doi.org/10.7910/DVN/HH6GQM](https://doi.org/10.7910/DVN/HH6GQM), Harvard Dataverse, V1

The evidence base for each event's coding decisions can be viewed in this [Shiny app](https://anonymous-academic.shinyapps.io/timeline_app_upload/), which displays the tweets associated with each event.

### Downloads

[Download BEEPED_event.csv](/files/BEEPED_event.csv){: .btn .btn--primary}
[Download BEEPED_group_comb_day.csv](/files/BEEPED_group_comb_day.csv){: .btn .btn--primary}
[Download Codebook (PDF)](/files/BEEPED Codebook.pdf){: .btn .btn--primary}

### Data format

The dataset is provided in two formats:

1. **BEEPED_event** - Event-level dataset. Importantly, in this dataset, one group could appear as the actor for two distinct events, if those events appear to be uncoordinated (e.g. two branches of Extinction Rebellion organizing distinct actions with distinct demands in different locations).

2. **BEEPED_group_comb_day** - Group-combination-day dataset. Rows represent unique combinations of participating groups and days. This aggregation implicitly treats actions by the same group on the same day as part of the same event. This simplification makes the linking of events to news coverage more tractable. As such, in contrast to BEEPED_event, BEEPED_group_comb_day has columns representing the number of news articles in each of 14 national newspapers.

### Variables

**Variables common to both formats**

- `Event_date` - day of event
- `Event_group` - comma separated list of all groups participating in the event
- `involvement` - comma separated list indicating involvement type of each group participating in the event (same order as Event_group)
- `IsProtest` - indicates event type ('Protest', 'Strike', 'Both')
- `preannounced` - indicates when the event is first announced ('Before event', 'On day, before event', 'After event')
- `public_invitation` - indicates whether the public are invited to join the event ('Yes', 'No')
- `disruption` - indicates whether the event involves disruption ('Yes', 'No')
- `violence` - indicates whether the event involves violence ('Yes', 'No')
- `symbolic` - indicates whether the event involves symbolic elements ('Yes', 'No')
- `arrests` - indicates whether arrests take place at the event ('Yes', 'No')
- `location_target` - indicates the primary location of the event ('Public space', 'Company site', 'Political site', 'Embassy', 'Court', 'Entertainment/cultural', 'Other', 'Unknown')
- `Event_name` - free text string based on the participating group's own description. Event name if given, otherwise states demands.
- `headcount` - free text string based on the participating group's own description of headcount or event size.
- `action_freetext` - free text string based on the participating group's own description of action taken.
- `location_freetext` - free text string based on the participating group's own description of location.

**Variable only in BEEPED_event**

- `Event_id` - unique event identifier
- `Event_day` - day of the week of the event
- `Event_prob_protest` - aggregated output of BERT-NLI model, reflecting the model's confidence that the cluster of tweets associated with the event does in fact describe an event taking place on the relevant day, organized by the relevant group(s).
- `issue` - the broad issue area of the protest ('env' = environmental, 'pov' = economic)

**Variables only in BEEPED_group_comb_day**

**NB:** If a variable has 'bm' in its name, this indicates that it is constructed using the 'best match' method for event-article linking. This ensures that each article is only assigned to a single event, the one with the highest probability. Article count variables without 'bm' are constructed from the raw output of the random forest model, and it is possible that an article is 'double-counted' (assigned to more than one event).

- `group_date_id` - unique group-combination-day identifier
- `date_preannounced` - date of the first mention of the event.
- `n_tweets_about_event_day` - number of tweets by participating groups mentioning the event day.
- `n_tweets_about_event_day_weighted` - number of tweets by participating groups mentioning the event day, weighted by the probability that the tweet is about a protest event on that day (output of BERT-NLI model).
- `n_articles`/`n_articles_bm` - total number of articles predicted to be about the event.
- `n_articles_after`/`n_articles_bm_after` - number of articles predicted to be about the event, restricted to those published on or after the event day.
- `source_*`/`bm_source_*` - number of articles predicted to be about the event in each source. Source code: 'ind' = The Independent, 'express' = The Express, 'guardian' = The Guardian, 'dstar' = The Daily Star, 'mirror' = The Mirror, 'sun' = The Sun, 'metro' = The Metro, 'telegraph' = The Daily Telegraph, 'times' = The Times, 'ft' = The Financial Times, 'itv' = ITV News (TV transcripts), 'four' = Channel 4 News (TV transcripts), and 'bbc' = BBC News (TV transcripts).
