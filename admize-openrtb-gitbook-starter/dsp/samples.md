# DSP: Samples

Provide realistic, redacted examples from your staging environment.

## Banner Request (Example)
```json
{ "id": "...", "imp": [{ "id": "06a5f7...", "banner": { "w": 320, "h": 50 }, "bidfloor": 0.1, "tagid": "1" }], "device": { "os": "Android", "ifa": "..." }, "at": 1, "tmax": 100, "cur": ["USD"] }
```

## Banner Response (Example)
```json
{ "id": "...", "seatbid": [{ "bid": [{ "id": "...", "impid": "320x50", "price": 0.3068, "adm": "<html>...</html>" }] }] }
```
