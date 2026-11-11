# Data dictionary

Conventions used throughout:

- `scope`: `all`, `ecommerce`, `software` or `services`. The market a brand belongs to follows from its category.
- Dates are ISO `YYYY-MM-DD` (UTC). A `week` or `*_week` column is the Monday that starts the week.
- `pct` columns are percentages from 0 to 100, rounded to one decimal unless noted.
- "Mean brand share" means the share is worked out for each brand on its own, then averaged across brands with 5 or more launches that week, so one large advertiser cannot move it.
- An empty cell means "not applicable" (for example, an event with no fixed date).

## Trends: [admakeai.com/ad-insights/trends](https://admakeai.com/ad-insights/trends)

Panel of 730 brands; ads launched June 8 to October 25, 2026; computed November 10, 2026.

### `trends_summary.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market (see above) |
| window_start | date | | First day of the launch window |
| window_end | date | | Last day of the launch window |
| weeks | integer | weeks | Complete weeks in the window |
| brands | integer | brands | Brands in the fixed panel |
| categories | integer | categories | Distinct brand categories in the panel |
| new_ads | integer | ads | Ads launched in the window by panel brands, after we began watching each brand |
| lifespan_brands | integer | brands | Brands whose full list of live ads was re-read in the last 10 days; the lifespan tables use only these |
| lifespan_ads | integer | ads | Ads behind the lifespan curve (sum of `ads` in `trends_lifespan_curve.csv`) |
| half_off_within_weeks | integer | weeks | Weeks after launch by which more than half of new ads are no longer running |
| pct_running_at_4_weeks | number | % of ads | Share of new ads still running 4 weeks after launch |
| last_week_charted | integer | weeks since launch | Last point of the lifespan curve |
| pct_running_at_last_week | number | % of ads | Share still running at `last_week_charted` |
| live_ads_by_age_sample | integer | ads | Ads running at the latest check, behind `trends_live_ads_by_age.csv` |
| typical_new_ads_per_week | integer | ads per brand per week | Median of the weekly median launches per brand, over the last 8 weeks |
| top_quarter_new_ads_per_week | integer | ads per brand per week | Median of the weekly upper-quartile launches per brand, over the last 8 weeks |
| pct_brand_weeks_no_launch | number | % of brand-weeks | Share of brand-weeks with no new ad |
| pct_off_low | number | mean brand share, % | Lowest weekly share of new ads stating a "% off" |
| pct_off_low_week | date | | Week of `pct_off_low` |
| pct_off_high | number | mean brand share, % | Highest weekly share of new ads stating a "% off" |
| pct_off_high_week | date | | Week of `pct_off_high` |
| computed_on | date | | Date the page computed these numbers |

### `trends_lifespan_curve.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| weeks_since_launch | integer | whole weeks | Age of the ads at the brand's latest full re-read |
| pct_still_running | number | % of ads | Share of ads that age seen running in the brand's last two weekly reads (within 8 days) |
| ads | integer | ads | Ads of that age behind the point |

### `trends_lifespan_by_format.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| format | string | | Single image, Video, Carousel or Dynamic creative (formats with under 1,000 ads are left out) |
| pct_still_running_4_to_7_weeks | number | % of ads | Share of ads 4 to 7 whole weeks old that are still running |
| ads | integer | ads | Ads of that format and age |

### `trends_lifespan_by_launch_week.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| launch_week | date | | Week the ads launched |
| pct_running_4_weeks_later | number | % of ads | Share of that week's launches last seen live 28 or more days after their start date |

### `trends_live_ads_by_age.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| age_bucket | string | | Label of the age band |
| min_days | integer | days | Lower bound of the band (inclusive) |
| max_days_exclusive | integer | days | Upper bound (exclusive); empty for the open-ended band |
| pct_of_live_ads | number | % of live ads | Share of ads running at the latest check whose start date falls in the band. Counts every launch date, not only ads launched in the window |
| live_ads | integer | ads | All ads running at the latest check in this scope (same on every row of a scope) |

### `trends_launch_mix_weekly.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| group | string | | `format`, `placement` or `button` |
| attribute | string | | Format (Video, Single image, Carousel, Dynamic creative), placement (WhatsApp, Threads, Messenger, Audience Network) or button (Shop now, Learn more, Sign up, Get quote, Install app, Get offer) |
| week | date | | Launch week |
| mean_brand_share_pct | number | mean brand share, % | Share of a brand's new ads that week with this attribute |
| pct_brands_using | number | % of brands | Share of brands launching that week with at least one such ad |

Placements are not exclusive: one ad can run on several.

### `trends_launch_mix_change.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| group | string | | `format`, `placement` or `button` |
| attribute | string | | As in `trends_launch_mix_weekly.csv` |
| first_4_weeks_pct | number | mean brand share, % | Mean of the first four weekly values |
| last_4_weeks_pct | number | mean brand share, % | Mean of the last four weekly values |
| moved | boolean | | `true` when the change is 5+ points and 1.5x, both per brand and pooled, and 3x its normal weekly variation |

### `trends_sale_calendar_weekly.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| week | date | | Launch week |
| series | string | | `% off` (the ad text states a number followed by "% off"), or the name of a seasonal event matched in the ad text |
| mean_brand_share_pct | number | mean brand share, % | Share of a brand's new ads that week in the series |

