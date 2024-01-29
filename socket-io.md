# Socket.IO Integration Guide("socket.io": "^4.7.2")

## Introduction

Socket.IO is a JavaScript library that enables real-time, bidirectional communication between the server and the client. This guide will walk you through the steps to integrate waxpeer Socket.IO into your application.

- Authentication is done in 2 ways:
  1. Session based via cookies in headers
  2. Having waxpeer API in header as authorization

## Event Subscriptions

Now you can use the `sub/subscribe` and `unsubscribe` methods to listen for specific events, such as:

- `csgo`,`rust`,`tf2`,`dota2` (It will emit `new`,`removed`,`update` events per item)
- `privat_sales` or `item_id` of specific item.
- `inspect`
- `add_item`(deprecated please use game channels)
- `remove`(deprecated please use game channels)
- `update_item`(deprecated please use steamTrade)

### item_id & game channels

Currently it will emit only changes to

- `back`
- `front`
- `full_screenshot`
- `selling`
- `price`
- `float`
- `paint_index`
- `sticker_names`
  Example:

```json
{
  "game": "csgo",
  "name": "AWP | Gungnir (Well-Worn)",
  "float": 0.44339460134506226,
  "price": 7260000,
  "item_id": "34822680618",
  "paint_index": 756,
  "selling": false,
  "sticker_names": ["Sticker | keshandr (Foil) | Krakow 2017"]
}
```

# User events currently supported

- `payment`
- `notification`
- `change_user`
- `connection`
- `steamTrade`

### payment

```json
{
  "type": "update", // update | create
  "data": {
    "id": 727016,
    "status": "completed",
    "transaction_id": null,
    "updated": "2023-12-17T23:05:11.991545-05:00",
    "direction": "out"
  }
}
```

### notification

```json
{
  "type": "update", // update | create
  "data": {
    "id": 19240228,
    "user": "dadf0f33-3563-441a-9ae0-73c0d1b1954c",
    "link": null,
    "action": "sending_steam",
    "image": "https://steamcommunity-a.akamaihd.net/economy/image/class/730/4302203073/200fx125f",
    "message": "Sticker | Heroic | 2020 RMR",
    "parameter": "canceled",
    "read": true,
    "identification": "10375241dadf0f33-3563-441a-9ae0-73c0d1b1954c25707995376",
    "created": "2024-01-18T09:15:33.330Z",
    "updated": "2024-01-19T05:29:12.758Z"
  }
}
```

### change_user

It will emit object key changes from User (wallet,kyc_status,no_p2p_until,failed_trades,failed_row,success_trades and etc.)

```json
{
  "wallet": 10000,
  "kyc_status": "requested"
}
```

### connections

It will emit full connection object if there is create/update/delete operation

```json
{
  "type": "delete", // create | update | delete
  "data": null, // same object as previous_data if present
  "previous_data": {
    "id": 4,
    "username": "®Suspect4you®",
    "user": "2b4fd250-f1528-4307-904e-c86d7e7c0f65",
    "email": "asdad@hotmail.com",
    "avatar": "https://cdn.discordapp.com/avatars/374121399750492160/8d68bf6a22d3279341f6f51ee2c72509.png",
    "oauth": "discord",
    "oauth_id": "123",
    "discriminator": "31270",
    "date": "2019-09-17T12:25:22.051749-04:00",
    "bot": "bot1",
    "main": false
  } // only in delete operation
}
```

### steamTrade

Will be sent to both buyer and seller, it will be the same for both

