# atlas

Symbol reference data and identifying marks for listed equities, ETFs and
digital assets.

- **101,807** logo images across **64 exchanges** plus crypto
- **92,430** symbols with name, exchange, region, currency and instrument type

## Layout

```
logos/<EXCHANGE>/<SYMBOL>.png     e.g. logos/NASDAQ/AAPL.png
logos/crypto/<BASE>.png           e.g. logos/crypto/BTC.png
symbols/<market>.json             e.g. symbols/japan.json
symbols/by-exchange/<EXCHANGE>.json
manifest.json                     counts and per-exchange index
```

Logos are keyed by exchange because a ticker is only unique within one. More
than 10,000 symbols appear on multiple exchanges and around 3,200 of those are
different companies, so a flat ticker-keyed layout cannot be correct.

Crypto is the deliberate exception: a logo belongs to the base asset rather
than the venue, so all exchanges share one image per asset.

## Filename rule

Alphanumerics and `.` `-` `_` pass through unchanged. Every other character
becomes `-`. This affects roughly 1,500 symbols containing `/`, `!` or `&`.

```
BET:FORRAS/OE  ->  logos/BET/FORRAS-OE.png
NSE:ARE&M      ->  logos/NSE/ARE-M.png
```

Consumers must apply the identical mapping or lookups will 404.

## Symbol records

```json
{
  "symbol": "AAPL",
  "name": "Apple Inc.",
  "exchange": "NASDAQ",
  "exchangeName": "Nasdaq",
  "date": "2026-08-09",
  "type": "cs",
  "region": "US",
  "currency": "USD",
  "isEnabled": true,
  "logoid": "apple",
  "logoFile": "NASDAQ/AAPL.png"
}
```

`logoFile` is present only when the image exists, so it doubles as a coverage
flag. Resolve a logo by joining it to the `logos/` root.

## Coverage

| Segment | Coverage |
| --- | --- |
| Equities and ETFs | 91,006 / 92,430 (98.5%) |
| Crypto base assets | 6,287 / 11,975 (52.5%) |

Most exchanges are between 97% and 100%. Crypto is lower because the long
tail of micro-cap tokens has no published mark.

`logos/_ledger/` records the outcome for every symbol attempted, including
those with no logo available, so a regeneration does not retry known misses.

## Notice

The images are the trademarks of their respective owners, included for
identification only. See [NOTICE](NOTICE). Removal requests are honoured on
request via an issue.
