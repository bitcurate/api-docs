# Bitcurate API Documentation
⚠️⚠️⚠️ WORK IN PROGRESS ⚠️⚠️⚠️

*This is a living document, subject to change as more information becomes available, or changes in external and internal conditions create the need for revision. Figures are rough estimations until the final version is created.*

## General API Information
* The base endpoint is: **https://api.bitcurate.com**
* All endpoints return either a JSON object or array.
* Data is returned in **ascending** order. Oldest first, newest last.
* HTTP `4XX` return codes are used for for malformed requests;
  the issue is on the sender's side.
* HTTP `5XX` return codes are used for internal errors; the issue is on
  Bitcurate's side.
* For `POST` endpoints, the parameters must be sent in the `request body` with content type
  `application/json`.

## Access
For access to api endpoints please register at `https://bitcurate.com`. After the email confirmaton, you will be able to use your API credentials.

In order to get access token you would need to make POST request to `https://api.bitcurate.com/api/v1/login`\
with the request body `{"login": "your_email_here", "password": "your_password_here"}`

After recieving the token you can make requests to API with the header `Authorization: Bearer YOUR_TOKEN`\
where `YOUR_TOKEN` - is your token from the login endpoint. Token is valid for one month during the beta testing period.
You would need to update your token after the expiration date.


## Endpoints

### Available exchanges
To get the list of all available exchanges, pairs, and coins make GET request to\
`https://api.bitcurate.com/api/v1/exchanges`

responce example:
```
{
  "exchanges":[
    {"id":"1","name":"binance","pairs":["1","4"],"coins":["1","2","5"]},
    {"id":"2","name":"kraken","pairs":["3"],"coins":["1","4"]},
    {"id":"3","name":"coinbase","pairs":["2"],"coins":["1","5"]},
    {"id":"4","name":"bitstamp","pairs":[],"coins":[]}
  ],
  "pairs":[
    {"id":"1","coins":["1","5"]},
    {"id":"2","coins":["1","5"]},
    {"id":"3","coins":["1","4"]},
    {"id":"4","coins":["2","5"]}
  ],
  "coins":[
    {"id":"1","name":"eth"},
    {"id":"2","name":"btc"},
    {"id":"3","name":"ltc"},
    {"id":"4","name":"usd"},
    {"id":"5","name":"usdt"}
  ]
}
```

### Data stream
⚠️⚠️⚠️ WORK IN PROGRESS ⚠️⚠️⚠️

### Latest data
To get latest data for coin pair make GET request to\
`https://api.bitcurate.com/api/v1/<exchange_name>/<pair_name>/latest`\
where `<exchange_name>` is the name of the exchange from result of `https://api.bitcurate.com/api/v1/exchanges` and `<pair_name>` - is the pair of coin names from result of `https://api.bitcurate.com/api/v1/exchanges`, separated with "_".

request example:
 `https://api.bitcurate.com/api/v1/binance/eth_usdt/latest`

responce example:
```
  {
    "name":"ETH/USDT",
    "exchange":
    "binance",
    "ask":315.08,
    "average":0,
    "bid":315.06,
    "change":9.94,
    "open":0,
    "high":0,
    "low":0,
    "last":315.06,
    "percentage":3.258,
    "utc":"2019-06-23T05:15:41",
    "timestamp":1561266941868
  }
```

### Historical data
To get historical data for coin pair make GET request to\
`https://api.bitcurate.com/api/v1/<exchange_name>/<pair_name>/history/<delta>`\
where `<exchange_name>` is the name of the exchange from result of `https://api.bitcurate.com/api/v1/exchanges` and `<pair_name>` - is the pair of coin names from result of `https://api.bitcurate.com/api/v1/exchanges`, separated with "_",
and `<delta>` - is the time range in seconds

request example:
 `https://api.bitcurate.com/api/v1/binance/eth_usdt/history/1000`

responce example:
```
[
  {
    "name":"ETH/USDT",
    "exchange":
    "binance",
    "ask":315.08,
    "average":0,
    "bid":315.06,
    "change":9.94,
    "open":0,
    "high":0,
    "low":0,
    "last":315.06,
    "percentage":3.258,
    "utc":"2019-06-23T05:15:41",
    "timestamp":1561266941868
  },
  {
    "name":"ETH/USDT",
    "exchange":"binance",
    "ask":315.08,
    "average":0,
    "bid":315.06,
    "change":9.94,
    "open":0,
    "high":0,
    "low":0,
    "last":315.06,
    "percentage":3.258,
    "utc":"2019-06-23T05:15:41",
    "timestamp":1561266941868
  },
  ...
]
```

### Price prediction
⚠️⚠️⚠️ DISCLAIMER: prediction is currently at the test stage ⚠️⚠️⚠️

To get the price prediction for a coin pair make GET request to\
`https://api.bitcurate.com/api/v1/forecast/<pair_name>`
where `<pair_name>` - is the pair of coin names from result of `https://api.bitcurate.com/api/v1/exchanges`, separated with "_"

