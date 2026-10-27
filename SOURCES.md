# Automatic station observations

Collection uses public retailer-posted prices, with no driver reports and no
archived Google Places prices. Coverage depends on what each source publishes.
Stations without a matching current price and dated history receive no trend.

- Kwik Trip / Kwik Star: public store catalog and locator price responses at https://www.kwiktrip.com/locator.
- Circle K / Holiday: the official public locator at https://www.circlek.com/store-locator supplies automatic station-price responses. US coverage now uses bounded regional queries, splitting full responses to avoid the locator's 500-result truncation, deduplicating padded viewports, and rejecting conflicting duplicate records. The collector stops after 128 requests rather than claim a complete truncated result. Only unambiguous UNL regular gasoline and DSL diesel in USD per gallon are accepted. Ethanol, premium variants, DEF and ambiguous duplicate quotes are excluded.
- Marathon: https://www.marathonfuel.com/stations/ directly uses the public station catalog at https://www.marathonarcorewards.com/ajax_trip_planner_search.html?reason=get-station-info. Only US MARATHON Rewards records with numeric prices are accepted; ARCO and non-Rewards records are excluded. UNLEADED, MIDGRADE, PREMIUM and DIESEL are kept separate from ethanol, recreational/marine, off-road and unknown products. Cash, credit and unspecified posted price bases are retained independently; duplicate grade entries are rejected, never selected by cheapest. The page says prices refresh up to two hours ago, but individual quote timestamps are absent, so collection time means observed on the retailer website, not a verified pump update. Operator names such as Admiral are preserved and the app requires an exact operator or Marathon identity plus address, coordinates, grade and current displayed price.
- Pilot / Flying J network: public station pages linked from https://pilotcompany.com/fuel-prices. Product codes are preserved. E15 is not treated as regular gasoline. Differing cash/credit prices are excluded.
- Costco / Sam's Club: automatically collected retailer observations published by https://github.com/coatless-data/club-gas-prices. Release digests are checked. The publisher licenses its code under MIT and makes no license claim for retailer-derived data.
- Current Costco observations are also fetched from the retailer's own public US price response. Old snapshots are never relabelled as today's observations. Puerto Rico's per-litre prices are excluded from the US-gallon comparison feed.

Collection times mean "observed on the website", not a confirmed price-change
time. Prices may differ from the pump. Sources are unofficial integrations and
may become unavailable. History uses each station's timezone and compares the
same source, physical station, product, pricing basis, currency and unit.

Circle K's raw retailer update label is retained separately from our observation
time. A newly fetched official posted price can retain an older update label;
requiring that label to change every day wrongly prevents unchanged-price history.
Offset-aware update timestamps may be at most seven days old. Offset-free labels
must be within the preceding seven station-local calendar days; no UTC offset or
precise source-update instant is invented. Older, future, missing or invalid labels
stay excluded. Our website observations still expire after 12 hours and are dated
when actually collected, not when the retailer last updated the price.
History accumulates from actual future
collections; today's observation is never backfilled into yesterday or last week.
The app still requires a matching Google station identity, grade and current
displayed price. Existing Google places named only Holiday may not match a
Circle K source record until the map's retailer identity is updated.

Timezone boundaries are provided by timezonefinder-data / timezone-boundary-builder,
derived from OpenStreetMap; see those projects for their ODbL attribution and
data licensing. Source data is not relicensed by this repository.

New app builds download only relevant 5-degree latitude by 10-degree longitude
regional files, with a bounded cache. The legacy fuel-history.json remains limited
to its original supported providers and northern Circle K area for build73 and
earlier. Empty regions are explicitly published; stale data never becomes Same.
Each region and the legacy feed retain the 4 MB / 10,000 station size limits.
User coordinates, trips, Google API keys and Google prices are never uploaded to
the collector; downloading a public region file reveals only that coarse region.
No protected endpoint, embedded site key, login challenge or paid plan is used.

Checked October 27, 2026: Shell's public Ishpeming and NJ station records returned
null prices despite the official Shell app offering prices. BP Marquette's public
record had no numeric fuel prices. Krist's locator listed locations/amenities but
no price fields. Exxon/Mobil's locator refused automated access (HTTP 403); no
challenge bypass was attempted. Sunoco's official locator FAQ explicitly states
that it does not show gas prices. These sources are not claimed as coverage.
The source sites retain their own rights; this repository does not relicense
retailer data, page text or brand artwork.
