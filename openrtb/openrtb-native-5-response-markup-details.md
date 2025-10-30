# 5 Native Ad Response Markup Details

The structure and contents of the Bid Response are the same as in the OpenRTB standard. The difference is in how the ad creative is returned. The native creative shall be returned as a JSON-encoded string in the adm field of the Bid Object. Note some implementers have chosen to use a direct object in a new field rather than JSON encoded string.

## 5.1 Native Markup Response Object

The native object is the top level JSON object which identifies a native response. The native object has following attributes:

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| ver | string | Recommended | "1.2" | Version of the Native Markup version in use. |
| assets | object array | Recommended | - | List of native ad's assets. Required if no assetsurl. Recommended as fallback even if assetsurl is provided. |
| assetsurl¹ | string | Optional | - | URL of an alternate source for the assets object. The expected response is a JSON object mirroring the assets object in the bid response, subject to certain requirements as specified in the individual objects. Where present, overrides the asset object in the response. |
| dcourl | string | Optional | - | URL where a dynamic creative specification may be found for populating this ad, per the Dynamic Content Ads Specification. Note this is a beta option as the interpretation of the Dynamic Content Ads Specification and how to assign those elements into a native ad is outside the scope of this spec and must be agreed offline between the parties or as may be specified in a future revision of the Dynamic Content Ads spec. Where present, overrides the asset object in the response. |
| link | object | Required | - | Destination Link. This is default link object for the ad. Individual assets can also have a link object which applies if the asset is activated(clicked). If the asset doesn't have a link object, the parent link object applies. See LinkObject Definition |
| imptrackers | string array | Optional | - | Array of impression tracking URLs, expected to return a 1x1 image or 204 response - typically only passed when using 3rd party trackers. To be deprecated - replaced with eventtrackers. |
| jstracker | string | Optional | - | Optional JavaScript impression tracker. This is a valid HTML, Javascript is already wrapped in `<script>` tags. It should be executed at impression time where it can be supported. To be deprecated - replaced with eventtrackers. |
| eventtrackers | object array | Optional | - | Array of tracking objects to run with the ad, in response to the declared supported methods in the request. Replaces imptrackers and jstracker, to be deprecated. |
| privacy | string | Optional | - | If support was indicated in the request, URL of a page informing the user about the buyer's targeting activity. |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

**¹** The provided "assetsurl" or "dcourl" should be expected to provide a valid response when called in any context, including importantly the brand name and example thumbnails and headlines (to use for reporting, blacklisting, etc), but it is understood the final actual call should come from the client device from which the ad will be rendered to give the buyer the benefit of the cookies and header data available in that context.

**Note:** Prior to VERSION 1.1, the native response's root node was an object with a single field "native" that would contain the object above as its value. The Native Object specified above is now the root object.

**Note re: assetsurl format responses:** In the case of assetsurl or dcourl (beta) bidding, since the ultimate buyer/creative engine cannot alter the assets response based on the details inside the assets request (as it does not receive said request), it is critical that all required assets are provided, and such communications will need to be handled offline for recommended/optional elements.

In the normal embedded response, certain attributes of the response are assumed based on matching the ID of the asset object in the response to the ID of the asset object in the request. Since the asset response will not be reading the asset request directly in this implementation, that information is added as option in the below object definitions and marked for that use case.

It is also recommended that where the standard specifies multiple options for an element, that all options be provided. IE all 4 supported thumbnail aspect ratios and all 3 supported title lengths.

The ID component of the asset responses can be omitted.

Note that this change to provide the metadata description of the asset in the response, rather than using the asset ID to implicitly specify that, may be reflected into the inline version of responses in a future version to align the two methods of replying. Making that change now would break backwards compatibility of the inline response mechanism.

## 5.2 Asset Response Object

Corresponds to the Asset Object in the request. The main container object for each asset requested or supported by Exchange on behalf of the rendering client. Any object that is required is to be flagged as such. Only one of the {title,img,video,data} objects should be present in each object. All others should be null/absent. The id is to be unique within the AssetObject array so that the response can be aligned.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| id | integer | Optional | - | Optional if assetsurl/dcourl is being used; required if embedded asset is being used. |
| required | integer | Optional | 0 | Set to 1 if asset is required. (bidder requires it to be displayed). |
| title | object | Optional¹ | - | Title object for title assets. See TitleObject definition. |
| img | object | Optional¹ | - | Image object for image assets. See ImageObject definition. |
| video | object | Optional¹ | - | Video object for video assets. See Video response object definition. Note that in-stream video ads are not part of Native. Native ads may contain a video as the ad creative itself. |
| data | object | Optional¹ | - | Data object for ratings, prices etc. |
| link | object | Optional | - | Link object for call to actions. The link object applies if the asset item is activated (clicked). If there is no link object on the asset, the parent link object on the bid response applies. |
| ext² | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

