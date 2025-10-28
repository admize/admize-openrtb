# SSP: Bid Request

## Required/Recommended Objects
- `id` (string): Unique request ID.
- `imp[]` (array): One or more impressions (`banner` or `native` required).
- `app` or `site` (recommended).
- `device` (optional).
- Optional brand/app/category blocks: `badv[]`, `bapp[]`, `bcat[]`.
- Auction type `at` default **2** (second price). Currency `cur` default **USD**.

## `imp` Object (banner/native)
- `id` (required)
- `banner` **or** `native` (at least one required)
- `tagid` (required)
- `instl` (0/1, optional; default 0)
- `bidfloor` (required), `bidfloorcur` (default USD)
- `secure` (0/1, optional; default 0)
- `displaymanager` (e.g., `"Admize"`), `displaymanagerver` (e.g., `"1.0.0"`)

## Banner
- `w`, `h` required

## Video (if applicable)
- Follow OpenRTB; Admize supports VAST 2.0–4.0.

## Device
Common fields include `ua`, `ip`, `devicetype`, `os`, `ifa`, `osv`, `make`, `model`, `language`, `geo`, and `ext`.

> Replace this page with your detailed field tables and constraints.
