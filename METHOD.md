# Method

## Snapshot

These tables are exported from the data each page served at the time below, so they match the page as it stood then. The pages keep updating (trends daily, the others every few hours), and the files here do not.

| Page | What it covers | Snapshot |
| --- | --- | --- |
| [Trends](https://admakeai.com/ad-insights/trends) | 538,068 new ads from 730 brands, launched June 8 to October 25, 2026 (20 weeks) | computed November 10, 2026 |
| [Longest-running ads](https://admakeai.com/ad-insights/longest-running-ads) | the oldest ad still running for each of 947 brands | November 11, 2026, 05:48 UTC |
| [Black Friday 2026](https://admakeai.com/ad-insights/black-friday-ads) | Black Friday and Cyber Monday ads of the same 947 brands | November 11, 2026, 07:49 UTC |

## How the numbers are made

**Source.** The Meta Ad Library, Meta's public record of the ads running on Facebook, Instagram, Messenger, WhatsApp, Threads and the Audience Network. For each ad we keep the start date the library shows, its format, placements, button and text, and when we last saw it running.

**Brands.** A panel of 730 active Meta advertisers across 36 categories (385 ecommerce, 141 software, 204 services), all watched since June 8, 2026, so every week compares the same brands. The panel is chosen by industry and weighted to ecommerce, software and services brands that advertise heavily. The longest-running and Black Friday tables use all 947 published brands with an ad running.

**Trends window.** Ads launched June 8 to October 25, 2026: 20 weeks. A week counts once it ended 10 days ago, because new ads take a few days to appear in the library. An ad counts only if it launched after we began watching its brand.

**Lifespan.** Uses the 510 brands with a complete weekly read of their live ads in the 10 days before the computation (273,302 ads). An ad's age is counted in whole weeks from its start date to the brand's latest full read. It counts as running if it was seen live in one of the brand's last two weekly reads (within 8 days). A week is charted only with 1,000+ ads from 50+ brands behind it.

**Shares.** Each weekly share is the mean of every brand's own share, counting brands with 5 or more launches that week, so one big advertiser cannot move a line. A line is flagged `moved` only when it changes by 5+ points and 1.5x, both per brand and with all ads pooled, and by 3x its normal weekly variation.

**Sale copy.** An ad has a "% off" when its text (body, headline or link description) matches a number followed by "% off". Seasonal events are matched on words in the same text, for example "black friday", "cyber monday" or "bfcm".

**Longest-running.** For each brand, its oldest ad that is still live: active in the library and seen running in the last 14 days. Days running is the time from the start date to the last time we saw it live.

**Black Friday.** An ad counts when its text says Black Friday, Cyber Monday or BFCM. Live means seen running in the last 14 days. First-ad weeks count the 715 brands watched since August 3, 2026, the start of the season. The "% off" is worked out per brand (the median of what its live ads from this season state), so a brand with 300 ads counts once.

## Limits

- Ads are checked weekly, so an ad can count as running for up to a week after it stops: real lifespans are slightly shorter than shown. Ads under 2 weeks old are not charted.
- Holiday and "% off" figures read the ad text. Offers shown only in the image or video, or written in another language, are not counted.
- The library shows no spend or results for these ads.
- The Black Friday tables are a mid-season snapshot (November 11, 2026). The latest weeks were still filling in.

## Not included

Ad copy, images, videos and personal data. The only per-ad rows are the longest-running ads the page lists, each linked to its public Ad Library entry. Brands are named only where the pages name them.
