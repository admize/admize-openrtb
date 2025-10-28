# Native Specification

Admize supports OpenRTB Dynamic Native Ads API Specification Version 1.2.

**Note**: Admize currently does not support Native Video Asset Objects.

## Request Object

Native ad request object embedded in the bid request.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| ver | string | Version of the Native Markup version in use | Optional | - |
| context | integer | The context in which the ad appears. See Context Type IDs table | Recommended | - |
| contextsubtype | integer | A more detailed context. See Context Sub Type IDs table | Optional | - |
| plcmttype | integer | The design/format/layout of the ad unit. See Placement Type IDs table | Recommended | - |
| plcmtcnt | integer | The number of identical placements in this layout | Recommended | - |
| seq | integer | 0 for the first ad, 1 for the second ad, and so on | Optional | Admize does not support |
| assets | object array | Array of Asset Objects. Any bid response must comply with the array of elements expressed in the bid request | Required | - |
| aurlsupport | integer | Whether the supply source/impression supports returning an assetsurl instead of an asset object. 0 or absence indicates no support | Optional | Admize does not support |
| durlsupport | integer | Whether the supply source/impression supports returning a dco url. 0 or absence indicates no support | Optional | Admize does not support |
| eventtrackers | object array | Specifies what type of event tracking is supported | Optional | - |
| privacy | integer | Set to 1 when the native ad supports buyer-specific privacy notice. Set to 0 (or absent) when it doesn't | Recommended | - |

## Asset Request Object

**Note**: Admize currently does not support native video assets.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | integer | Unique asset ID, assigned by exchange. Typically a counter for the array | Required | - |
| required | integer | Set to 1 if asset is required (exchange will not accept a bid without it) | Optional | - |
| title | object | Title object for title assets | Recommended | - |
| img | object | Image object for image assets | Recommended | - |
| video | object | Video object for video assets | Optional | Admize does not support |
| data | object | Data object for brand name, description, ratings, prices, etc. | Recommended | - |

### Title Request Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| len | integer | Maximum length of the text in the title element. Recommended to be 25, 90, or 140 | Required | - |

### Image Request Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| type | integer | Type ID of the image element. See Image Asset Types table | Optional | - |
| w | integer | Width of the image in pixels | Optional | - |
| wmin | integer | The minimum requested width of the image in pixels. Either w or wmin should be transmitted | Recommended | - |
| h | integer | Height of the image in pixels | Optional | - |
| hmin | integer | The minimum requested height of the image in pixels. Either h or hmin should be transmitted | Recommended | - |
| mimes | string array | Whitelist of content MIME types supported (e.g., "image/jpg", "image/gif") | Optional | - |

### Data Request Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| type | integer | Type ID of the element. See Data Asset Types table | Required | - |
| len | integer | Maximum length of the text in the element's response | Optional | - |

### Event Trackers Request Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| events | integer | Type of event available for tracking. See Event Types table | Required | - |
| methods | integer array | Array of the types of tracking available for the given event. See Event Tracking Methods table | Required | - |

## Response Object

Native ad response object returned in the bid response.

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| ver | string | Version of the Native Markup version in use | Recommended | Admize supports 1.2 |
| assets | object array | List of native ad's assets | Recommended | - |
| assetsurl | string | URL of an alternate source for the assets object | Optional | Admize does not support |
| dcourl | string | URL where a dynamic creative specification may be found | Optional | Admize does not support |
| link | object | Destination Link. This is default link object for the ad | Required | - |
| imptrackers | object array | Array of impression tracking URLs | Optional | - |
| jstrackers | string | Optional JavaScript impression tracker | Optional | Admize does not support |
| eventtrackers | object array | Array of tracking objects to run with the ad | Optional | Admize supports conditionally (only img type) |
| privacy | string | URL of a page informing the user about the buyer's targeting activity | Optional | - |

