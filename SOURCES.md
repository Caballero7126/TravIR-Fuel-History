# Automatic station observations

Collection uses public retailer-posted prices, with no driver reports and no
archived Google Places prices. Coverage depends on what each source publishes.
Stations without a matching current price and dated history receive no trend.

- Kwik Trip / Kwik Star: public store catalog and locator price responses at https://www.kwiktrip.com/locator.
- Pilot / Flying J network: public station pages linked from https://pilotcompany.com/fuel-prices. Product codes are preserved. E15 is not treated as regular gasoline. Differing cash/credit prices are excluded.
- Costco / Sam's Club: automatically collected retailer observations published by https://github.com/coatless-data/club-gas-prices. Release digests are checked. The publisher licenses its code under MIT and makes no license claim for retailer-derived data.

Collection times mean "observed on the website", not a confirmed price-change
time. Prices may differ from the pump. Sources are unofficial integrations and
may become unavailable. History uses each station's timezone and compares the
same source, physical station, product, pricing basis, currency and unit.

Timezone boundaries are provided by timezonefinder-data / timezone-boundary-builder,
derived from OpenStreetMap; see those projects for their ODbL attribution and
data licensing. Source data is not relicensed by this repository.

The app downloads a public feed. User locations, trips, Google API keys and Google
prices are never uploaded to this collector. No protected endpoint, embedded site
key, login challenge or paid data plan is used.
