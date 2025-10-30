# Request & Response Examples

This page provides complete examples of bid requests and responses for different ad formats from the DSP integration perspective.

## Banner Examples

### Banner Bid Request

```json
{
  "id": "1-1701305999872-3223-7338-625196",
  "imp": [
    {
      "id": "06a5f7ca-0f13-4ae1-6a6e-15ffef02c650",
      "banner": {
        "w": 320,
        "h": 50
      },
      "bidfloor": 0.1,
      "bidfloorcur": "USD",
      "tagid": "1",
      "displaymanager": "Admize",
      "displaymanagerver": "1.0.0"
    }
  ],
  "app": {
    "publisher": {
      "id": "p_1875135418654156",
      "name": "Admize",
      "ext": {
        "sid": 6
      }
    },
    "id": "10124831",
    "name": "pubnative_ssp_testapp1",
    "bundle": "pubnative_ssp_testapp.com1",
    "storeurl": "pubnative_ssp_testapp.com2"
  },
  "device": {
    "ifa": "638343a6-e910-4f33-b836-000de74b4c18",
    "ua": "Mozilla/5.0 (Linux; Android 5.1.1; SM-N910P Build/LMY47X; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/55.0.2883.91 Mobile Safari/537.36",
    "ip": "73.94.129.148",
    "geo": {
      "country": "KOR",
      "city": "Seoul"
    },
    "language": "en",
    "model": "android",
    "os": "Android",
    "osv": "5.1.1",
    "connectiontype": 2,
    "devicetype": 1
  },
  "at": 1,
  "tmax": 100,
  "cur": ["USD"],
  "badv": ["foosite.com"],
  "bcat": ["IAB13", "IAB14"],
  "bapp": ["com.foo.test1", "io.testssp.testapp"],
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
            "asi": "center.admize.io",
            "sid": "p_1875135558794156",
            "hp": 1
          }
        ]
      }
    }
  }
}
```

### Banner Bid Response

```json
{
  "id": "4b64365402e54e0869e1d39c2ee4c432",
  "seatbid": [
    {
      "bid": [
        {
          "id": "1-1644894781441-161-23-2446841",
          "impid": "320x50",
          "price": 0.3068,
          "adid": "495E8194:1644894781:0363905980",
          "adm": "<!doctype html>\n<html>\n<head>\n  <meta charset=\"utf-8\">\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no\">\n  <link rel=\"icon\" href=\"data:,\">\n  <style>\n    BODY { margin: 0; padding: 0; }\n    .container { width:100%; height:100%; }\n    .block { width:320px; height:50px; margin:0 auto; overflow:hidden; }\n  </style>\n</head>\n<body>\n  <div class=\"container\">\n    <div class=\"block\">\n      <iframe id=\"Admize_area\" name=\"Admize_area\" style=\"width:320px; height:50px; margin:0px; padding:0px; border: none;\"></iframe>\n    </div>\n  </div>\n  <script>\n    createBeacon('https://test-event.admize.io/imp/ssp/v1/1-1644894781441-161-23-2446841?ap=${AUCTION_PRICE}');\n  </script>\n</body>\n</html>",
          "adomain": ["id535886823"],
          "cid": "23501",
          "crid": "454651",
          "cat": ["IAB1-1"],
          "w": 320,
          "h": 50
        }
      ]
    }
  ]
}
```

## Native Examples

### Native Bid Request

```json
{
  "id": "4b6436abc2e54e0869e1d39c2ee4c432",
  "imp": [
    {
      "id": "16abc7ca-0f13-4ae1-6a6e-15ffabec650",
      "native": {
        "ver": "1.2",
        "request": "{\"native\":{\"ver\":\"1.2\",\"plcmttype\":1,\"plcmtcnt\":1,\"seq\":0,\"assets\":[{\"id\":1,\"required\":0,\"data\":{\"type\":12,\"len\":10}},{\"id\":2,\"required\":1,\"title\":{\"len\":10}},{\"id\":3,\"required\":1,\"img\":{\"type\":1,\"w\":80,\"wmin\":0,\"h\":80,\"hmin\":0}},{\"id\":4,\"required\":1,\"img\":{\"type\":3,\"w\":1200,\"wmin\":0,\"h\":627,\"hmin\":0}}]}}"
      },
      "bidfloor": 0.1,
      "bidfloorcur": "USD",
      "tagid": "test-tagid",
      "instl": 1
    }
  ],
  "app": {
    "id": "1266591536",
    "name": "adidas",
    "bundle": "1266591536",
    "storeurl": "https://apps.apple.com/kr/app/adidas/id1266591536",
    "cat": ["IAB9"],
    "mobile": 1,
    "publisher": {
      "id": "p_3926858200918887",
      "name": "ssp7"
    }
  },
  "device": {
    "ifa": "juyeon-e910-4f33-b836-000de74b4c18",
    "dnt": 1,
    "ua": "Mozilla/5.0 (Linux; Android 5.1.1; SM-N910P Build/LMY47X; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/55.0.2883.91 Mobile Safari/537.36",
    "ip": "73.94.129.148",
    "geo": {
      "lat": 45.2874,
      "lon": -93.4336,
      "country": "USA",
      "region": "MN",
      "city": "Anoka",
      "zip": "55303",
      "type": 2
    },
    "carrier": "Comcast Cable",
    "language": "en",
    "model": "ios",
    "os": "Ios",
    "osv": "5.1.1",
    "connectiontype": 2,
    "devicetype": 1,
    "w": 720,
    "h": 1230
  },
  "user": {
    "id": "f0fe0536-9d50-5d5d-b28b-fb8ad0e45ac0"
  },
  "at": 2,
  "tmax": 200,
  "allimps": 0,
  "cur": ["USD"],
  "bcat": ["IAB11"]
}
```

