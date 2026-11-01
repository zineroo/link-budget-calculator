# Satellite Link Budget Calculator

A browser-based uplink budget calculator for geostationary satellites. Enter earth-station and carrier parameters and it works out whether the link closes, and by how much margin, for any DVB-S2 MODCOD.

**Live demo:** https://zineroo.github.io/link-budget-calculator/

## What it calculates

| Step | Formula |
|---|---|
| Antenna gain | G = 10·log₁₀(η · (πD/λ)²) |
| EIRP | P_tx (dBW) + G − feed loss |
| Slant range (GEO) | d = √((Rₑ+h)² − (Rₑ·cos El)²) − Rₑ·sin El |
| Free-space path loss | FSPL = 20·log₁₀(d_km) + 20·log₁₀(f_GHz) + 92.45 |
| Carrier-to-noise density | C/N₀ = EIRP − FSPL − losses + G/T + 228.6 |
| Es/N₀ | C/N₀ − 10·log₁₀(R_s) |
| Link margin | Es/N₀ received − Es/N₀ required by the MODCOD |

It also shows the useful bitrate (symbol rate × MODCOD spectral efficiency), the occupied bandwidth (symbol rate × (1 + roll-off)), and a line-by-line budget ledger.

MODCOD thresholds are the ideal quasi-error-free values from ETSI EN 302 307 (DVB-S2), normal FECFRAME, no pilots.

## Why I built it

I work in a satellite uplink control center, where link margin decides whether a carrier survives a storm. I wanted a tool that shows the whole budget at a glance, so you can see exactly where the dBs go and what changes when you swap a dish, an amplifier or a MODCOD.

## How it was built

I defined the requirements (which parameters, which formulas, DVB-S2 MODCOD thresholds, what the output should show) and verified every calculation by hand against standard satcom references. The code was written with AI assistance (Claude), then reviewed and tested by me.

## Running it

No install or build step. Open `index.html` in any browser, or use the live demo above.

## Limitations

- Uplink only. An end-to-end budget would also combine the downlink C/N and transponder intermodulation.
- Rain fade is entered manually rather than computed from the ITU-R P.618 model.
- Ideal thresholds; real modems need about 0.5–1 dB of implementation margin.

## Roadmap

- [ ] Downlink budget and combined end-to-end C/N
- [ ] ITU-R P.618 rain attenuation from location and availability target
- [ ] Elevation angle calculated from earth-station coordinates and satellite longitude
- [ ] Shareable links that save inputs in the URL

## Author

Jawad Ahmad — [@zineroo](https://github.com/zineroo)

## License

MIT © 2026 Jawad Ahmad (@zineroo). See [LICENSE](LICENSE).
