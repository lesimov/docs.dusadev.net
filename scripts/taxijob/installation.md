---
icon: down
---

# Installation

## Requirements

| Dependency                                         | Required | Purpose                                                      |
| -------------------------------------------------- | -------- | ------------------------------------------------------------ |
| [dusa\_bridge](https://docs.dusadev.net)           | ✅ Yes    | Player, job, duty, notification & money framework adaptation |
| [ox\_lib](https://github.com/overextended/ox_lib)  | ✅ Yes    | Locales and callback transport                               |
| [oxmysql](https://github.com/overextended/oxmysql) | ✅ Yes    | Persistent station, vehicle & economy data                   |
| lb-phone                                           | Optional | Public employee phone numbers via `GetEquippedPhoneNumber`   |
| MugShotBase64                                      | Optional | Player ped avatars (data-URL) in recruitment UI              |

## Steps

1. Download **Taxi Job** from the Cfx.re portal
2. Extract into `resources/[dusa]/`
3. Add to `server.cfg`:

```cfg
ensure dusa_taxijob
```

4. Restart the server — done. The database tables are **created automatically** on first start.

> 💡 **Database issues?** If automatic table creation fails on your setup, import the SQL manually: `dusa_taxijob/database/install.sql` (creates `dusa_taxi_stations`, `dusa_taxi_vehicles`, `dusa_taxi_trips`, `dusa_taxi_transactions`).
