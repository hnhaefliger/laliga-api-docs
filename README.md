# laliga-api-docs
Documentation for the LaLiga data api

## /api/v1

### Verification headers
```
Ocp-Apim-Subscription-Key: c13c3a8e2f6b46da9c5c425cf61fab3e (/v1)
```

### List active competitions
```
GET https://apim.laliga.com/public-service/api/v1/competitions
```
```
limit = int (opt)
orderType = {ASC/DESC} (opt)
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
            "opta_id": str,
            "lde_id": int
        }, 
        ...
    ]
}
```

### Get info about a competition
```
https://apim.laliga.com/public-service/api/v1/subscriptions/laliga-santander-{start-year} 
```

## /api/web