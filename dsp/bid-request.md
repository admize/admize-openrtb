# Bid Request

This page describes the bid request format sent from Admize to DSPs.

## Request Header

HTTP headers sent with each bid request:

- `x-openrtb-version`: 2.3, 2.5
- `Accept-Encoding`: gzip
- `Content-Type`: application/json
- `Content-Encoding`: gzip (only for DSPs who support gzip compression)
- `Content-Length`: [request body length]

## BidRequest Object

The top-level bid request object.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Unique ID of the bid request, provided by the Admize exchange | Required | - |
| imp | object array | Array of Imp objects | Required | - |
| app | object | App object. Only applicable and recommended for apps | Optional | - |
| site | object | Site object. Only applicable and recommended for websites | Optional | - |
| device | object | A Device object | Required | - |
| regs | object | A Regs object | Optional | - |
| source | object | A Source object | Optional | - |
| bcat | string array | Blocked advertiser categories using the IAB content categories | Optional | - |
| badv | string array | Block list of advertisers by their domains (e.g., "ford.com") | Optional | - |
| bapp | string array | Block list of applications by their platform-specific exchange-independent application identifiers. On Android, bundle or package names (e.g., com.foo.mygame). On iOS, numeric IDs | Optional | - |
| tmax | integer | Maximum time in milliseconds the exchange allows for bids including Internet latency to avoid timeout | Optional | - |
| at | integer | Auction type. 2: second price, 1: first price | Optional | 2 |
| cur | string array | Array of allowed currencies for bids using ISO-4217 alpha codes | Optional | USD |

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
| displaymanager | string | Name of ad mediation partner, SDK technology, or player. "Admize" as fixed value | Optional | Admize |
| displaymanagerver | string | Version of ad mediation partner, SDK technology, or player. "1.0.0" as fixed value | Optional | 1.0.0 |

\* Must include at least one or more of either banner or native object.

## Banner Object

Describes a banner ad placement.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| w | integer | Width of the impression in pixels | Required | - |
| h | integer | Height of the impression in pixels | Required | - |
| id | string | Unique identifier for this banner object | Optional | - |

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
| publisher | object | Publisher Object | Required | - |

## Site Object

Details about the website.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | string | Exchange-specific site ID | Required | - |
| name | string | Site name | Required | - |
| domain | string | Domain of the site | Required | - |
| cat | string array | Array of IAB content categories of the site | Optional | - |
| publisher | object | Publisher Object | Required | - |

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
| os | string | Device operating system | Required | - |
| ifa | string | ID sanctioned for advertiser use in the clear (i.e., not hashed) | Optional | - |
| osv | string | Device operating system version (e.g., "3.1.2") | Optional | - |
| make | string | Device make (e.g., "Apple") | Optional | - |
| model | string | Device model (e.g., "iPhone") | Optional | - |
| language | string | Browser language using ISO-639-1-alpha-2 | Optional | - |
| connectiontype | integer | Network connection type | Optional | - |
| geo | object | A Geo object | Optional | - |
| ext | object | Admize SDK device extensions | Optional | - |

## Geo Object

Geographic information about the user.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| country | string | Country code using ISO-3166-1-alpha-3 | Optional | - |
| city | string | City name | Optional | - |

## Regs Object

Regulatory information.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| coppa | integer | Flag indicating if this request is subject to COPPA regulations (USA FTC), where 0 = no, 1 = yes | Optional | - |

## Source Object

Details about the inventory source.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| ext | object | A SourceExt object (schain data) | Optional | - |

## SourceExt Object

Extended source information including supply chain.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| schain | object | Admize schain Object (Refer to OpenRTB SupplyChain object) | Optional | - |

### Supply Chain (schain) Example

```json
{
  "source": {
    "ext": {
      "schain": {
        "ver": "1.0",
        "complete": 1,
        "nodes": [
          {
            "asi": "cauly.net",
            "sid": "6374",
            "hp": 1
          },
          {
            "asi": "center.Admize.io",
            "sid": "p_1875135558794156",
            "hp": 1
          }
        ]
      }
    }
  }
}
```

The schain object provides transparency about the supply chain for the ad impression, showing each intermediary involved in the transaction.