request example:
`https://api.bitcurate.com/api/v1/forecast/eth_usdt`

responce example:
```
{
  "name": "ETH\USDT",
  "exchange": "gateio",
  "arima_confidence": {
    "up": 0,
    "down": 0
  },
  "arima_future": null,
  "arima_prob": {
    "up": 0,
    "down": 0
  },
  "linear_confidence": {
    "up": 0,
    "down": 0
  },
  "linear_future": [
    254.95035469886,
    255.12550404162,
    255.30065338437,
    255.47580272712,
    255.65095206988,
    255.82610141263,
    256.00125075539,
    256.17640009814,
    256.35154944089,
    256.52669878365,
    256.7018481264,
    256.87699746916,
    257.05214681191,
    257.22729615466,
    257.40244549742,
    257.57759484017,
    257.75274418293,
    257.92789352568,
    258.10304286843,
    258.27819221119,
    258.45334155394,
    258.6284908967,
    258.80364023945,
    258.97878958221,
    259.15393892496,
    259.32908826771,
    259.50423761047,
    259.67938695322,
    259.85453629598,
    260.02968563873,
    260.20483498148,
    260.37998432424,
    260.55513366699,
    260.73028300975,
    260.9054323525,
    261.08058169525,
    261.25573103801,
    261.43088038076,
    261.60602972352,
    261.78117906627,
    261.95632840902,
    262.13147775178,
    262.30662709453,
    262.48177643729,
    262.65692578004,
    262.8320751228,
    263.00722446555,
    263.1823738083,
    263.35752315106,
    263.53267249381,
    263.70782183657,
    263.88297117932,
    264.05812052207,
    264.23326986483,
    264.40841920758,
    264.58356855034,
    264.75871789309,
    264.93386723584,
    265.1090165786,
    265.28416592135,
    265.45931526411,
    265.63446460686,
    265.80961394962,
    265.98476329237,
    266.15991263512,
    266.33506197788,
    266.51021132063,
    266.68536066339,
    266.86051000614,
    267.03565934889,
    267.21080869165,
    267.3859580344,
    267.56110737716,
    267.73625671991,
    267.91140606266,
    268.08655540542,
    268.26170474817,
    268.43685409093,
    268.61200343368,
    268.78715277643,
    268.96230211919,
    269.13745146194,
    269.3126008047,
    269.48775014745,
    269.66289949021,
    269.83804883296,
    270.01319817571,
    270.18834751847,
    270.36349686122,
    270.53864620398,
    270.71379554673,
    270.88894488948,
    271.06409423224,
    271.23924357499,
    271.41439291775,
    271.5895422605,
    271.76469160325,
    271.93984094601,
    272.11499028876,
    272.29013963152,
    272.46528897427,
    272.64043831703,
    272.81558765978,
    272.99073700253,
    273.16588634529,
    273.34103568804,
    273.5161850308,
    273.69133437355,
    273.8664837163,
    274.04163305906,
    274.21678240181,
    274.39193174457,
    274.56708108732
  ],
  "linear_prob": {
    "up": 0,
    "down": 0
  },
  "lstm_confidence": {
    "up": 0,
    "down": 0
  },
  "lstm_future": null,
  "lstm_prob": {
    "up": 0,
    "down": 0
  },
  "future_timestamp": [
    "2019-06-17T06:00:00",
    "2019-06-17T07:00:00",
    "2019-06-17T08:00:00",
    "2019-06-17T09:00:00",
    "2019-06-17T10:00:00",
    "2019-06-17T11:00:00",
    "2019-06-17T12:00:00",
    "2019-06-17T13:00:00",
    "2019-06-17T14:00:00",
    "2019-06-17T15:00:00",
    "2019-06-17T16:00:00",
    "2019-06-17T17:00:00"
  ],
  "timestamp": [
    "2019-06-13T01:00:00",
    "2019-06-13T02:00:00",
    "2019-06-13T03:00:00",
    "2019-06-13T04:00:00",
    "2019-06-13T05:00:00",
    "2019-06-13T06:00:00",
    "2019-06-13T07:00:00",
    "2019-06-13T08:00:00",
    "2019-06-13T09:00:00",
    "2019-06-13T10:00:00",
    "2019-06-13T11:00:00",
    "2019-06-13T12:00:00",
    "2019-06-13T13:00:00",
    "2019-06-13T14:00:00",
    "2019-06-13T15:00:00",
    "2019-06-13T16:00:00",
    "2019-06-13T17:00:00",
    "2019-06-13T18:00:00",
    "2019-06-13T19:00:00",
    "2019-06-13T20:00:00",
    "2019-06-13T21:00:00",
    "2019-06-13T22:00:00",
    "2019-06-13T23:00:00",
    "2019-06-14T00:00:00",
    "2019-06-14T01:00:00",
    "2019-06-14T02:00:00",
    "2019-06-14T03:00:00",
    "2019-06-14T04:00:00",
    "2019-06-14T05:00:00",
    "2019-06-14T06:00:00",
    "2019-06-14T07:00:00",
    "2019-06-14T08:00:00",
    "2019-06-14T09:00:00",
    "2019-06-14T10:00:00",
    "2019-06-14T11:00:00",
    "2019-06-14T12:00:00",
    "2019-06-14T13:00:00",
    "2019-06-14T14:00:00",
    "2019-06-14T15:00:00",
    "2019-06-14T16:00:00",
    "2019-06-14T17:00:00",
    "2019-06-14T18:00:00",
    "2019-06-14T19:00:00",
    "2019-06-14T20:00:00",
    "2019-06-14T21:00:00",
    "2019-06-14T22:00:00",
    "2019-06-14T23:00:00",
    "2019-06-15T00:00:00",
    "2019-06-15T01:00:00",
    "2019-06-15T02:00:00",
    "2019-06-15T03:00:00",
    "2019-06-15T04:00:00",
    "2019-06-15T05:00:00",
    "2019-06-15T06:00:00",
    "2019-06-15T07:00:00",
    "2019-06-15T08:00:00",
    "2019-06-15T09:00:00",
    "2019-06-15T10:00:00",
    "2019-06-15T11:00:00",
    "2019-06-15T12:00:00",
    "2019-06-15T13:00:00",
    "2019-06-15T14:00:00",
    "2019-06-15T15:00:00",
    "2019-06-15T16:00:00",
    "2019-06-15T17:00:00",
    "2019-06-15T18:00:00",
    "2019-06-15T19:00:00",
    "2019-06-15T20:00:00",
    "2019-06-15T21:00:00",
    "2019-06-15T22:00:00",
    "2019-06-15T23:00:00",
    "2019-06-16T00:00:00",
    "2019-06-16T01:00:00",
    "2019-06-16T02:00:00",
    "2019-06-16T03:00:00",
    "2019-06-16T04:00:00",
    "2019-06-16T05:00:00",
    "2019-06-16T06:00:00",
    "2019-06-16T07:00:00",
    "2019-06-16T08:00:00",
    "2019-06-16T09:00:00",
    "2019-06-16T10:00:00",
    "2019-06-16T11:00:00",
    "2019-06-16T12:00:00",
    "2019-06-16T13:00:00",
    "2019-06-16T14:00:00",
    "2019-06-16T15:00:00",
    "2019-06-16T16:00:00",
    "2019-06-16T17:00:00",
    "2019-06-16T18:00:00",
    "2019-06-16T19:00:00",
    "2019-06-16T20:00:00",
    "2019-06-16T21:00:00",
    "2019-06-16T22:00:00",
    "2019-06-16T23:00:00",
    "2019-06-17T00:00:00",
    "2019-06-17T01:00:00",
    "2019-06-17T02:00:00",
    "2019-06-17T03:00:00",
    "2019-06-17T04:00:00",
    "2019-06-17T05:00:00"
  ],
  "values": [
    261.32998657227,
    259.55999755859,
    258.95001220703,
    259.10000610352,
    259.11999511719,
    258.95001220703,
    259.2200012207,
    259.0299987793,
    258.66000366211,
    257.29998779297,
    257.01000976562,
    258,
    259.5299987793,
    259.70001220703,
    261.32000732422,
    259.60000610352,
    259.04998779297,
    261.20999145508,
    260.86999511719,
    259.35998535156,
    261.04998779297,
    261.04998779297,
    255.89999389648,
    256.54998779297,
    254.9700012207,
    254.11000061035,
    254.19999694824,
    254.41000366211,
    255.5,
    254.75,
    255.38000488281,
    257.26998901367,
    255.74000549316,
    255.99000549316,
    255.53999328613,
    255.67999267578,
    257.29998779297,
    257.79998779297,
    257.33999633789,
    257.32000732422,
    255.30999755859,
    256.17001342773,
    256.20001220703,
    257.32000732422,
    261.92999267578,
    262.89001464844,
    263.9700012207,
    263.20001220703,
    265.20001220703,
    265.66000366211,
    264.64999389648,
    264.10998535156,
    264.45999145508,
    265,
    263.42001342773,
    263.60000610352,
    263.17999267578,
    262.80999755859,
    262.86999511719,
    262.42001342773,
    262.29998779297,
    264.82000732422,
    265.48001098633,
    271.29000854492,
    269.70001220703,
    269.2200012207,
    269,
    268.25,
    268.73999023438,
    269.70001220703,
    268.98999023438,
    267.94000244141,
    270,
    271.4700012207,
    270.95999145508,
    270.89999389648,
    275,
    274.45001220703,
    275.08999633789,
    276.70001220703,
    269.79000854492,
    268.95001220703,
    269.32000732422,
    270,
    272.85000610352,
    272.73001098633,
    272.04998779297,
    271.98999023438,
    271.45001220703,
    269.42999267578,
    268.76000976562,
    267.42999267578,
    268.48999023438,
    269.64001464844,
    270.67999267578,
    271.79998779297,
    272.48999023438,
    271.5,
    269.42999267578,
    268.88000488281,
    267.73999023438
  ]
}
```
