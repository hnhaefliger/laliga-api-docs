# LaLiga

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
### Get player info
```curl
GET https://apim.laliga.com/public-service/api/v1/players/{player_slug}
```
```json
{
    "player": {
        "id": int,
        "slug": str,
        "name": str,
        "nickname": str,
        "firstname": str,
        "lastname": str,
        "gender": str,
        "date_of_birth": str-timestamp,
        "international": bool,
        "country": {
            "id": str
        },
        "roles": [
            {
                "id": int,
                "name": str,
                "female_name": str,
                "slug": str,
                "active": bool,
                "opta_id": str,
                "lde_id": int
            },
            ...
        ],
        "squad": dict
    }
}
```
### Get list of team stats
```curl
GET https://apim.laliga.com/public-service/api/v1/subscriptions/{subscription_slug}/teams/stats
```
```
limit = int (opt)
offset = int (opt)
orderField = stat.{lost, points, position, games_played, games_pending, won, drawn, putthrough_blocked_distribution_won, possession_percentage, duels_won, ground_duels_won, corners_taken_incl_short_corners, times_tackled, unsuccessful_launches, total_successful_passes_excl_crosses_corners, gk_successful_distribution, offsides, goals_conceded_inside_box, aerial_duels_lost, total_shots, clearances_off_the_line, goals_conceded_outside_box, shots_off_target_inc_woodwork, goals_conceded, open_play_passes, points_gained_from_losing_positions, throw_ins_to_opposition_player, goal_conversion, penalty_goals_conceded, unsuccessful_crosses_open_play, total_passes, passing_accuracy, interceptions, successful_fifty_fifty, unsuccessful_layoffs, successful_short_passes, drops, total_red_cards, successful_crosses_corners, index, catches, successful_long_passes, throw_ins_to_own_player, unsuccessful_short_passes, blocks, foul_attempted_tackle, ground_duels_lost, duels_lost, unsuccessful_dribbles, tackles_won, successful_layoffs, unsuccessful_crosses_corners, successful_crosses_open_play, aerial_duels_won, last_man_tackle, handballs_conceded, successful_corners_into_box, tackles_lost, shots_on_conceded_outside_box, total_fouls_conceded, games_played, attempts_from_set_pieces, yellow_cards, left_foot_goals, putthrough_blocked_distribution, corners_won, duels, hit_woodwork, unsuccessful_passes_own_half, total_shots_conceded, goals, shots_on_conceded_inside_box, ground_duels, goals_from_inside_box, goals_from_outside_box, successful_passes_opposition_half, right_foot_goals, total_clearances, successful_launches, total_fouls_won, tackle_success, unsuccessful_passes_opposition_half, total_losses_of_possession, aerial_duels, clean_sheets, unsuccessful_long_passes, successful_dribbles, successful_passes_own_half, points_dropped_from_winning_positions, red_card_2nd_yellow, passing_opp_half, shooting_accuracy, key_passes_attempt_assists, recoveries, fifty_fifty, blocked_shots, successful_open_play_passes, gk_unsuccessful_distribution, goal_assists, shots_on_target_inc_goals, total_unsuccessful_passes_excl_crosses_corners, crossing_accuracy, unsuccessful_corners_into_box, penalties_conceded, home_goals, away_goals, total_players} (opt)
orderType = {ASC, DESC} (opt)
```
```json
{
    "total": int,
    "team_stats": [
        {
            "id": int,
            "name": str,
            "short_name": str,
            "nick_name": str,
            "slug": str,
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
            "stats": [
                {
                    "name": str,
                    "stat": int
                },
                ...
            ],
            "opta_id": str,
            "lde_id": int
        },
    ]
}
```
### Get list of teams
```curl
GET https://apim.laliga.com/public-service/api/v1/teams
```
```
subscriptionSlug = str (opt)
limit= int (opt)
offset= int (opt)
orderField = str (opt)
orderType = {ASC, DESC} (opt)
```
```json
{
    "total": int,
    "teams": [
        {
            "id": int,
            "slug": str,
            "name": str,
            "nickname": str,
            "boundname": str,
            "shortname": str,
            "sprite_status": str,
            "club": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "selector_name": str
            },
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
            "opta_id": str
        },
        ...
    ]
}
```
### Get team info
```curl
GET https://apim.laliga.com/public-service/api/v1/teams/{team-slug}
```
```json
{
    "team": {
        "id": int,
        "slug": str,
        "name": str,
        "nickname": str,
        "boundname": str,
        "shortname": str,
        "sprite_status": str,
        "club": {
            "id": int,
            "slug": str,
            "name": str,
            "nickname": str,
            "boundname": str,
            "shortname": str,
            "selector_name": str
        },
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
        "competitions": [
            {
                "id": int,
                "name": str,
                "slug": str,
                "main": bool
            }
        ],
        "opta_id": str
    }
}
```
### Get list of players in team
```curl
GET https://apim.laliga.com/public-service/api/v1/teams/{team-slug}/squad-manager
```
```
limit = int
offset = int
orderField = str
orderType = {ASC, DESC}
seasonYear = int
```
```json
{
    "total": int,
    "squads": [
        {
            "id": int,
            "shirt_number": int,
            "current": bool,
            "loan": bool,
            "loan_to": bool,
            "position": {
                "id": 1,
                "name": str,
                "slug": str,
                "plural_name": str,
                "female_name": str,
                "female_plural_name": str
            },
            "team": {
                "id": ,
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
                "competitions": array
            },
            "person": {
                "id": int,
                "name": str,
                "nickname": str,
                "firstname": str,
                "lastname": str,
                "gender": str,
                "date_of_birth": str-timestamp,
                "place_of_birth": str,
                "weight": int,
                "height": int,
                "international": bool,
                "country": {
                    "id": str
                },
                "slug": str
            },
            "role": {
                "id": 1,
                "name": str,
                "female_name": str,
                "slug": str
            },
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
            "lde_id": int
        },
        ...
    ]
}
```
### Get a team's stats in a subscription
```curl
GET https://apim.laliga.com/public-service/api/v1/teams/athletic-club/stats
```
```
subscriptionSlug = str
orderField = stat.{"lost", "points", "position", "games_played", "games_pending", "won", "drawn", "possession_percentage", "recoveries", "total_fouls_conceded", "ground_duels_won", "shots_on_conceded_inside_box", "shots_off_target_inc_woodwork", "set_pieces_goals", "duels", "corners_taken_incl_short_corners", "unsuccessful_dribbles", "duels_won", "points_dropped_from_winning_positions", "aerial_duels_lost", "gk_unsuccessful_distribution", "corners_won", "unsuccessful_passes_own_half", "drops", "shots_on_target_inc_goals", "aerial_duels", "hit_woodwork", "successful_crosses_corners", "catches", "red_card_2nd_yellow", "offsides", "goals_from_outside_box", "successful_passes_opposition_half", "fifty_fifty", "total_successful_passes_excl_crosses_corners", "unsuccessful_short_passes", "successful_passes_own_half", "unsuccessful_launches", "successful_fifty_fifty", "crossing_accuracy", "total_clearances", "passing_accuracy", "goal_conversion", "total_fouls_won", "unsuccessful_long_passes", "blocks", "unsuccessful_crosses_open_play", "total_unsuccessful_passes_excl_crosses_corners", "aerial_duels_won", "open_play_passes", "headed_goals", "foul_attempted_tackle", "successful_open_play_passes", "total_losses_of_possession", "goals_conceded_inside_box", "goals", "ground_duels", "straight_red_cards", "ground_duels_lost", "games_played", "unsuccessful_layoffs", "successful_launches", "total_red_cards", "interceptions", "right_foot_goals", "penalties_taken", "penalty_goals_conceded", "clean_sheets", "throw_ins_to_own_player", "unsuccessful_passes_opposition_half", "passing_opp_half", "successful_layoffs", "duels_lost", "tackle_success", "successful_corners_into_box", "clearances_off_the_line", "putthrough_blocked_distribution_won", "unsuccessful_corners_into_box", "attempts_from_set_pieces", "penalties_conceded", "successful_crosses_open_play", "yellow_cards", "last_man_tackle", "goals_from_inside_box", "throw_ins_to_opposition_player", "successful_dribbles", "shots_on_conceded_outside_box", "own_goals_accrued", "index", "penalty_goals", "tackles_lost", "key_passes_attempt_assists", "total_passes", "total_shots_conceded", "putthrough_blocked_distribution", "shooting_accuracy", "unsuccessful_crosses_corners", "successful_long_passes", "goal_assists", "blocked_shots", "gk_successful_distribution", "points_gained_from_losing_positions", "handballs_conceded", "tackles_won", "total_shots", "successful_short_passes", "times_tackled", "goals_conceded", "foul_won_penalty", "home_goals", "away_goals", "total_players"}
orderType = {ASC, DESC} (opt)
```
```json
{
    "team_stats": {
        "id": int,
        "name": str,
        "short_name": str,
        "nick_name": str,
        "slug": str,
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
        "stats": [
            {
                "name": str,
                "stat": int
            },
            ...
        ],
        "opta_id": str,
        "lde_id": int
    }
}

```
### Get a list of transfers
```curl
https://apim.laliga.com/public-service/api/v1/transfers
```
```
competitionSlug = str
teamTo = str
orderField = str
orderType= {ASC, DESC}
offset = int
limit = int
```
```json
{
    "total": 3,
    "transfers": [
        {
            "id": int,
            "name": str,
            "date": str-timestamp,
            "team_from": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "foundation": str-timestamp,
                "web": str,
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
                "competitions": array
            },
            "team_to": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "foundation": str-timestamp,
                "web": str,
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
                "competitions": array
            },
            "competition": {
                "id": int,
                "name": str,
                "slug": str,
                "main": bool
            },
            "procedure": {
                "id": int,
                "name": str,
                "slug": str
            },
            "nationality_birth": {
                "id": str,
                "name": str
            },
            "state": str,
            "squad": {
                "id": int,
                "shirt_number": 12,
                "current": true,
                "loan": false,
                "loan_to": false,
                "team": {
                    "id": 3,
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
                    "competitions": [
                        {
                            "id": int,
                            "name": str,
                            "slug": str,
                            "main": bool
                        }
                    ]
                },
                "person": {
                    "id": int,
                    "name": str,
                    "nickname": str,
                    "firstname": str,
                    "lastname": str,
                    "gender": str,
                    "date_of_birth": str-timestamp,
                    "place_of_birth": str,
                    "weight": int,
                    "height": int,
                    "international": bool,
                    "country": {
                        "id": str
                    },
                    "slug": str
                },
                "role": {
                    "id": int,
                    "name": str,
                    "female_name": str,
                    "slug": str
                },
                "photos": [
                    {
                        "url": str-url,
                        "string_size": str,
                        "format": str
                    },
                    ...
                ],
                "opta_id": str,
                "lde_id": int
            }
        },
        ...
    ]
}
```
# Get a list of matches played by a team
```curl
https://apim.laliga.com/public-service/api/v1/matches
```
```
seasonYear = int
teamSlug = str
limit = int
status = {played, notplayed}
orderField = str
orderType = str
```
```json
{
    "total": int,
    "matches": [
        {
            "id": int,
            "name": str,
            "slug": str,
            "date": str-timestamp,
            "time": str-timestamp,
            "hashtag": str,
            "competition": {
                "id": int,
                "name": str,
                "slug": str,
                "main": bool,
                "opta_id": str,
                "lde_id": int
            },
            "status": str,
            "note": str,
            "home_team": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "foundation": str-timestamp,
                "web": str,
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
            "away_team": {
                "id": int,
                "slug": str,
                "name": str,
                "nickname": str,
                "boundname": str,
                "shortname": str,
                "color": str,
                "color_secondary": str,
                "foundation": str-timestamp,
                "web": str,
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
            "gameweek": {
                "id": int,
                "week": int,
                "name": str,
                "shortname": str,
                "date": str-timestamp
            },
            "venue": {
                "id": int,
                "name": str,
                "latitude": str,
                "longitude": str,
                "capacity": int,
                "address": str,
                "timezone": str,
                "city": str,
                "slug": str,
                "opta_id": str,
                "lde_id": int
            },
            "persons_role": [
                {
                    "person": {
                        "id": int,
                        "name": str,
                        "nickname": str,
                        "firstname": str,
                        "lastname": str,
                        "gender": str,
                        "international": bool,
                        "slug": str
                    },
                    "role": {
                        "id": int,
                        "name": str,
                        "female_name": str,
                        "slug": str
                    },
                    "opta_id": str,
                    "lde_id": int
                },
                ...
            ],
            "season": {
                "id": int,
                "name": str,
                "year": int,
                "slug": str,
                "opta_id": str,
                "lde_id": int
            },
            "is_brand_day": bool,
            "temperature": {
                "enabled_historical": bool,
                "enabled_forecast": bool
            },
            "ball": {
                "id": int,
                "name": str,
                "image": str
            },
            "opta_id": str,
            "lde_id": int
        },
        ...
    ]
}
```

