# Bid Response

This page describes the bid response format that DSPs should return to Admize.

## BidResponse Object

The top-level bid response object.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | ID of the bid request to which this is a response | Required | - |
| seatbid | object array | Array of seatbid objects; 1+ required if a bid is to be made | Required | - |
| cur | string | Bid currency using ISO-4217 alpha codes | Optional | USD |

## Seatbid Object

A collection of bids made by the bidder.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| bid | object array | Array of 1+ Bid objects, each related to an impression. Multiple bids can relate to the same impression | Required | - |
| seat | string | ID of the bidder seat on whose behalf this bid is made | Optional | - |

## Bid Object

Details about a specific bid.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Bidder generated bid ID to assist with logging/tracking | Required | - |
| impid | string | ID of the Imp object in the related bid request | Required | - |
| price | float | Bid price expressed as CPM | Required | - |
| adid | string | Ad ID | Optional | - |
| adm | string | Ad markup | Required | - |
| adomain | string/array | Advertiser domain | Optional | - |
| cat | string/array | Array of IAB content categories of the ad | Optional | - |
| cid | string | Campaign ID to assist with ad quality checking | Required | - |
| crid | string | Creative ID to assist with ad quality checking | Optional | - |
| w | integer | Width of the creative in pixels (extracted from impid, e.g., 320x50 → 320) | Optional | - |
| h | integer | Height of the creative in pixels (extracted from impid, e.g., 320x50 → 50) | Optional | - |
| nurl | string | Win notice URL called by the exchange if the bid wins; optional means of serving ad markup | Optional | - |
| burl | string | Billing notice URL called by the exchange when a winning bid becomes billable based on exchange-specific business policy | Optional | - |
| lurl | string | Loss notice URL called by the exchange when a bid is known to have been lost | Optional | - |

## Win, Billing, and Loss Notifications

### Win Notice (nurl)
Called when the bid wins the auction. Use this for:
- Confirming the win
- Final ad serving decisions
- Internal tracking

### Billing Notice (burl)
Called when the impression becomes billable (typically after viewability confirmation). Use this for:
- Confirming billable impressions
- Financial reconciliation

### Loss Notice (lurl)
Called when the bid loses the auction. Use this for:
- Understanding competition
- Bid optimization
- Loss analysis

## Substitution Macros

Macros that can be used in URLs for tracking and reporting.

| Macro | Description |
|-------|-------------|
| ${AUCTION_ID} | ID of the bid request; from BidRequest.id attribute |
| ${AUCTION_SEAT_ID} | ID of the bidder seat for whom the bid was made |
| ${AUCTION_AD_ID} | ID of the ad markup the bidder wishes to serve; from bid.adid attribute |
| ${AUCTION_BID_ID} | ID of the bid; from BidResponse.bidid attribute |
| ${AUCTION_IMP_ID} | ID of the impression just won; from imp.id attribute |
| ${AUCTION_CURRENCY} | The currency used in the bid (explicit or implied); for confirmation only |
| ${AUCTION_PRICE} | Clearing price using the same currency and units as the bid |
| ${AUCTION_PRICE:B64} | Base64 encoded clearing price |

## Usage Example

### Simple Response

```json
{
  "id": "1-1701305999872-3223-7338-625196",
  "seatbid": [
    {
      "bid": [
        {
          "id": "1-1644894781441-161-23-2446841",
          "impid": "06a5f7ca-0f13-4ae1-6a6e-15ffef02c650",
          "price": 0.3068,
          "adid": "495E8194:1644894781:0363905980",
          "adm": "<creative markup here>",
          "adomain": ["example.com"],
          "cid": "23501",
          "crid": "454651",
          "cat": ["IAB1-1"],
          "w": 320,
          "h": 50
        }
      ]
    }
  ]
}
```

### Response with Notification URLs

```json
{
  "id": "1-1701305999872-3223-7338-625196",
  "seatbid": [
    {
      "bid": [
        {
          "id": "1-1644894781441-161-23-2446841",
          "impid": "06a5f7ca-0f13-4ae1-6a6e-15ffef02c650",
          "price": 0.3068,
          "adm": "<creative markup here>",
          "cid": "23501",
          "nurl": "https://dsp.example.com/win?id=${AUCTION_BID_ID}&price=${AUCTION_PRICE}",
          "burl": "https://dsp.example.com/bill?id=${AUCTION_BID_ID}&price=${AUCTION_PRICE}",
          "lurl": "https://dsp.example.com/loss?id=${AUCTION_BID_ID}"
        }
      ]
    }
  ]
}
```
