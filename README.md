# World cities with IANA time zones

6,275 cities (population 100,000 and up) mapped to their IANA time zone, as CSV and JSON. Maintained by [SavvyToolz](https://savvytoolz.com), the home of a free [time zone converter](https://savvytoolz.com/en/time-zone-converter).

- `cities.csv`: UTF-8, comma separated, header row
- `cities.json`: the same rows as an array of objects

## Schema

| Field | Type | Description |
|---|---|---|
| `name` | string | City name (GeoNames spelling) |
| `country` | string | Country name |
| `iso2` | string | ISO 3166-1 alpha-2 country code |
| `admin1` | string | State, province or region (may be empty) |
| `timezone` | string | IANA time zone, e.g. `Europe/London` |
| `lat`, `lng` | number | Coordinates in decimal degrees, 3 decimals |
| `population` | integer | Population as reported by GeoNames; urban-area figures can include surrounding districts |
| `slug` | string | Stable URL slug used on savvytoolz.com, unique per row |

## Usage

JavaScript, current time in each city:

```js
import cities from "./cities.json" with { type: "json" };

for (const c of cities.slice(0, 5)) {
  const time = new Intl.DateTimeFormat("en", { timeStyle: "short", timeZone: c.timezone }).format(new Date());
  console.log(`${c.name}: ${time}`);
}
```

Python:

```python
import csv
from datetime import datetime
from zoneinfo import ZoneInfo

with open("cities.csv", newline="", encoding="utf-8") as f:
    for row in csv.DictReader(f):
        if row["name"] == "Tokyo":
            print(datetime.now(ZoneInfo(row["timezone"])))
```

## Source and license

City names, coordinates, populations and time zones derive from [GeoNames](https://www.geonames.org) (`cities15000`), licensed under [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/). SavvyToolz reconciles, filters and re-publishes it under the same license.

This dataset is therefore licensed **CC BY 4.0**. You may share and adapt it, including commercially, provided you give attribution. Suggested attribution:

> City data (c) [GeoNames](https://www.geonames.org), [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Compiled by [SavvyToolz](https://savvytoolz.com).

The export script is released under the MIT license. Time zone identifiers come from the IANA Time Zone Database (public domain).

Time zone rules change; always resolve offsets with an up-to-date tz database (`Intl`, `zoneinfo`, `tzdata`) rather than storing offsets.
