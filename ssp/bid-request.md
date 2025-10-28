# Bid Request

This page describes the bid request format sent from SSPs to Admize.

## BidRequest Object

The top-level bid request object.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Unique ID of the bid request, provided by the Admize exchange | Required | - |
| imp | object array | Array of Imp objects | Required | - |
| app | object | App object. Only applicable and recommended for apps | Optional | - |
| site | object | Site object. Only applicable and recommended for websites | Optional | - |
| device | object | A Device object | Optional | - |
| bcat | string array | Blocked advertiser categories using the IAB content categories | Optional | - |
| badv | string array | Block list of advertisers by their domains (e.g., "ford.com") | Optional | - |
| bapp | string array | Block list of applications by their platform-specific exchange-independent application identifiers. On Android, these should be bundle or package names (e.g., com.foo.mygame). On iOS, these are numeric IDs | Optional | - |
| at | integer | Auction type. 1: first price, 2: second price | Optional | 2 |
| cur | string array | Array of allowed currencies for bids on this bid request using ISO-4217 alpha codes | Optional | USD |

## Imp Object

Describes an ad placement or impression being auctioned.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | A unique identifier for this impression within the context of the bid request | Required | - |
| banner | object | A Banner object | Required* | - |
| native | object | A Native object | Required* | - |
| tagid | string | Identifier for specific ad placement or ad tag that was used to initiate the auction | Required | - |
| instl | integer | 1 = the ad is interstitial or full screen, 0 = not interstitial | Optional | 0 |
| bidfloor | float | Minimum bid for this impression expressed in CPM | Required | - |
| bidfloorcur | string | Currency specified using ISO-4217 alpha codes | Optional | USD |
| secure | integer | Flag to indicate if the impression requires secure HTTPS URL creative assets and markup, where 0 = non-secure, 1 = secure | Optional | 0 |
| displaymanager | string | Name of ad mediation partner, SDK technology, or player responsible for rendering ad. "Admize" as fixed value | Optional | Admize |
| displaymanagerver | string | Version of ad mediation partner, SDK technology, or player. "1.0.0" as fixed value | Optional | 1.0.0 |

\* Must include at least one or more of either banner or native object.

## Banner Object

Describes a banner ad placement.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| w | integer | Width of the impression in pixels | Required | - |
| h | integer | Height of the impression in pixels | Required | - |
| id | string | Unique identifier for this banner object | Optional | - |

## Video Object

Describes a video ad placement.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| mimes | string array | Content MIME types supported (e.g., "video/x-ms-wmv", "video/mp4") | Required | - |
| minduration | integer | Minimum video ad duration in seconds | Required | - |
| maxduration | integer | Maximum video ad duration in seconds | Required | - |
| protocols | integer array | Array of supported video protocols. Refer to List 5.8. At least one supported protocol must be specified. **Admize supports VAST only** | Required | VAST 2.0-4.0 |
| w | integer | Width of the video player in device independent pixels (DIPS) | Optional | - |
| h | integer | Height of the video player in device independent pixels (DIPS) | Optional | - |
| startdelay | integer | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll ad placements | Optional | - |
| placement | integer | Placement type for the impression | Optional | - |
| linearity | integer | Indicates if the impression must be linear, nonlinear, etc. | Optional | - |
| skip | integer | Indicates if the player will allow the video to be skipped, where 0 = no, 1 = yes | Optional | - |
| skipmin | integer | Videos of total duration greater than this number of seconds can be skippable | Optional | - |
| skipafter | integer | Number of seconds a video must play before skipping is enabled | Optional | - |
| sequence | integer | If multiple ad impressions are offered in the same bid request, the sequence number will allow for the coordinated delivery of multiple creatives | Optional | - |
| battr | integer array | Blocked creative attributes | Optional | - |
| maxextended | integer | Maximum extended ad duration if extension is allowed | Optional | - |
| minbitrate | integer | Minimum bit rate in Kbps | Optional | - |
| maxbitrate | integer | Maximum bit rate in Kbps | Optional | - |
| boxingallowed | integer | Indicates if letter-boxing of 4:3 content into a 16:9 window is allowed, where 0 = no, 1 = yes | Optional | - |
| playbackmethod | integer array | Playback methods that may be in use | Optional | - |
| playbackend | integer | The event that causes playback to end | Optional | - |
| delivery | integer array | Supported delivery methods (e.g., streaming, progressive) | Optional | - |
| pos | integer | Ad position on screen | Optional | - |
| companionad | object array | Array of Banner objects if companion ads are available | Optional | - |
| api | integer array | List of supported API frameworks for this impression | Optional | - |
| companiontype | integer array | Supported VAST companion ad types | Optional | - |
| ext | object | Extended video object | Optional | - |

### Video Extension Object

| Attribute | Type | Description | Default |
|-----------|------|-------------|---------|
| rewarded | integer | Indicates rewarded video. 0 = non-rewarded, 1 = rewarded | 0 |

## Native Object

Describes a native ad placement.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| request | string | Request payload complying with the Native Ad Specification | Required | - |
| ver | string | Version of the Dynamic Native Ads API to which request complies | Optional | 1.2 (Admize supports 1.2) |

## App Object

Details about the application.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Exchange-specific app ID | Required | - |
| bundle | string | Application bundle or package name (e.g., com.foo.mygame) | Required | - |
| name | string | App name | Required | - |
| storeurl | string | App store URL for an installed app | Optional | - |
| domain | string | Domain of the app | Optional | - |
| cat | string array | Array of IAB content categories of the app | Optional | - |
| publisher | object | Publisher Object | Optional | - |

## Site Object

Details about the website.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Exchange-specific site ID | Required | - |
| name | string | Site name | Required | - |
| domain | string | Domain of the site | Required | - |
| cat | string array | Array of IAB content categories of the site | Optional | - |
| publisher | object | Publisher Object | Optional | - |

## Publisher Object

Details about the publisher.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Admize publisher ID | Required | - |
| name | string | Publisher name | Optional | - |

## Device Object

Details about the user's device.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| ua | string | Browser user agent string | Optional | - |
| ip | string | IPv4 address closest to device | Optional | - |
| devicetype | integer | The general type of device. Refer to List 5.17 (OpenRTB 2.3) | Optional | - |
| os | string | Device operating system | Optional | - |
| ifa | string | ID sanctioned for advertiser use in the clear (i.e., not hashed) | Optional | - |
| osv | string | Device operating system version (e.g., "3.1.2") | Optional | - |
| make | string | Device make (e.g., "Apple") | Optional | - |
| model | string | Device model (e.g., "iPhone") | Optional | - |
| language | string | Browser language using ISO-639-1-alpha-2 | Optional | - |
| geo | object | A Geo object | Optional | - |
| ext | object | Admize SDK device extensions | Optional | - |

## Geo Object

Geographic information about the user.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| country | string | Country code using ISO-3166-1-alpha-3 | Optional | - |
| city | string | City name | Optional | - |

## Device Extension Object

Extended device information.

| Attribute | Type | Description | Default |
|-----------|------|-------------|---------|
| emulator | integer | 1 = emulator, 0 = not emulator | 0 |
