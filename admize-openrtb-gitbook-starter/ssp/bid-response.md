# SSP: Bid Response

- `id`: Mirrors `BidRequest.id`
- `seatbid[]`: Contains one or more `bid[]` items
- Currency `cur` defaults to `USD`

## Bid
- `id`, `impid`, `price` (CPM), `adm` (markup)
- Optional: `adid`, `adomain[]`, `cat[]`, `cid`, `crid`
- `w`, `h` can be extracted from `impid` or set explicitly
- `ext.clicktrackers[]` for click tracking (optional)

## Substitution Macros (examples)
- `${AUCTION_ID}`, `${AUCTION_IMP_ID}`, `${AUCTION_CURRENCY}`, `${AUCTION_PRICE}`, `${AUCTION_PRICE:B64}`, etc.

> Add creative policies, QA, and tracking notes here.
