# [BETA] pybotters

An advanced api client for python botters.

## ð Description

`pybotters`ã¯[ä»®æ³éè²¨botter](https://note.com/hht/n/n61e6ecefd059)åãã®Pythonã©ã¤ãã©ãªã§ãã

è¤æ°åå¼æã«å¯¾å¿ããéåæI/Oã®APIã¯ã©ã¤ã¢ã³ãã§ãããbotéçºã«ããç´ æ´ãããDXãæä¾ãã¾ãã

## ð©âð»ð¨âð» In development

`pybotters` ã¯ç¾å¨ ** **BETAãã¼ã¸ã§ã³** ** ã§ãã
ä¸é¨æ©è½ã¯éçºä¸­ã§ãã

éçºç¶æ³ã«ã¤ãã¦ã¯ [ãã¡ã(Issues)](https://github.com/MtkN1/pybotters/issues) ãåç§ãã¦ãã ããã

## ð Features

- â¨ HTTP / WebSocket Client
    - è¤æ°åå¼æã®ãã©ã¤ãã¼ãAPIãèªåèªè¨¼
    - [`aiohttp`](https://docs.aiohttp.org/)ã©ã¤ãã©ãªãåºç¤ã¨ããéåæéä¿¡
    - WebSocketã®èªååæ¥ç¶ãèªåãã¼ããã¼ã
- â¨ DataStore
    - WebSocketç¨ã®èªåãã¼ã¿ä¿ç®¡ã¯ã©ã¹
    - åç§æ¸¡ãã«ããé«éãªãã¼ã¿åç§
    - åå¼æå¥ãã¼ã¿ã¢ãã«ã®å®è£
- â¨ Developer Experience
    - `asyncio`ã©ã¤ãã©ãªãå©ç¨ããéåæãã­ã°ã©ãã³ã°
    - `typing`ã¢ã¸ã¥ã¼ã«ã«ããåãã³ãã®ãµãã¼ã

## ð¦ Exchanges

| Name | API auth | DataStore | API docs |
| --- | --- | --- | --- |
| Bybit | â | â | [LINK](https://bybit-exchange.github.io/docs/inverse) |
| Binance | â | WIP | [LINK](https://binance-docs.github.io/apidocs/spot/en/) |
| FTX | â | â | [LINK](https://docs.ftx.com/) |
| BTCMEX | â | â | [LINK](https://help.btcmex.com/hc/ja/articles/360035945452-API) |
| BitMEX | â | WIP | [LINK](https://www.bitmex.com/app/apiOverview) |
| bitFlyer | â | WIP | [LINK](https://lightning.bitflyer.com/docs) |
| GMO Coin | â | WIP | [LINK](https://api.coin.z.com/docs/) |
| Liquid | â | WIP | [LINK](https://document.liquid.com/) |
| bitbank | â | WIP | [LINK](https://docs.bitbank.cc/) |

## ð Requires

Python 3.7+

## ð  Installation

```sh
pip install pybotters
```

## ð° Usage

### Single exchange

```python
import asyncio
import pybotters

apis = {
    'bybit': ['BYBIT_API_KEY', 'BYBIT_API_SECRET'],
}

async def main():
    async with pybotters.Client(apis=apis, base_url='https://api.bybit.com') as client:
        # REST API
        resp = await client.get('/v2/private/position/list', params={'symbol': 'BTCUSD'})
        data = await resp.json()
        print(data)

        # WebSocket API (with print handler)
        ws = await client.ws_connect(
            url='wss://stream.bybit.com/realtime',
            send_json={'op': 'subscribe', 'args': ['trade.BTCUSD', 'order', 'position']},
            hdlr_json=lambda msg, ws: print(msg),
        )
        await ws # this await is wait forever (for usage)

try:
    asyncio.run(main())
except KeyboardInterrupt:
    pass
```

### Multiple exchanges

```python
apis = {
    'bybit': ['BYBIT_API_KEY', 'BYBIT_API_SECRET'],
    'btcmex': ['BTCMEX_API_KEY', 'BTCMEX_API_SECRET'],
    'binance': ['BINANCE_API_KEY', 'BINANCE_API_SECRET'],
}

async def main():
    async with pybotters.Client(apis=apis) as client:
        await client.post('https://api.bybit.com/v2/private/order/create', data={'symbol': 'BTCUSD', ...: ...})
        ...
        await client.post('https://www.btcmex.com/api/v1/order', data={'symbol': 'XBTUSD', ...: ...})
        ...
        await client.post('https://dapi.binance.com/dapi/v1/order', data={'symbol': 'BTCUSD_PERP', ...: ...})
        ...
```

## ð Wiki

è©³ããå©ç¨æ¹æ³ã¯ð[Wikiãã¼ã¸ã¸](https://github.com/MtkN1/pybotters/wiki)

## ð½ License

MIT

## ð Author

https://twitter.com/MtkN1XBt
