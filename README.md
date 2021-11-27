# laliga-api-docs
Documentation for the LaLiga data api

## /api/v1

### Verification headers
```
Ocp-Apim-Subscription-Key: c13c3a8e2f6b46da9c5c425cf61fab3e (/v1)
```

### List active competitions

The list includes non-laliga competitions.

```curl
GET https://apim.laliga.com/public-service/api/v1/competitions
```
```
limit = int (opt)
orderType = {ASC,DESC} (opt)
showInCalendar = bool (opt)
```
```json
{
    "competitions": [
        {
            "id": int,
            "name": str,
            "slug": str,
            "main": bool,
            "opta_id": str (opt), 
            "lde_id": int (opt)
        }, 
        ...
    ]
}
```

### Get info about a competition

This only works for certain competitions. e.g. "laliga-santander-2021" or "copa-del-rey-2020".

```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{competition_string}
```
```json
{
    "subscription": {
        "id": int,
        "name": str,
        "slug": str,
        "season": str,
        "season_name": str,
        "year": int,
        "teams": [
            {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str (opt),
                "color_secondary": str (opt),
                "foundation": str-timestamp (opt),
                "web": str-url (opt),
                "sprite_status": str,
                "shield": {
                    "id": int,
                    "name": str,
                    "url": str-url,
                    "resizes": {
                        "xsmall": str-url,
                        "small": str-url,
                        "medium": str-url,
                        "large": str-url,
                        "xlarge": str-url
                    }
                },
                "competitions": array,
                "opta_id": str,
                "lde_id": int
            },
            ...
        ],
        "rounds": [
            {
                "id": int,
                "name": str,
                "slug": str,
                "position": int,
                "has_groups": bool,
                "type": str,
                "status": str,
                "num_gameweeks": int,
                "gameweeks": [
                    {
                        "id": int,
                        "week": int,
                        "name": str,
                        "shortname": str,
                        "date": str-timestamp
                    },
                    ...
                ],
                "groups": array
            },
            ...
        ],
        "current_gameweek": {
            "id": int,
            "week": int,
            "name": str,
            "shortname": str,
            "date": str-timestamp,
            "round": {
                "id": int,
                "name": str,
                "slug": str,
                "position": int,
                "has_groups": bool,
                "type": str,
                "status": str,
                "gameweeks": array,
                "groups": array
            }
        },
        "current_gameweek_standing": {
            "id": int,
            "week": int,
            "name": str,
            "shortname": str,
            "date": str-timestamp
        },
        "competition": {
            "id": int,
            "name": str,
            "slug": str,
            "main": bool
        }
    }
}
```
### Get the current gameweek

```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/laliga-santander-2021/current-gameweek
```
```json
{
    "gameweek": {
        "id": int,
        "week": int,
        "name": str,
        "shortname": str,
        "date": str-timestamp
    }
}
```
### Get a list of calendar events

```curl
GET https://apim.laliga.com/public-service/api/v1/calendar
```
```
startDate = str (YYYY-MM-DD) (opt)
endDate = str (YYYY-MM-DD) (opt)
competitionSlug = str (opt)
offset = int (opt)
```
```json
{
    "calendars": [
        {
            "date": str-timestamp,
            "calendar_gameweeks": [
                {
                    "competition": {
                        "id": int,
                        "name": str,
                        "slug": str,
                        "main": bool
                    },
                    "season": {
                        "id": int,
                        "name": str,
                        "year": int,
                        "slug": str
                    },
                    "gameweek": {
                        "id": int,
                        "week": int,
                        "name": str,
                        "shortname": str,
                        "date": str-timestamp
                    }
                },
                ...
            ]
        },
        ...
    ]
}
```
## /api/web