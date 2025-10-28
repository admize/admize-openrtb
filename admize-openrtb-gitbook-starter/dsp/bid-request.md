# DSP: Bid Request

## Transport
- Headers: `x-openrtb-version: 2.3|2.5`, `Accept-Encoding: gzip`, `Content-Type: application/json`, optionally `Content-Encoding: gzip` if body gzipped.
- `tmax` indicates total timeout budget (ms).

## Core Objects
- `id`, `imp[]` (banner/native), `app`/`site`, `device` (required), `regs` (optional), `source` (optional), blocks `badv[]`, `bapp[]`, `bcat[]`.
- `at` default **2** (second price), `cur` default **USD**.

## Device
- Requires `os`; other fields like `ifa`, `ua`, `ip`, `devicetype`, `connectiontype`, `geo`, etc. as available.

## Source / schain
- `source.ext.schain` following IAB SupplyChain object.

> Add your field-by-field contract and per-SSP variations.
