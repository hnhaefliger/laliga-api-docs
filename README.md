# laliga-api-docs

Documentation for the LaLiga data api

## /api/v1

### Verification headers
```
Ocp-Apim-Subscription-Key: c13c3a8e2f6b46da9c5c425cf61fab3e
```
### List active competitions
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
### Get a list of related subscriptions
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions
```
```
competitionSlug = str
```
```json
{
    "total": int,
    "subscriptions": [
        {
            "id": int,
            "name": str,
            "slug": str,
            "season": str,
            "season_name": str,
            "year": int,
            "teams": array,
            "rounds": array,
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
            "competition": {
                "id": int,
                "name": str,
                "slug": str,
                "main": bool
            }
        },
        ...
    ]
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
### Get info about a subscription
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}
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
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/current-gameweek
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
### Get completed gameweeks
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/standing-gameweeks
```
```json
{
    "gameweeks": [
        {
            "id": int,
            "week": int,
            "name": str,
            "shortname": str,
            "date": str-timestamp
        },
        ...
    ]
}
```
### Get completed gameweeks
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/standing-gameweeks
```
```json
{
    "gameweeks": [
        {
            "id": int,
            "week": int,
            "name": str,
            "shortname": str,
            "date": str-timestamp
        },
        ...
    ]
}
```
### Get list of players with ranked stats
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/players/rankings
```
```
limit = int (opt)
offset = int (opt)
orderField = stat.{total_effective_clearance_ranking, total_effective_clearance, total_clearance_ranking, total_clearance, total_fwd_zone_pass_ranking, total_fwd_zone_pass, total_attempts_conceded_obox_ranking, total_attempts_conceded_obox, total_attempts_conceded_ibox_ranking, total_attempts_conceded_ibox, total_games_ranking, total_games, total_mins_played_ranking, total_mins_played, total_sub_on_ranking, total_sub_on, total_accurate_pass_ranking, total_accurate_pass, total_accurate_fwd_zone_pass_ranking, total_accurate_fwd_zone_pass, total_pass_ranking, total_pass, total_accurate_back_zone_pass_ranking, total_accurate_back_zone_pass} (opt)
orderType = {ASC,DESC} (opt)
```
```json
{
    "total": int,
    "player_rankings": [
        {
            "id": int,
            "name": str,
            "nickname": str,
            "position": {
                "id": int,
                "name": str,
                "slug": str,
                "plural_name": str,
                "female_name": str,
                "female_plural_name": str
            },
            "slug": str,
            "country": {
                "id": str
            },
            "team": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "foundation": str-timestamp,
                "web": str-url,
                "sprite_status": str,
                "shield": {
                    "id": int,
                    "name": str,
                    "caption": str,
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
            "stats": [
                {   
                    "name": str,
                    "stat": int
                },
                ...
            ],
            "photos": {
                "001": {
                    "1024x1113": str-url,
                    "128x139": str-url,
                    "2048x2225": str-url,
                    "256x278": str-url,
                    "512x556": str-url,
                    "64x70": str-url
                },
                "002": {
                    "1024x1024": str-url,
                    "128x128": str-url,
                    "2048x2048": str-url,
                    "256x256": str-url,
                    "512x512": str-url,
                    "64x64": str-url
                },
                "003": {
                    "1024x1024": str-url,
                    "128x128": str-url,
                    "2048x2048": str-url,
                    "256x256": str-url,
                    "512x512": str-url,
                    "64x64": str-url
                }
            },
            "opta_id": str,
            "lde_id": int,
            "shirt_number": int,
            "extra_info": array
        },
        ...
    ]
}
```
### Get list of player stats
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/players/stats
```
```
limit = int (opt)
offset = int (opt)
orderField = stat.{successful_crosses_corners, unsuccessful_dribbles, index, ground_duels, tackles_lost, goals_conceded, total_passes, recoveries, successful_passes_opposition_half, ground_duels_lost, appearances, goals_conceded_inside_box, unsuccessful_crosses_open_play, backward_passes, unsuccessful_crosses_corners, substitute_on, time_played, successful_short_passes, total_clearances, touches, duels, ground_duels_won, putthrough_blocked_distribution, leftside_passes, unsuccessful_passes_opposition_half, successful_open_play_passes, games_played, times_tackled, successful_passes_own_half, duels_lost, open_play_passes, duels_won, successful_crosses_open_play, total_touches_in_opposition_box, total_fouls_won, total_losses_of_possession, total_successful_passes_excl_crosses_corners, total_tackles, home_goals, away_goals, winning_goal, team_games_played} (opt)
orderType = {ASC, DESC} (opt)
```
```json
{
    "total": int,
    "player_stats": [
        {
            "id": int,
            "name": str,
            "nickname": str,
            "position": {
                "id": int,
                "name": str,
                "slug": str,
                "plural_name": str,
                "female_name": str,
                "female_plural_name": str
            },
            "slug": str,
            "country": {
                "id": str
            },
            "team": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "shirt_style": str,
                "foundation": str-timestamp,
                "web": str-url,
                "sprite_status": str,
                "shield": {
                    "id": str,
                    "name": str,
                    "caption": str,
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
            "stats": [
                {
                    "name": str,
                    "stat": int
                },
                ...
            ],
            "photos": {
                "001": {
                    "1024x1113": str-url
                    "128x139": str-url
                    "2048x2225": str-url
                    "256x278": str-url
                    "512x556": str-url
                    "64x70": str-url   
                },
                "002": {
                    "1024x1024": str-url
                    "128x128": str-url
                    "2048x2048": str-url
                    "256x256": str-url
                    "512x512": str-url
                    "64x64": str-url   
                },
                "003": {
                    "1024x1024": str-url
                    "128x128": str-url
                    "2048x2048": str-url
                    "256x256": str-url
                    "512x512": str-url
                    "64x64": str-url   
                }
            },
            "opta_id": int,
            "shirt_number": int,
            "extra_info": array
        },
        ...
    ]
}
```
### Get list of team stats
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/teams/stats
```
```
limit = int (opt)
offset = int (opt)
orderField = stat.{stat_name} (opt)
orderType = {ASC,DESC} (opt)
```
```json
```

## /api/web