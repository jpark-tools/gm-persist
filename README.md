# gm-persist

Lightweight utility & persistence helpers for [Tampermonkey](https://www.tampermonkey.net/) / [Violentmonkey](https://violentmonkey.github.io/) userscripts.

## Features

- **`formatPnL(value)`** — Format a numeric value as a PnL string (`+$12.50` / `-$3.20`)
- **`uid()`** — Generate a short unique ID (base36 timestamp + random suffix)
- **`ts([date])`** — Locale-formatted timestamp (`HH:MM:SS`)
- **`dateKey([date])`** — ISO date key (`YYYY-MM-DD`)
- Built-in `GM_setValue` / `GM_getValue` state persistence with cross-tab deduplication
- Zero dependencies, < 2 KB minified

## Installation

Add to your userscript header:

```js
// @require  https://cdn.jsdelivr.net/gh/jpark-tools/gm-persist@2.5.0/index.js
```

## Usage

```js
// Access utilities via the global GMPersist object
const utils = GMPersist;

console.log(utils.formatPnL(42.5));    // "+$42.50"
console.log(utils.formatPnL(-8.3));    // "-$8.30"
console.log(utils.uid());              // "m1a2b3c4d5"
console.log(utils.ts());              // "14:32:07"
console.log(utils.dateKey());          // "2026-02-08"
```

### State persistence

If `GM_setValue` is available, gm-persist automatically handles storage normalization and cross-tab deduplication for your userscript state. No additional configuration needed — just use `GM_setValue` / `GM_getValue` as usual.

## API

| Method | Params | Returns | Description |
|--------|--------|---------|-------------|
| `formatPnL` | `value: number` | `string` | Formats a PnL value with sign and `$` prefix |
| `uid` | — | `string` | Short unique identifier |
| `ts` | `date?: Date` | `string` | Locale time string (fr-FR) |
| `dateKey` | `date?: Date` | `string` | ISO date portion (`YYYY-MM-DD`) |

## Compatibility

- Tampermonkey ≥ 4.x
- Violentmonkey ≥ 2.x
- Greasemonkey ≥ 4.x (limited — no `GM_setValue` persistence)

## Building

The distributed `index.js` is built with Rollup + Terser. Source is in `src/`.

```bash
npm run build
```

## License

[MIT](LICENSE)
