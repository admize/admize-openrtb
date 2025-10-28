# Bid Response

This page describes the bid response format returned by Admize to SSPs.

## BidResponse Object

The top-level bid response object.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | ID of the bid request to which this is a response | Required | - |
| seatbid | object array | Array of seatbid objects; 1+ required if a bid is to be made | Required | - |

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
| w | integer | Width of the creative in pixels (extracted from impid, e.g., 320x50 → 320) | Required | - |
| h | integer | Height of the creative in pixels (extracted from impid, e.g., 320x50 → 50) | Required | - |
| ext | object | Extended bid object for click tracking | Optional | - |

## Bid Extension Object

Extended information for the bid.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| clicktrackers | string/array | Click tracking URL(s) | Optional | - |

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

Macros are typically used in impression tracking URLs:

```
https://test-event.admize.io/imp/ssp/v1/1-1644894781441-161-23-2446841?ap=${AUCTION_PRICE}
```

When the ad wins, the macro will be replaced with the actual auction price before the URL is called.