**¹:** asset object may contain only one of title, img, data or video.

**²:** Bidders are encouraged not to use asset.ext for exchanging text assets. Use data.ext with custom type instead.

## 5.3 Title Response Object

Corresponds to the Title Object in the request, with the value filled in.

If using assetsurl or dcourl response rather than embedded asset response, it is recommended that three title objects be provided, the length of each of which is less than or equal to the three recommended maximum title lengths (25,90,140).

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| text | string | Required | - | The text associated with the text element. |
| len | integer | Optional | - | The length of the title being provided. Required if using assetsurl/dcourl representation, optional if using embedded asset representation. |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

## 5.4 Image Response Object

Corresponds to the Image Object in the request. The Image object to be used for all image elements of the Native ad such as Icons, Main Image, etc.

It is recommended that if assetsurl/dcourl is being used rather than embedded assets, that an image of each recommended aspect ratio (per the Image Types table) be provided for image type 3.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| type | integer | Optional | - | Required for assetsurl or dcourl responses, not required for embedded asset responses. The type of image element being submitted from the Image Asset Types table. |
| url | string | Required | - | URL of the image asset. |
| w | integer | Recommended | - | Width of the image in pixels. Recommended for embedded asset responses. Required for assetsurl/dcourl responses if multiple assets of same type submitted. |
| h | integer | Recommended | - | Height of the image in pixels. Recommended for embedded asset responses. Required for assetsurl/dcourl responses if multiple assets of same type submitted. |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

## 5.5 Data Response Object

Corresponds to the Data Object in the request, with the value filled in. The Data Object is to be used for all miscellaneous elements of the native unit such as Brand Name, Ratings, Review Count, Stars, Downloads, Price count etc. It is also generic for future native elements not contemplated at the time of the writing of this document.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| type | integer | Optional | - | Required for assetsurl/dcourl responses, not required for embedded asset responses. The type of data element being submitted from the Data Asset Types table. |
| len | integer | Optional | - | Required for assetsurl/dcourl responses, not required for embedded asset responses. The length of the data element being submitted. Where applicable, must comply with the recommended maximum lengths in the Data Asset Types table. |
| value | string | Required | - | The formatted string of data to be displayed. Can contain a formatted value such as "5 stars" or "$10" or "3.4 stars out of 5". |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

## 5.6 Video Response Object

Corresponds to the Video Object in the request, yet containing a value of a conforming VAST tag as a value.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| vasttag | string | Required | - | vast xml. |

## 5.7 Link Response Object

Used for 'call to action' assets, or other links from the Native ad. This Object should be associated to its peer object in the parent Asset Object or as the master link in the top level Native Ad response object. When that peer object is activated (clicked) the action should take the user to the location of the link.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| url | string | Required | - | Landing URL of the clickable link. |
| clicktrackers | string array | Optional | - | List of third-party tracker URLs to be fired on click of the URL. |
| fallback | string (URL) | Optional | - | Fallback URL for deeplink. To be used if the URL given in url is not supported by the device. |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |

## 5.8 Event Tracker Response Object

The event trackers response is an array of objects and specifies the types of events the bidder wishes to track and the URLs/information to track them. Bidder must only respond with methods indicated as available in the request. Note that most javascript trackers expect to be loaded at impression time, so it's not generally recommended for the buyer to respond with javascript trackers on other events, but the appropriateness of this is up to each buyer.

| Attribute | Type | Require/Optional | Default | Description |
|-----------|------|------------------|---------|-------------|
| event | integer | Required | - | Type of event to track. See Event Types table. |
| method | integer | Required | - | Type of tracking requested. See Event Tracking Methods table. |
| url | string | Optional | - | The URL of the image or js. Required for image or js, optional for custom. |
| customdata | object containing key:value pairs | Optional | - | To be agreed individually with the exchange, an array of key:value objects for custom tracking, for example the account number of the DSP with a tracking company. IE {"accountnumber":"123"}. |
| ext | object | Optional | - | This object is a placeholder that may contain custom JSON agreed to by the parties to support flexibility beyond the standard defined in this specification |