## /api/web

### Verification headers
```
Ocp-Apim-Subscription-Key: ee7fcd5c543f4485ba2a48856fc7ece9
```

https://apim.laliga.com/webview/api/web/seasons/opta/2021/competitions/opta/23/rankings/players/group?stats%5B0%5D=stat.total_goals_ranking&stats%5B1%5D=stat.total_ontarget_attempt_ranking&stats%5B2%5D=stat.total_pass_ranking&stats%5B3%5D=stat.total_assists_ranking&stats%5B4%5D=stat.total_interception_ranking&stats%5B5%5D=stat.total_yellow_card_ranking&stats%5B6%5D=stat.total_red_card_ranking&stats%5B7%5D=stat.total_fouls_ranking&optaTeamId=t174

https://apim.laliga.com/webview/api/web/subscriptions/laliga-santander-2021/week/15/matches

https://apim.laliga.com/webview/api/web/gameweeks/2482/summary

https://apim.laliga.com/webview/api/web/subscriptions/laliga-santander-2021/standing?week=15

https://apim.laliga.com/webview/api/web/subscriptions/laliga-santander-2021/standing?orderField=homePosition&week=15

https://apim.laliga.com/webview/api/web/subscriptions/laliga-santander-2021/standing?orderField=awayPosition&week=15

https://apim.laliga.com/webview/api/web/subscriptions/116/teams/3/faqs

https://apim.laliga.com/webview/api/web/seasons/opta/2021/competitions/opta/23/rankings/players/group?stats%5B0%5D=stat.total_goals_ranking&stats%5B1%5D=stat.total_ontarget_attempt_ranking&stats%5B2%5D=stat.total_pass_ranking&stats%5B3%5D=stat.total_assists_ranking&optaTeamId=t174