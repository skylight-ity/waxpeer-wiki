# Main Page Endpoints Documentation

## GET `/data/index` Items list

Query Parameters:

- `sort`: Optional. Specifies the sorting order. Valid values are "asc" or "desc". Default is "desc".
- `order`: Optional. Specifies the sorting field. Valid values are "float", "date", "deals", "profit", or "price".
- `shop`: Optional. Specifies the shop ID (sellers id or shop nickname) to filter the inventory by.
- `stickers`: Optional. Specifies the stickers to filter the inventory by.
- `game`: Optional. Specifies the game to filter the inventory by. Default is "csgo" (second enabled is "tf2").
- `limit`: Optional. Specifies the maximum number of items to load. Must be a number between 1 and 99. Default is 50.
- `min_price`: Optional. Specifies the minimum price of items to load ($1 = 1000).
- `max_price`: Optional. Specifies the maximum price of items to load ($1 = 1000).
- `live`: Optional. Specifies whether to load live page items. Must be 1 or 0 (Live page: https://waxpeer.com/live).
- `merchant`: Optional. Specifies the merchant to filter the inventory by.
- `pack`: Optional. Specifies whether to filter by pack items. Must be 1 or 0.
- `sticker_count`: Optional. Specifies the number of stickers to filter the inventory by. Must be a number between 0 and 5.
- `search`: Optional. Specifies the search query to filter the inventory by.
- `exact`: Optional. Specifies whether to perform an exact search (Exact search used on click, otherwise vector search). Must be 1 or 0. Default is 0.
- `category`: Optional. Specifies the category to filter the inventory by. Can be a string or an array of strings. Example "Desert Eagle".
- `skip`: Optional. Specifies the number of items to skip.
- `lang`: Optional. Specifies the language for localization. Possible values are "en" (English), "ru" (Russian), "uk" (Ukrainian), "es" (Spanish), "da" (Danish), "de" (German), "fr" (French), "nl" (Dutch), "pl" (Polish), "pt" (Portuguese), "ro" (Romanian), "sv" (Swedish), "tr" (Turkish), "zh" (Simplified Chinese). Default is "en".
- `phase`: Optional. Specifies the phase of the item to filter the inventory by. Valid values are "p1" (Phase 1), "p2" (Phase 2), "p3" (Phase 3), "p4" (Phase 4), "sh" (Sapphire), "rb" (Ruby), "bp" (Black Pearl), "em" (Emerald). Can be a string or an array of strings.
- `stat_trak`: Optional. Specifies whether to filter the inventory by StatTrak items. Must be a boolean value (0 or 1).

Array of string should be used as `&phase=p1&phase=p2`

Response:
The response schema depends on the passed queries. If the function executes successfully, the response will have a status code of 200 and the body will contain:

- `success`: A boolean indicating whether the operation was successful.
- `msg`: Optional. A message providing additional information or an error message if an error occurred during the execution of the function.
- `items`: Optional. An array of loaded inventory items.
- `shopStats`: Optional. Shop statistics for the loaded inventory.
- `seller`: Optional. Seller information for the loaded inventory.

If an error occurs during the execution of the function, the response will have a status code of 500 and the body will be:

Example:
Request: `GET /api/data/index?sort=ASC&order=price&game=csgo&limit=50&min_price=10&max_price=1000000&sticker_count=3&exact=0&shop=matrix&search=Fuel%20Injector&exact=0&skip=1&lang=en`

Example Response:

```
{
    "success": true,
    "items": [
        {
            "item_id": "37803458124",
            "brand": "rifle",
            "image": "https://steamcommunity-a.akamaihd.net/economy/image/class/730/5923030628/200fx125f",
            "full_ex": "Battle-Scarred",
            "type": "AK-47",
            "price": 89878,
            "game": "csgo",
            "exterior": "BS",
            "name": "AK-47 | Fuel Injector (Battle-Scarred)",
            "market_name": "Fuel Injector",
            "by": "4e56af1d-8deb-4b9f-b829-1e89b0d4c3fa",
            "stat_trak": false,
            "float": 0.8774367570877075,
            "steam_price_number": 129950,
            "phase": null,
            "auto": true,
            "popular": false,
            "steam_price": {
                "name": "AK-47 | Fuel Injector (Battle-Scarred)",
                "item_id": "34774384033",
                "average": 129950,
                "current": 120350,
                "img": "https://images.waxpeer.com/i/730-ak-47-fuel-injector-battle-scarred.webp",
                "game_id": 730,
                "popular": false,
                "lowest_price": 89024,
                "highest_offer": 91486,
                "type": "Rifle",
                "rarity_color": "#EB4B4B",
                "rarity": "Covert",
                "ru_name": "AK-47 | Топливный инжектор (Закалённое в боях)",
                "ch_name": "AK-47 | 燃料喷射器 (战痕累累)",
                "api_count": 34,
                "localized_name": "AK-47 | Fuel Injector (Battle-Scarred)"
            },
            "inspect_item": {
                "origin": 8,
                "floatvalue": 0.8774367570877075,
                "imageurl": "http://media.steampowered.com/apps/730/icons/econ/default_generated/weapon_ak47_gs_ak47_supercharged_light_large.8a0d53e84b7049366a3e3dbb25d29f473d76dceb.png",
                "weapon_type": "AK-47",
                "front": "https://images.waxpeer.com/screenshot/items/37803458124_front_auto_1716622880440.webp",
                "back": "https://images.waxpeer.com/screenshot/items/37803458124_back_auto_1716622880440.webp",
                "full_screenshot": null,
                "stickers": []
            }
        }
    ],
    "shopStats": {
        "total": 781542774,
        "count": "47823"
    },
    "seller": {
        "id": "4e56af1d-8deb-4b9f-b829-1e89b0d4c3fa",
        "name": "matrix",
        "can_p2p": true,
        "success_trades": 122951,
        "failed_trades": 685,
        "failed_row": 0,
        "average_time": 34,
        "auto": false,
        "avatar": "https://avatars.akamai.steamstatic.com/f2fcdc30aec2ff5a34c8db8780bf0d9887343f41_full.jpg",
        "force_off": false,
        "shop_public": true,
        "shop_history": true,
        "kyc_status": "approved"
    }
}
```

### Interface

```
interface RootObject {
  success: boolean;
  msg?: string;
  items?: Item[];
  shopStats?: ShopStats; // Available with shop query
  seller?: Seller; // Available with shop query
}

interface Seller {
  id: string;
  name: string;
  can_p2p: boolean;
  success_trades: number;
  failed_trades: number;
  failed_row: number;
  average_time: number;
  auto: boolean;
  avatar: string;
  force_off: boolean;
  shop_public: boolean; // Is seller info is public (If false - ingognito nickname and avatar applied)
  shop_history: boolean; // Is sell history is public (If true - "/api/sales" could be sent)
  kyc_status: string; // Possible values: null | "requested" | "approved"
}

interface ShopStats {
  total: number; // Total items amount $1 = 1000
  count: string; // Total items count
}

interface Item {
  item_id: string;
  brand: null | string;
  image: string;
  full_ex: string;
  type: string;
  price: number;
  game: string;
  exterior: null | string;
  name: string;
  market_name: string;
  by: string;
  stat_trak: boolean;
  float: null | number;
  steam_price_number: number;
  phase: null;
  auto: boolean;
  popular: boolean;
  steam_price: Steamprice;
  inspect_item: Inspectitem | null;
  moderateStats?: ModerateStats; // Admin feature
}

interface ModerateStats {
  approvedText: string[];
  approvedVideo: string[];
  textState: number;
  videoState: number;
  completeText: boolean;
  completeVideo: boolean;
}

interface Inspectitem {
  origin: number;
  floatvalue: number;
  imageurl: string | null;
  weapon_type: string;
  front: string | null;
  back: string | null;
  full_screenshot: string | null;
  stickers: Sticker[];
}

interface Sticker {
  id: string;
  wear: number;
  name: string;
  image: string;
  slot: number;
  steam_price: Steamprice2;
}

interface Steamprice2 {
  average: number;
  img: string;
  type: string;
  localized_name: string;
}

interface Steamprice {
  name: string;
  item_id: null | string;
  average: number;
  current: number;
  img: string;
  game_id: number;
  popular: boolean;
  lowest_price: number;
  highest_offer: number;
  type: string;
  rarity_color: string;
  rarity: string;
  ru_name: null | string;
  ch_name: null | string;
  api_count: number;
  localized_name: string;
}
```
