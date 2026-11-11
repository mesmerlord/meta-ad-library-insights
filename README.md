# Meta Ad Library insights, 2026

Aggregate statistics on the ads that a fixed panel of brands launches on Facebook, Instagram and the rest of Meta: how long new ads stay live, which formats, placements and buttons they use, when sale copy appears, how many ads a brand launches a week, the longest-running ads still live, and Black Friday 2026 ads. Every number comes from the public [Meta Ad Library](https://www.facebook.com/ads/library/).

These are the tables behind three web pages, exported from the data those pages served, so every value here matches the page:

| Page | What it covers | Snapshot |
| --- | --- | --- |
| [admakeai.com/ad-insights/trends](https://admakeai.com/ad-insights/trends) | 538,068 new ads from 730 brands, launched June 8 to October 25, 2026 (20 weeks) | computed November 10, 2026 |
| [admakeai.com/ad-insights/longest-running-ads](https://admakeai.com/ad-insights/longest-running-ads) | the oldest ad still running for each of 947 brands | November 11, 2026, 05:48 UTC |
| [admakeai.com/ad-insights/black-friday-ads](https://admakeai.com/ad-insights/black-friday-ads) | Black Friday and Cyber Monday ads of the same 947 brands | November 11, 2026, 07:49 UTC |

The pages are recomputed every few hours (trends daily), so their numbers move on from this snapshot. The files here do not.

## Files

All files are UTF-8 CSV with a header row. Every column is described in [DATA_DICTIONARY.md](DATA_DICTIONARY.md). `scope` is `all`, `ecommerce`, `software` or `services`; weeks are named by their Monday (ISO date).

| File | Rows | What it holds |
| --- | ---: | --- |
| `data/trends_summary.csv` | 4 | Panel size, sample sizes and headline figures, one row per scope |
| `data/trends_lifespan_curve.csv` | 64 | Share of new ads still running, by weeks since launch |
| `data/trends_lifespan_by_format.csv` | 14 | Share still running 4 to 7 weeks after launch, by format |
| `data/trends_lifespan_by_launch_week.csv` | 64 | Share of each launch week still running 4 weeks later |
| `data/trends_live_ads_by_age.csv` | 20 | Ads running at the latest check, by how long ago they launched |
| `data/trends_launch_mix_weekly.csv` | 1,120 | Weekly share of a brand's new ads in each format, placement and button |
| `data/trends_launch_mix_change.csv` | 56 | The same shares, first four weeks against last four |
| `data/trends_sale_calendar_weekly.csv` | 320 | Weekly share of new ads with a "% off", and with each seasonal event in the copy |
| `data/trends_sale_events.csv` | 12 | When each seasonal event's ads start and peak |
| `data/trends_launch_pace_weekly.csv` | 80 | New ads per brand per week: lower quartile, median, upper quartile |
| `data/trends_launch_weekday.csv` | 28 | Launches per weekday, relative to the busiest day |
| `data/trends_top_launchers.csv` | 15 | The five brands launching the most per market, latest four weeks |
| `data/longest_running_summary.csv` | 1 | Brands, live ads, and brands with an ad live for 1+ and 2+ years |
| `data/longest_running_by_industry.csv` | 36 | Brands per industry, and how many have an ad live for a year or more |
| `data/longest_running_ads.csv` | 108 | The three longest-running live ads in each industry (one per brand), with the top 10 overall ranked |
| `data/black_friday_summary.csv` | 1 | Live Black Friday ads and brands, and the "% off" they state |
| `data/black_friday_first_ads_weekly.csv` | 15 | Brands launching their first Black Friday ad of the season, by week |
| `data/black_friday_pct_off_bands.csv` | 4 | Brands by the typical "% off" their Black Friday ads state |
| `data/black_friday_most_live_ads.csv` | 3 | The three brands with the most live Black Friday ads |

## A few of the numbers

- Half of new Meta ads are switched off within 3 weeks. 28.2% are still running 4 weeks after launch, and 2.1% after 21 weeks.
- Between the first and last four weeks of the window, the share of a brand's new ads placed on Messenger fell from 76.8% to 20.6%, and on WhatsApp rose from 2.4% to 26.0%. Video held at about a third.
- The typical brand launches 16 new ads a week; the busiest quarter launch 50 or more. Sunday sees 30% as many launches as Tuesday.
- 115 of 947 brands have kept one ad running for a year or more; the longest has run 1,871 days.
- On November 11, 2026, 6,005 Black Friday ads from 147 brands were live. Of the brands whose ads state a "% off", the typical one says 45%.

## Method

**Source.** The Meta Ad Library, Meta's public record of the ads running on Facebook, Instagram, Messenger, WhatsApp, Threads and the Audience Network. For each ad we keep the start date the library shows, its format, placements, button and text, and when we last saw it running.

**Brands.** A panel of active Meta advertisers chosen by industry, not a random sample of all advertisers. The trends tables use a fixed panel of the 730 brands (36 categories: 385 ecommerce, 141 software, 204 services) we were already watching by June 8, 2026, so every week compares the same brands. The longest-running and Black Friday tables use all 947 published brands with an ad running.

**Trends window.** Ads launched June 8 to October 25, 2026: 20 weeks. A week counts once it ended 10 days ago, because new ads take a few days to appear in the library. An ad counts only if it launched after we began watching its brand.

**Lifespan.** Uses the 273,302 ads of the 510 brands whose full list of live ads we re-read in the 10 days before the computation; most of the rest run too many ads to re-read in full every week. An ad's age is counted in whole weeks from its start date to the brand's latest full re-read; it counts as running if it was seen live in one of the brand's last two weekly reads (within 8 days). A week is charted only with 1,000+ ads from 50+ brands behind it, and the curve stops where those run out or the share starts to rise.

**Shares.** Each weekly share is the mean of every brand's own share, counting brands with 5 or more launches that week, so one big advertiser cannot move a line. A line is flagged `moved` only when it changes by 5+ points and 1.5x, both per brand and with all ads pooled, and by 3x its usual week-to-week wobble.

**Sale copy.** An ad has a "% off" when its text (body, headline or link description) matches a number followed by "% off". Seasonal events are matched on words in the same text, for example "black friday", "cyber monday" or "bfcm".

**Longest-running.** For each brand, its oldest ad that is still live: active in the library and seen running in the last 14 days. Days running is the time from the start date to the last time we saw it live.

**Black Friday.** An ad counts when its text says Black Friday, Cyber Monday or BFCM. Live means seen running in the last 14 days. First-ad weeks count only the 715 brands we watched before August 3, 2026, the start of the season. The "% off" is worked out per brand (the median of what its live ads from this season state), so a brand with 300 ads counts once.

## Limits

- Weekly reads cannot date the end of an ad more finely than a week, so nothing under 2 weeks old is charted, and an ad can count as running for up to a week after it stops. The "switched off within" figures are, if anything, conservative.
- Holiday and "% off" figures match words in the ad text, so offers shown only in the image or video, or written in another language, are missed.
- The library shows no spend or results for these ads, so a long run is not proof of a profitable ad.
- The panel is brands we chose to track, weighted to ecommerce, software and services brands that advertise heavily. It does not represent all Meta advertisers.
- The Black Friday tables are a mid-season snapshot (November 11, 2026); the latest week was still filling in.

## What is not here

No ad copy, images or videos, no personal data, and no per-ad rows except the longest-running ads the page lists, each linked to its public Ad Library entry. Brands are named only where the pages name them.

## How to cite

Cite the page a number comes from:

> AdMakeAI (2026). Meta Ad Trends: how Facebook and Instagram ads are changing, week by week. New ads from 730 brands in the Meta Ad Library, June 8 to October 25, 2026. https://admakeai.com/ad-insights/trends

> AdMakeAI (2026). The longest-running Meta ads. 947 brands in the Meta Ad Library, as of November 11, 2026. https://admakeai.com/ad-insights/longest-running-ads

> AdMakeAI (2026). Black Friday 2026 ads on Meta. 947 brands in the Meta Ad Library, as of November 11, 2026. https://admakeai.com/ad-insights/black-friday-ads

To cite the dataset itself, use [CITATION.cff](CITATION.cff) (GitHub's "Cite this repository" button reads it).

## Source and license

The underlying records are public data from the Meta Ad Library. This dataset is not affiliated with, endorsed by or sponsored by Meta Platforms, Inc. Brand names belong to their owners.

The tables and text are published by [AdMakeAI](https://admakeai.com) under [CC BY 4.0](LICENSE): you can share and adapt them for any purpose, with credit and a link to the source page.
