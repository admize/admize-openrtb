# DSP Integration Guide

This guide is for Demand-Side Platforms (DSPs) integrating with Admize as a supply partner.

## Overview

The Admize OpenRTB integration for DSPs supports:

- **OpenRTB Versions**: 2.3 to 2.5
- **Native Ads**: OpenRTB Dynamic Native Ads API Specification Version 1.2
- **Ad Formats**: Banner, Native

## Integration Flow

1. **Bid Request**: Admize sends bid requests to DSP
2. **Bid Response**: DSP responds with bids
3. **Ad Serving**: Winning ads are served to end users
4. **Tracking**: Impression, click, and win/loss notifications

## Supported Features

### Ad Formats
- Banner ads (standard IAB sizes)
- Native ads (OpenRTB Native 1.2)

### Targeting
- Geographic targeting
- Device targeting
- App/Site targeting
- Category blocking
- Advertiser blocking

### Auction Types
- First-price auction (at=1)
- Second-price auction (at=2, default)

### Additional Features
- Supply Chain Object (schain) support
- COPPA compliance
- Win/Loss notifications (nurl, burl, lurl)

## Quick Start

1. Review the [Bid Request](bid-request.md) specification
2. Understand the [Bid Response](bid-response.md) format
3. For native ads, see [Native Specification](native-spec.md)
4. Check [Examples](examples.md) for sample requests and responses

## Technical Requirements

### Request Headers
- `x-openrtb-version`: 2.3 or 2.5
- `Accept-Encoding`: gzip
- `Content-Type`: application/json
- `Content-Encoding`: gzip (optional, for DSPs supporting compression)
- `Content-Length`: [request body length]

### Response Requirements
- JSON format
- UTF-8 encoding
- HTTPS creative URLs (secure=1)
- Timeout: Specified in bid request tmax field (default 100ms)

## Standard References

- [OpenRTB 2.5 Specification](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-5-FINAL.pdf)
- [OpenRTB Native Ads 1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf)
- [OpenRTB Supply Chain Specification](https://iabtechlab.com/ads-txt/)
