# monsterflavours

The flavour catalog for the Monster Tracker app, published so the app can download updates.

App help: [Support](SUPPORT.md) · [Privacy policy](PRIVACY.md) · [Report a problem or flavour correction](https://github.com/OldGafferSoftware/monsterflavours/issues/new) · info@oldgaffersoftware.com

- `catalog.json`: the full catalog (released flavours only)
- `version.json`: a small file the app checks first, so it only downloads the catalog when it changed
- `scripts/validate.py`: run before every commit; checks the rules below and writes `version.json`

The app reads these through raw GitHub links:

```
https://raw.githubusercontent.com/OldGafferSoftware/monsterflavours/main/version.json
https://raw.githubusercontent.com/OldGafferSoftware/monsterflavours/main/catalog.json
```

Each update is one commit, so the history is a record of every change.

## What's included

Monster Energy-branded drinks sold since the first can in 2002: the original line, Ultra, Juice Monster, Java Monster and the other coffee lines (X-Presso, Espresso, Caffè, Killer Brew), Rehab, Reserve, Nitro, Nitrous and Maxx, Hydro and HydroSport, Dragon Tea, Muscle Monster shakes, the Hitman shooters, and signature drinks such as Valentino Rossi and Lando Norris.

Left out: other brands Monster Beverage owns (Reign, Bang, NOS, Burn, Mutant and so on), Monster Tour Water, the alcoholic Beast Unleashed and Nasty Beast drinks, and pack sizes or can sizes that are the same flavour. A zero-sugar version of the same flavour is shown with `zeroSugar: true` rather than as its own entry, except where Monster sells it as a separate drink (Zero Sugar, Zero Ultra).

## Format

```json
{
  "schemaVersion": 1,
  "version": 1,
  "generated": "2026-11-03",
  "count": 155,
  "license": "CC BY-SA 4.0",
  "attribution": "https://github.com/OldGafferSoftware/monsterflavours#attribution",
  "flavours": [
    {
      "id": "monster-ultra-paradise",
      "name": "Ultra Paradise",
      "notes": "Description shown at the top of the flavour screen",
      "status": "current",
      "markets": ["US", "UK", "Europe", "Japan"],
      "availability": "Where to find it, if not ordinary stores",
      "zeroSugar": true,
      "since": "2019",
      "update": "Short note on the latest status",
      "sourceURL": "https://…",
      "changed": "2026-11-13",
      "discontinued": false
    }
  ]
}
```

`status` is `current`, `limited` (on sale for a limited time), `retired`, or `null` when the current status isn't known. `discontinued` repeats `status == "retired"` for older app versions that only read that field. Every field except `id` and `name` may be `null`.

`changed` is the date (YYYY-MM-DD) this entry was last added or changed in the catalog. The app's "Recent changes" view lists flavours by this date. It is `null` for entries that haven't changed since this field was added on 2026-11-12 (earlier changes were filled in from the repo history).

## Rules

1. Released flavours only. No upcoming, rumoured or cancelled flavours, and no alcoholic products.
2. An `id` is permanent. Never remove or rename one: people's tastings are stored against it. A flavour that ends is marked `retired`.
3. Any change to `flavours` raises `version` by exactly 1, and every new or changed entry gets `changed` set to the catalog's `generated` date.
4. Run `python3 scripts/validate.py` before committing. It refuses a catalog that breaks these rules.

## How status was worked out

Launch years and the list of drinks come mainly from Monster Beverage's annual reports (Form 10-K, 2002 to 2025), which list each year's new products and the products still on sale, leaving out discontinued ones. A drink that drops off that list is marked `retired`, with the year it last appeared in the `update` note. Recent launches, limited editions and cuts come from news reports and company announcements. Each entry's `sourceURL` links the source for its latest status.

Things to know:

- `markets` is a best effort and is incomplete for drinks sold mainly outside the US.
- Some drinks Monster has stopped in the US are still sold elsewhere. Those stay `current`, and the `update` note says where.
- Drinks reported in autumn 2026 to be phasing out by the end of the year (such as Ultra Fantasy Ruby Red, Juice Monster Rio Punch, Java Monster Café Latte and Irish Crème, Rehab Green Tea and Nitro Super Dry) stay `current` until they are gone, with a note.
- Very old or regional drinks with too little information to pin down are left out rather than guessed. Corrections are welcome as issues.

## Attribution

Researched with AI assistance from Monster Beverage's SEC filings, news reports and company announcements, and written in our own words. Each entry links its source in `sourceURL`.

The catalog is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). This license covers the catalog data only, not the names, which may be trademarks of their owners. This is an unofficial fan project, not affiliated with or endorsed by Monster Beverage Corporation or any brand owner.
