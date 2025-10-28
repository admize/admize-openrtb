# SSP: Samples

Provide redacted examples for typical flows.

## Banner Request (Example)
```json
{ "id": "...", "imp": [{ "id": "...", "banner": { "w": 320, "h": 50 }, "bidfloor": 0.1, "tagid": "1" }], "app": { "id": "10124831", "name": "pubnative_ssp_testapp1", "bundle": "pubnative_ssp_testapp.com1" }, "device": { "ifa": "..." }, "cur": ["USD"] }
```

## Banner Response (Example)
```json
{ "id": "...", "seatbid": [{ "bid": [{ "id": "...", "impid": "...", "price": 0.3068, "adm": "<html>...</html>" }] }] }
```

> Replace with your actual, validated samples.