### Native Bid Response

```json
{
  "id": "4b6436abc2e54e0869e1d39c2ee4c432",
  "cur": "USD",
  "seatbid": [
    {
      "bid": [
        {
          "id": "16abc7ca-0f13-4ae1-6a6e-15ffabec65011",
          "impid": "16abc7ca-0f13-4ae1-6a6e-15ffabec650",
          "price": 0.15,
          "adm": "{\"native\":{\"ver\":\"1.2\",\"assets\":[{\"id\":1,\"required\":0,\"data\":{\"len\":20,\"type\":12,\"value\":\"더 알아보기\"}},{\"id\":2,\"title\":{\"text\":\"테스트-타이틀\"}},{\"id\":3,\"img\":{\"w\":80,\"h\":80,\"type\":1,\"url\":\"https://cdn-admize.com/images-icon/05d8013c9a129785373d319ef7f01117.jpg\"}},{\"id\":4,\"img\":{\"w\":1200,\"h\":627,\"type\":3,\"url\":\"https://cdn-admize.com/images-main/05d8013c9a129785373d319ef7f01117.jpg\"}}],\"link\":{\"url\":\"https://admize-test-api-backend.com/link.js\"},\"imptrackers\":[],\"eventtrackers\":[]}}",
          "cid": "1-1-1-1"
        }
      ]
    }
  ]
}
```

## Key Differences from SSP Integration

### Request Headers
DSP integrations receive these additional headers:
- `x-openrtb-version`: Indicates the OpenRTB version
- `Content-Encoding`: May be gzip if compression is supported

### Supply Chain
DSP requests include the `source.ext.schain` object showing the supply chain:

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
            "asi": "center.admize.io",
            "sid": "p_1875135558794156",
            "hp": 1
          }
        ]
      }
    }
  }
}
```

### Publisher Information
Publisher details are always included with extended information:

```json
{
  "publisher": {
    "id": "p_1875135418654156",
    "name": "Admize",
    "ext": {
      "sid": 6
    }
  }
}
```

## Native Request Details

The native request string (when decoded) contains:

```json
{
  "native": {
    "ver": "1.2",
    "plcmttype": 1,
    "plcmtcnt": 1,
    "seq": 0,
    "assets": [
      {
        "id": 1,
        "required": 0,
        "data": {
          "type": 12,
          "len": 10
        }
      },
      {
        "id": 2,
        "required": 1,
        "title": {
          "len": 10
        }
      },
      {
        "id": 3,
        "required": 1,
        "img": {
          "type": 1,
          "w": 80,
          "wmin": 0,
          "h": 80,
          "hmin": 0
        }
      },
      {
        "id": 4,
        "required": 1,
        "img": {
          "type": 3,
          "w": 1200,
          "wmin": 0,
          "h": 627,
          "hmin": 0
        }
      }
    ]
  }
}
```

## Native Response Details

The native response adm (when decoded) contains:

```json
{
  "native": {
    "ver": "1.2",
    "assets": [
      {
        "id": 1,
        "required": 0,
        "data": {
          "len": 20,
          "type": 12,
          "value": "더 알아보기"
        }
      },
      {
        "id": 2,
        "title": {
          "text": "테스트-타이틀"
        }
      },
      {
        "id": 3,
        "img": {
          "w": 80,
          "h": 80,
          "type": 1,
          "url": "https://cdn-admize.com/images-icon/05d8013c9a129785373d319ef7f01117.jpg"
        }
      },
      {
        "id": 4,
        "img": {
          "w": 1200,
          "h": 627,
          "type": 3,
          "url": "https://cdn-admize.com/images-main/05d8013c9a129785373d319ef7f01117.jpg"
        }
      }
    ],
    "link": {
      "url": "https://admize-test-api-backend.com/link.js"
    },
    "imptrackers": [],
    "eventtrackers": []
  }
}
```

## Testing Tips

1. **Validate JSON**: Ensure your response is valid JSON
2. **Check Required Fields**: All required fields must be present
3. **Test with Different Sizes**: Support multiple banner sizes
4. **Native Asset Compliance**: Ensure native responses match requested assets
5. **URL Encoding**: Properly encode tracking URLs
6. **Timeout Handling**: Respond within tmax milliseconds
7. **Error Handling**: Return appropriate HTTP status codes