## Asset Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| id | integer | Asset ID (optional if assetsurl/dcourl is used) | Optional | - |
| required | integer | Set to 1 if asset is required | Optional | - |
| title | object | Title object for title assets | Optional | - |
| img | object | Image object for image assets | Optional | - |
| video | object | Video object for video assets | Optional | Admize does not support |
| data | object | Data object for ratings, prices, etc. | Optional | - |
| link | object | Link object for call to actions | Optional | - |

### Title Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| text | string | The text associated with the text element | Required | - |
| len | integer | The length of the title being provided | Optional | - |

### Image Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| type | integer | The type of image element being submitted | Optional | - |
| url | string | URL of the image asset | Required | - |
| w | integer | Width of the image in pixels | Recommended | - |
| h | integer | Height of the image in pixels | Recommended | - |

### Data Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| type | integer | The type of data element being submitted | Optional | - |
| len | integer | The length of the data element being submitted | Optional | - |
| value | string | The formatted string of data to be displayed (e.g., "5 stars", "$10") | Required | - |

### Link Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| url | string | Landing URL of the clickable link | Required | - |
| clicktrackers | string array | List of third-party tracker URLs to be fired on click | Optional | - |
| fallback | string | Fallback URL for deeplink | Optional | - |

### Event Tracker Response Object

| Attribute | Type | Description | Required/Optional | Default |
|-----------|------|-------------|-------------------|---------|
| event | integer | Type of event to track. See Event Types table | Required | - |
| method | integer | Type of tracking requested. See Event Tracking Methods table | Required | - |
| url | string | The URL of the image or js | Optional | - |
| customdata | object (key:value) | Array of key:value objects for custom tracking | Optional | - |

## Reference & Enumeration

### Context Type IDs

| ID | Description |
|----|-------------|
| 1 | Content-centric context such as newsfeed, article, image gallery, video gallery, or similar |
| 2 | Social-centric context such as social network feed, email, chat, or similar |
| 3 | Product context such as product listings, details, recommendations, reviews, or similar |

### Context Sub Type IDs

| ID | Description |
|----|-------------|
| 10 | General or mixed content |
| 11 | Primarily article content |
| 12 | Primarily video content |
| 13 | Primarily audio content |
| 14 | Primarily image content |
| 15 | User-generated content - forums, comments, etc. |
| 20 | General social content such as a general social network |
| 21 | Primarily email content |
| 22 | Primarily chat/IM content |
| 30 | Content focused on selling products, whether digital or physical |
| 31 | Application store/marketplace |
| 32 | Product reviews site primarily (which may sell product secondarily) |

### Placement Type IDs

| ID | Description |
|----|-------------|
| 1 | In the feed of content |
| 2 | In the atomic unit of the content |
| 3 | Outside the core content |
| 4 | Recommendation widget |

### Image Asset Types

| ID | Name | Description |
|----|------|-------------|
| 1 | Icon | Icon Image |
| 3 | Main | Ad Image |

### Data Asset Types

| ID | Name |
|----|------|
| 1 | sponsored |
| 2 | desc |
| 3 | rating |
| 4 | likes |
| 5 | downloads |
| 6 | price |
| 7 | saleprice |
| 8 | phone |
| 9 | address |
| 10 | desc2 |
| 11 | displayurl |
| 12 | ctatext |

### Event Types

| ID | Name | Description | Default |
|----|------|-------------|---------|
| 1 | Impression | Impression | - |
| 2 | viewable-mrc50 | Visible impression using MRC definition at 50% in view for 1 second | Admize does not support |
| 3 | viewable-mrc100 | 100% in view for 1 second (GroupM standard) | Admize does not support |
| 4 | viewable-video50 | Visible impression for video using MRC definition at 50% in view for 2 seconds | Admize does not support |

### Event Tracking Methods

| ID | Name | Default |
|----|------|---------|
| 1 | img | - |
| 2 | js | Admize does not support |
