# Object Specifications

The subsections that follow define each of the objects in the bid response model. Several conventions are used throughout:

- Attributes are "required" if their omission would technically break the protocol.
- Some optional attributes are denoted "recommended" due to their elevated business importance.
- Unless a default value is explicitly specified, an omitted attribute is interpreted as "unknown".

## 1 Object: BidResponse

This object is the top-level bid response object (i.e., the unnamed outer JSON object). The `id` attribute is a reflection of the bid request ID for logging purposes. Similarly, `bidid` is an optional response tracking ID for bidders. If specified, it can be included in the subsequent win notice call if the bidder wins. At least one seatbid object is required, which contains at least one bid for an impression. Other attributes are optional.

To express a "no-bid", the options are to return an empty response with HTTP 204. Alternately if the bidder wishes to convey to the exchange a reason for not bidding, just a BidResponse object is returned with a reason code in the nbr attribute.

| Attribute | Type | Required/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| id | string | Required | - | ID of the bid request to which this is a response. |
| seatbid | object array | Required | - | Array of seatbid objects; 1+ required if a bid is to be made. |
| bidid | string | Optional | - | Bidder generated response ID to assist with logging/tracking. |
| cur | string | Optional | "USD" | Bid currency using ISO-4217 alpha codes. |
| customdata | string | Optional | - | Optional feature to allow a bidder to set data in the exchange's cookie. The string must be in base85 cookie safe characters and be in any format. Proper JSON encoding must be used to include "escaped" quotation marks. |
| nbr | integer | Optional | - | Reason for not bidding. Refer to List 5.24. |
| ext | object | Optional | - | Placeholder for bidder-specific extensions to OpenRTB. |

## 2 Object: SeatBid

A bid response can contain multiple SeatBid objects, each on behalf of a different bidder seat and each containing one or more individual bids. If multiple impressions are presented in the request, the `group` attribute can be used to specify if a seat is willing to accept any impressions that it can win (default) or if it is only interested in winning any if it can win them all as a group.

| Attribute | Type | Required/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| bid | object array | Required | - | Array of 1+ Bid objects (Section 3) each related to an impression. Multiple bids can relate to the same impression. |
| seat | string | Optional | - | ID of the buyer seat (e.g., advertiser, agency) on whose behalf this bid is made. |
| group | integer | Optional | 0 | 0 = impressions can be won individually; 1 = impressions must be won or lost as a group. |
| ext | object | Optional | - | Placeholder for bidder-specific extensions to OpenRTB. |

## 3 Object: Bid

A SeatBid object contains one or more Bid objects, each of which relates to a specific impression in the bid request via the `impid` attribute and constitutes an offer to buy that impression for a given price.

| Attribute | Type | Required/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| id | string | Required | - | Bidder generated bid ID to assist with logging/tracking. |
| impid | string | Required | - | ID of the Imp object in the related bid request. |
| price | float | Required | - | Bid price expressed as CPM although the actual transaction is for a unit impression only. Note that while the type indicates float, integer math is highly recommended when handling currencies (e.g., BigDecimal in Java). |
| nurl | string | Optional | - | Win notice URL called by the exchange if the bid wins (not necessarily indicative of a delivered, viewed, or billable ad); optional means of serving ad markup. Substitution macros (Section 4.4) may be included in both the URL and optionally returned markup. |
| burl | string | Optional | - | Billing notice URL called by the exchange when a winning bid becomes billable based on exchange-specific business policy (e.g., typically delivered, viewed, etc.). Substitution macros (Section 4.4) may be included. |
| lurl | string | Optional | - | Loss notice URL called by the exchange when a bid is known to have been lost. Substitution macros (Section 4.4) may be included. Exchange-specific policy may preclude support for loss notices or the disclosure of winning clearing prices resulting in ${AUCTION_PRICE} macros being removed (i.e., replaced with a zero-length string). |
| adm | string | Optional | - | Optional means of conveying ad markup in case the bid wins; supersedes the win notice if markup is included in both. Substitution macros (Section 4.4) may be included. |
| adid | string | Optional | - | ID of a preloaded ad to be served if the bid wins. |
| adomain | string array | Optional | - | Advertiser domain for block list checking (e.g., "ford.com"). This can be an array of for the case of rotating creatives. Exchanges can mandate that only one domain is allowed. |
| bundle | string | Optional | - | A platform-specific application identifier intended to be unique to the app and independent of the exchange. On Android, this should be a bundle or package name (e.g., com.foo.mygame). On iOS, it is a numeric ID. |
| iurl | string | Optional | - | URL without cache-busting to an image that is representative of the content of the campaign for ad quality/safety checking. |
| cid | string | Optional | - | Campaign ID to assist with ad quality checking; the collection of creatives for which iurl should be representative. |
| crid | string | Optional | - | Creative ID to assist with ad quality checking. |
| tactic | string | Optional | - | Tactic ID to enable buyers to label bids for reporting to the exchange the tactic through which their bid was submitted. The specific usage and meaning of the tactic ID should be communicated between buyer and exchanges a priori. |
| cat | string array | Optional | - | IAB content categories of the creative. Refer to List 5.1. |
| attr | integer array | Optional | - | Set of attributes describing the creative. Refer to List 5.3. |
| api | integer | Optional | - | API required by the markup if applicable. Refer to List 5.6. |
| protocol | integer | Optional | - | Video response protocol of the markup if applicable. Refer to List 5.8. |
| qagmediarating | integer | Optional | - | Creative media rating per IQG guidelines. Refer to List 5.19. |
| language | string | Optional | - | Language of the creative using ISO-639-1-alpha-2. The non-standard code "xx" may also be used if the creative has no linguistic content (e.g., a banner with just a company logo). |
| dealid | string | Optional | - | Reference to the deal.id from the bid request if this bid pertains to a private marketplace direct deal. |
| w | integer | Optional | - | Width of the creative in device independent pixels (DIPS). |
| h | integer | Optional | - | Height of the creative in device independent pixels (DIPS). |
| wratio | integer | Optional | - | Relative width of the creative when expressing size as a ratio. Required for Flex Ads. |
| hratio | integer | Optional | - | Relative height of the creative when expressing size as a ratio. Required for Flex Ads. |
| exp | integer | Optional | - | Advisory as to the number of seconds the bidder is willing to wait between the auction and the actual impression. |
| ext | object | Optional | - | Placeholder for bidder-specific extensions to OpenRTB. |

## 3-1 Object: Bid.Ext

| Attribute | Type | Required/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| clicktrackers | string array | Optional | - | ClickTracking Url. |

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