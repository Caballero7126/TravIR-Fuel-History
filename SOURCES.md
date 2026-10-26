# Automatic station observations

Collection uses public retailer-posted prices, with no driver reports and no
archived Google Places prices. Coverage depends on what each source publishes.
Stations without a matching current price and dated history receive no trend.

- Kwik Trip / Kwik Star: public store catalog and locator price responses at https://www.kwiktrip.com/locator.
- Circle K / Holiday: the official public locator at https://www.circlek.com/store-locator supplies automatic station-price responses. The current adapter covers the Upper Peninsula and nearby northern Michigan, Wisconsin and Minnesota communities in one bounded regional request. Only unambiguous UNL regular gasoline and DSL diesel in USD per gallon are accepted. Ethanol, premium variants, DEF and ambiguous duplicate quotes are excluded.
- Pilot / Flying J network: public station pages linked from https://pilotcompany.com/fuel-prices. Product codes are preserved. E15 is not treated as regular gasoline. Differing cash/credit prices are excluded.
- Costco / Sam's Club: automatically collected retailer observations published by https://github.com/coatless-data/club-gas-prices. Release digests are checked. The publisher licenses its code under MIT and makes no license claim for retailer-derived data.
- Current Costco observations are also fetched from the retailer's own public US price response. Old snapshots are never relabelled as today's observations. Puerto Rico's per-litre prices are excluded from the US-gallon comparison feed.

Collection times mean "observed on the website", not a confirmed price-change
time. Prices may differ from the pump. Sources are unofficial integrations and
may become unavailable. History uses each station's timezone and compares the
same source, physical station, product, pricing basis, currency and unit.

Circle K's raw retailer update label is retained separately from our observation
time. Offset-aware source timestamps must be no more than 12 hours old. When
the source omits its timezone, only labels dated today in the station's timezone
are accepted; no UTC offset or precise source-update instant is invented. Older,
missing or invalid labels stay excluded. History accumulates from actual future
collections; today's observation is never backfilled into yesterday or last week.
The app still requires a matching Google station identity, grade and current
displayed price. Existing Google places named only Holiday may not match a
Circle K source record until the map's retailer identity is updated.

Timezone boundaries are provided by timezonefinder-data / timezone-boundary-builder,
derived from OpenStreetMap; see those projects for their ODbL attribution and
data licensing. Source data is not relicensed by this repository.

The app downloads a public feed. User locations, trips, Google API keys and Google
prices are never uploaded to this collector. No protected endpoint, embedded site
key, login challenge or paid data plan is used.
