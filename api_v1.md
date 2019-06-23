⚠️⚠️⚠️ WORK IN PROGRESS ⚠️⚠️⚠️

*This is a living document, subject to change as more information becomes available, or changes in external and internal conditions create the need for revision. Figures are rough estimations until the final version is created.*

# Bitcurate API Documentation
Currently we are working on v1 implementation, it's still work in progress and more features will be available in the future.

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
with the request body `{"login": "user@example.com", "password": "your_password_here"}`

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


---------------------------------
### Available coin pairs

Ro get the list of all available coin pairs, for a particular exchange make GET requests to\
`https://api.bitcurate.com/api/v1/<exchange_name>/pairs`
Where <exchange_name> - is the name of exchange from result of `https://api.bitcurate.com/api/v1/exchanges` request

request example:
`https://api.bitcurate.com/api/v1/binance/pairs`

responce example:
```
[{"name":"ada_bnb"},
 {"name":"ada_btc"},
 {"name":"ada_eth"},
 {"name":"ada_usdt"},
 {"name":"adx_bnb"},
 {"name":"adx_btc"},
 {"name":"adx_eth"},
 {"name":"ae_bnb"},
 {"name":"ae_btc"},
 {"name":"ae_eth"},
 {"name":"agi_bnb"},
 {"name":"agi_btc"},
 {"name":"agi_eth"},
 {"name":"aion_bnb"},
 {"name":"aion_btc"} ...}]
 ```

### Coin pair data

To get coin pair data make GET request to\
`https://api.bitcurate.com/api/v1/<exchange_name>/<pair_name>/latest`
where `<exchange_name>` - is the name of the exchange from result of `https://api.bitcurate.com/api/v1/exchanges` request
and `<pair_name>` - is the name of coin pair from the result of `https://api.bitcurate.com/api/v1/<exchange-name>/pairs` request

request example:
 `https://api.bitcurate.com/api/v1/binance/btc_usdt/latest`

responce example:
```
{"name":"BTC/USDT",
 "exchange":"binance",
 "ask":3991.3,
 "average":0,
 "bid":3990.09,
 "change":9.75,
 "open":0,
 "high":0,
 "low":0,
 "last":3991.3,
 "percentage":0.245,
 "utc":"2019-03-25T07:04:29",
 "timestamp":1553497469687}
```
### Available coins

to get all available coins make GET request to\
`https://api.bitcurate.com/api/v1/coins`

responce example:
```
[{"name":"basic_attention_token"},
 {"name":"binance_coin"},
 {"name":"bitcoin"},
 {"name":"bitcoin_cash"},
 {"name":"bitcoin_gold"},
 {"name":"bitcoin_sv"},
 {"name":"cardano"},
 {"name":"chainlink"},
 {"name":"crypto_com_chain"},
 {"name":"dash"},
 {"name":"decred"},
 {"name":"dogecoin"},
 {"name":"eos"},
 {"name":"ethereum"},
 {"name":"ethereum_classic"},
 {"name":"iota"},
 {"name":"lisk"},
 {"name":"litecoin"},
 {"name":"maker"},
 {"name":"monero"},
 {"name":"nem", ...}
```
### Coin data

to get coin data make GET request to\
`https://api.bitcurate.com/api/v1/<coin_name>/latest`

where `<coin_name>` - is the name of the coin from `https://api.bitcurate.com/api/v1/coins` request

request example:
`https://api.bitcurate.com/api/v1/Ethereum/latest`

responce example:
```
{"name":"Ethereum",
 "slug":"ethereum",
 "circulating_supply":105310732.3741,
 "total_supply":105310732.3741,
 "max_supply":0,
 "rank":2,
 "price":139.050992627,
 "volume_24h":4338628958.45959,
 "change_1h":0.0060562,
 "change_24h":-0.278413,
 "change_7d":4.13387,
 "market_cap":14643561870.894949,
 "timestamp":1553065639}
```
### Price prediction

⚠️⚠️⚠️ DISCLAIMER: prediction is currently at the test stage, we provide prediction only for `LTC/BTC` trading pair, more pairs are comming soon, stay tuned ⚠️⚠️⚠️

To get the price prediction for a coin pair make GET request to\
`https://api.bitcurate.com/api/v1/forecast/<pair_name>`

where `<pair_name>` - is the name of coin-pair from result of `https://api.bitcurate.com/api/v1/<exchange-name>/pairs` request

request example:
`https://api.bitcurate.com/api/v1/forecast/ltc_btc`

responce example:
```
{"name":"LTC/BTC",
 "exchange":"binance",
 "arima_confidence":{"up":0.8226549176108906,"down":0.776381097587262},
 "arima_future":[0.014279000461101534,0.01476499996184219,0.015386999563792539,0.015146999617525454,0.014312809353285442,0.014968858537096662,0.015002590313277666,0.014834182589430657,0.014670900397597431,0.014586887767264434,0.01438891690207868,0.014399619146453707,0.014545154534408227,0.014497897772418495,0.014562111340469155,0.014470660248333444,0.014623716553268811,0.014705137486268054,0.014782058421428663,0.014762295915358712],
 "arima_prob":{"up":0.22749999999999998,"down":0.195},
 "linear_confidence":{"up":0,"down":0.9818900848589389},
 "linear_future":[0.014824005682566012,0.014811116109894011,0.014798226537222011,0.014785336964550012,0.014772447391878012,0.014759557819206012,0.014746668246534011,0.014733778673862013,0.014720889101190012,0.014707999528518012,0.014695109955846011,0.014682220383174013,0.014669330810502012,0.014656441237830012,0.014643551665158011,0.014630662092486013,0.014617772519814012,0.014604882947142012,0.014591993374470012,0.014579103801798013],
 "linear_prob":{"up":0,"down":0.81},
 "lstm_confidence":{"up":0.905345505054887,"down":0.671135257273922},
 "lstm_future":[0.014764999970793722,0.01472636699217489,0.014772728288793393,0.01475943844605099,0.014786052778498428,0.01485304190737813,0.014878742529302104,0.014857523017661191,0.014773169625103113,0.01475678135398817,0.014556629124793554,0.014493272487623334,0.014698892672619259,0.01474235104872579,0.01471727608289042,0.014633984630048615,0.014671884334087839,0.014740917324414961,0.014869024262515686,0.01483593543360029],
 "lstm_prob":{"up":0.26,"down":0.1625},
 "future_timestamp":["2019-03-16T00:00:00","2019-03-16T12:00:00"],
 "timestamp":["2019-03-07T00:00:00","2019-03-07T12:00:00","2019-03-08T00:00:00","2019-03-08T12:00:00","2019-03-09T00:00:00","2019-03-09T12:00:00","2019-03-10T00:00:00","2019-03-10T12:00:00","2019-03-11T00:00:00","2019-03-11T12:00:00","2019-03-12T00:00:00","2019-03-12T12:00:00","2019-03-13T00:00:00","2019-03-13T12:00:00","2019-03-14T00:00:00","2019-03-14T12:00:00","2019-03-15T00:00:00","2019-03-15T12:00:00"],
 "values":[0.014764999970793724,0.015143999829888344,0.01476799976080656,0.014570999890565872,0.015143999829888344,0.014929999597370625,0.014728999696671963,0.014600000344216824,0.014588999561965466,0.014279000461101532,0.014592999592423439,0.014632999897003174,0.014593999832868576,0.014587000012397766,0.01450399961322546,0.01476799976080656,0.014832999557256699,0.0148290004581213]}
```