```json
{
  "type": "update", // create | update
  "data": {
    "id": "10053737",
    "stage": 1,
    "costum_id": "1111-1111-1111-1111",
    "creator": "seller",
    "boxed": "2023-12-18T04:21:35.201Z",
    "send_until": "2023-12-18T04:21:35.201Z",
    "last_updated": "2023-12-18T04:15:42.784Z",
    "done": false,
    "now": "2024-01-19T05:44:11.075Z",
    "user": {
      "id": "ec374e08-5e6d-41b1-ae79-9a9be49969fd",
      "name": "igorhetfbe",
      "avatar": "https://avatars.steamstatic.com/e10b497168effd908662fcf24c28e5a9678380a7_medium.jpg",
      "can_p2p": false,
      "kyc_status": "approved"
    },
    "merchant": {
      "merchant": "waxpeer",
      "avatar": "https://images.waxpeer.com/merch/waxpeer_avatar.jpeg",
      "currency_value": 1,
      "currency_icon": "https://images.waxpeer.com/merch/waxpeer_currency_icon.svg",
      "successlink": "https://waxpeer.com/"
    },
    "seller": {
      "id": "1d1e6ae2-8a74-423c-a6f2-f760a84967f5",
      "name": "01ericksteam",
      "avatar": "https://avatars.steamstatic.com/fef49e7fa7e1997310d705b2a6158ff8dc1cdfeb_medium.jpg",
      "can_p2p": true,
      "kyc_status": null,
      "shop": "1d1e6ae2-8a74-423c-a6f2-f760a84967f5",
      "auto": true,
      "success_trades": 264,
      "failed_trades": 5
    },
    "for": {
      "name": "capTain",
      "avatar": "https://avatars.steamstatic.com/ddfbf17a89515fdd7755f1a9269bb86b0cec484b.jpg",
      "kyc_status": null,
      "steam_joined": 1648237897,
      "steam_level": null
    },
    "items": [
      {
        "id": 7156354,
        "price": 14672990,
        "name": "AWP | Dragon Lore (Factory New)",
        "status": 5,
        "merchant": null,
        "item_id": 30159199413,
        "trade_id": "6073009872",
        "image": "https://steamcommunity-a.akamaihd.net/economy/image/class/730/4880776820/200fx125f",
        "sent_time": "2023-05-20T20:01:02.667+00:00",
        "inspect_item": {
          "floatvalue": 0.043682489544153214,
          "rarity_name": "Covert",
          "stickers": [
            {
              "name": "Sticker | Fnatic (Foil) | Katowice 2015",
              "slot": 1,
              "wear": 0,
              "sticker_price": {
                "average": 118060,
                "img": "-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXQ9QVcJY8gulRYX0DbRvCiwMbQVg8kdFEYsLSkPw5j7PXHeDF94N2kk4XFkvOjZuiFlToG65B33-iY8I_2jlHk-0RqZGHyJNDBIAFoYArU-lG9lPCv28G7mykyXQ"
              }
            },
            {
              "name": "Sticker | Fnatic (Foil) | Katowice 2015",
              "slot": 1,
              "wear": 0,
              "sticker_price": {
                "average": 118060,
                "img": "-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXQ9QVcJY8gulRYX0DbRvCiwMbQVg8kdFEYsLSkPw5j7PXHeDF94N2kk4XFkvOjZuiFlToG65B33-iY8I_2jlHk-0RqZGHyJNDBIAFoYArU-lG9lPCv28G7mykyXQ"
              }
            },
            {
              "name": "Sticker | ZywOo (Gold) | Berlin 2019",
              "slot": 0,
              "wear": 0,
              "sticker_price": {
                "average": 55380,
                "img": "-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXQ9QVcJY8gulRfSV7cTur_h56KHE59IjtNr62qJDhn3P_MTjFD_tuz2tjSz6GkYOmJlD1X7ZMi077DoY2k31Di_hI9MW6nIoDAIwI3aA7S_1SggbC4EsI5-LU"
              }
            },
            {
              "name": "Sticker | s1mple (Gold) | Berlin 2019",
              "slot": 3,
              "wear": 0,
              "sticker_price": {
                "average": 69380,
                "img": "-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXQ9QVcJY8gulRfSV7cTur_h56KHE59IjtE57e1JwJf1PzEdQJO7c6xkc7cxvKgNe_UlzkEsJAh07vHpNvw21bk-UM9ZT_7Jo6XcwdoM1rRr1i6366x0ujAh_sf"
              }
            }
          ]
        },
        "steam_prices": {
          "rarity_color": "#EB4B4B",
          "game_id": 730,
          "collection": "The Cobblestone Collection",
          "collection_icon": "https://cdn.csmarketcap.com/icons/the-cobblestone-collection.png"
        }
      }
    ]
  }
}
```