Only events listed in `trends_sale_events.csv` for that scope have rows.

### `trends_sale_events.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| event | string | | Seasonal event matched in the ad text |
| event_date | date | | The day itself, when it has a fixed date |
| first_week | date | | First week the event was clearly in the copy (15% or more of its peak, working back from the peak) |
| peak_week | date | | Week with the highest share |
| peak_pct | number | mean brand share, % | Share of a brand's new ads mentioning the event in the peak week |
| lead_weeks | integer | weeks | Weeks between `first_week` and the week of the day |
| peak_weeks_before_day | integer | weeks | 0 = peaks in the week of the day, 1 = the week before, -1 = the week after |

### `trends_launch_pace_weekly.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| week | date | | Launch week |
| p25_new_ads | integer | ads per brand | Lower quartile of new ads per panel brand that week (brands with none count as 0) |
| median_new_ads | integer | ads per brand | Median |
| p75_new_ads | integer | ads per brand | Upper quartile |

### `trends_launch_weekday.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market |
| weekday | string | | Mon to Sun, by the ad's start date |
| index_vs_busiest_day | integer | index, busiest day = 100 | Launches on that weekday across the window, relative to the busiest weekday |

### `trends_top_launchers.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| scope | string | | Market (the page lists leaders per market only) |
| rank | integer | | 1 = most new ads |
| brand | string | | Brand name as shown on the page |
| new_ads_per_week | integer | ads per week | Mean new ads a week over the last four weeks of the window |

## Longest-running ads: [admakeai.com/ad-insights/longest-running-ads](https://admakeai.com/ad-insights/longest-running-ads)

All 947 published brands with an ad running; as of November 11, 2026.

### `longest_running_summary.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| as_of | date | | Date of the snapshot |
| live_within_days | integer | days | An ad counts as running if seen live in the library this recently |
| brands | integer | brands | Brands with at least one running ad |
| live_ads | integer | ads | Running ads across those brands |
| brands_1y_plus | integer | brands | Brands whose oldest running ad has run 365 days or more |
| brands_2y_plus | integer | brands | Brands whose oldest running ad has run 730 days or more |

### `longest_running_by_industry.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| industry | string | | Brand category |
| brands | integer | brands | Brands in the industry with a running ad |
| brands_1y_plus | integer | brands | Of those, brands whose oldest running ad has run 365 days or more |

### `longest_running_ads.csv`

One row per brand: its oldest running ad. Only the brands the page lists (the top three of each industry, which include the top 10 overall).

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| brand | string | | Brand name as shown on the page |
| industry | string | | Brand category |
| overall_rank | integer | | Rank among all 947 brands, 1 to 10; empty below 10 |
| industry_rank | integer | | Rank within the industry, 1 to 3 |
| running_since | date | | Start date shown in the Meta Ad Library |
| last_seen_live | date | | Last time the ad was seen running |
| days_running | integer | days | Whole days from `running_since` to `last_seen_live` |
| years_running | number | years | `days_running` / 365, one decimal |
| ad_library_url | string | URL | The ad's public Meta Ad Library entry |

## Black Friday: [admakeai.com/ad-insights/black-friday-ads](https://admakeai.com/ad-insights/black-friday-ads)

Ads whose text says Black Friday, Cyber Monday or BFCM; as of November 11, 2026, 07:49 UTC.

### `black_friday_summary.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| as_of | string | UTC timestamp | Time of the snapshot |
| season_from | date | | Start of the season; launches from here on are this season's |
| live_within_days | integer | days | An ad counts as live if seen running this recently |
| brands_tracked | integer | brands | Published brands with any ad running |
| live_bf_ads | integer | ads | Live Black Friday ads |
| live_bf_brands | integer | brands | Brands with at least one live Black Friday ad |
| brands_stating_pct_off | integer | brands | Brands whose live Black Friday ads from this season state a "% off" |
| median_pct_off | integer | % off | Median across those brands of each brand's median stated "% off" |
| p25_pct_off | integer | % off | Lower quartile of the same |
| p75_pct_off | integer | % off | Upper quartile of the same |
| panel_brands | integer | brands | Brands watched since before `season_from` (the base for the weekly table) |
| panel_brands_started | integer | brands | Of those, brands that have launched a Black Friday ad this season |
| panel_brands_started_last_14_days | integer | brands | Of those, brands whose first one launched in the last 14 days |

### `black_friday_first_ads_weekly.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| week | date | | Week of the season |
| brands_first_bf_ad | integer | brands | Panel brands whose first Black Friday ad of the season launched that week |
| week_complete | boolean | | `false` while the week is still filling in (new ads take up to 10 days to be found) |

### `black_friday_pct_off_bands.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| band | string | | Label of the "% off" band |
| min_pct | integer | % off | Lower bound (inclusive) |
| max_pct_exclusive | integer | % off | Upper bound (exclusive) |
| brands | integer | brands | Brands whose median stated "% off" falls in the band |

### `black_friday_most_live_ads.csv`

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| rank | integer | | 1 = most live Black Friday ads |
| brand | string | | Brand name as shown on the page |
| industry | string | | Brand category |
| live_bf_ads | integer | ads | Live Black Friday ads of the brand |
