# Changelog

All notable changes to this project are documented in this file.

## [0.5.9.5] - 2026-10-22

### Fixed

- **Setup failure with YAML dashboards:** The BTC Address Card was registered
  by creating a Lovelace resource, which does not exist in YAML mode and made
  the whole integration fail to set up. The card is now loaded with
  `add_extra_js_url`, which works in every dashboard mode. A resource created
  by an earlier version is harmless and can be removed manually.
- **Card not found by dashboards:** The card now registers itself once the
  Home Assistant frontend is ready. Loaded earlier via `add_extra_js_url`,
  dashboards and the card picker could report "Custom element doesn't exist".
- The `documentationURL` of the BTC Address Card now points to this repository.

### Removed

- Stray empty file `custom_components/file`.

## [0.5.9.4] - 2026-10-19

### Fixed

- **Optional sensors without data:** The sensors *Next block median fee*,
  *Next block TX count* and *Projected mempool blocks* never received any data.
  The coordinator now fetches `/api/v1/fees/mempool-blocks` through
  `_fetch_with_retry` and returns the result as `mempool_blocks`. Previous
  values are kept if the endpoint is temporarily unavailable.
- **Misleading fallback values:** The three sensors above now report `unknown`
  instead of `0.0` / `0` when no data is available.
- **Difficulty adjustment remaining time:** The value is returned by the
  Mempool API in milliseconds and was converted incorrectly. The sensor now
  shows the correct number of hours.

  Thx to @frenck

### Changed

- Added `CONFIG_SCHEMA` (`config_entry_only_config_schema`) to satisfy Hassfest
  for an integration that is set up only via the UI.
- **BTC Address Card:**
  - The card is only registered once, even if the script is loaded twice.
  - Removed the theme selector from the card editor (it had no effect).
  - The card is re-rendered only when the selected entity or the language
    changes, instead of on every state update in Home Assistant.
  - The card title falls back to the entity name if the name selector returns
    a non-text value.

## Earlier versions

Changes before 0.5.9.4 are not listed here. See the
[GitHub releases](https://github.com/jinx-22/mempool_watch/releases).
