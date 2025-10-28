# SSP Integration Guide

This guide is for Supply-Side Platforms (SSPs) integrating with Admize as a demand partner.

## Overview

The Admize OpenRTB integration for SSPs supports:

- **OpenRTB Versions**: 2.3 to 2.5
- **Native Ads**: OpenRTB Dynamic Native Ads API Specification Version 1.2
- **Ad Formats**: Banner, Video, Native

## Integration Flow

1. **Bid Request**: SSP sends bid requests to Admize
2. **Bid Response**: Admize responds with bids
3. **Ad Serving**: Winning ads are served to end users
4. **Tracking**: Impression and click tracking

## Supported Features

### Ad Formats
- Banner ads (standard IAB sizes)
- Video ads (VAST 2.0-4.0)
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

## Quick Start

1. Review the [Bid Request](bid-request.md) specification
2. Understand the [Bid Response](bid-response.md) format
3. For native ads, see [Native Specification](native-spec.md)
4. Check [Examples](examples.md) for sample requests and responses

## Technical Requirements

- HTTPS endpoint required
- JSON format
- UTF-8 encoding
- Timeout: 100ms default (configurable via tmax)

## Standard References

- [OpenRTB 2.5 Specification](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-5-FINAL.pdf)
- [OpenRTB Native Ads 1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf)
