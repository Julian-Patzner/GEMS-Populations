# GEMS-Populations

Population and setting files for [GEMS](https://github.com/IMMIDD/GEMS), built from the
[GESyLand](https://gesyland.eu) synthetic population of Germany.

GEMS downloads these files itself, e.g. `Simulation(population = "DE")`. Available identifiers:
`DE` and the federal states `BB`, `BE`, `BW`, `BY`, `HB`, `HE`, `HH`, `MV`, `NI`, `NRW`, `RP`, `SH`,
`SL`, `SN`, `ST`, `TH`.

## Versions

Versions are `<GESyLand version>.<conversion revision>`. The files are attached to the
[releases](../../releases); every people and settings file stores its version under the JLD2
key `"version"`.


## Settings file

Key `"settings"` holds, per setting type, a `table` of its scalar columns and `vectors`, its
vector columns (`contains` on container settings), each stored flat as `values` and `offsets`:
setting `i` holds `values[offsets[i]:offsets[i+1]-1]`. Up to 3.1, key `"data"` held one DataFrame
per setting type with a vector per setting, which JLD2 stores as one dataset each.

## People file

| Column | Type | Meaning |
|---|---|---|
| `id` | Int32 | Individual id |
| `household` | Int32 | Household id |
| `age` | Int8 | Age in years |
| `sex` | Int8 | Sex |
| `occupation` | Int16 | Main activity at work, Mikrozensus EF172 (1-21); -1 if not employed or unknown |
| `industry` | Int16 | Industry of the workplace, WZ 2008, Mikrozensus EF137; -2 if unknown. Load with `ind_extension = [:industry]` |
| `education` | Int8 | Highest degree as ISCED 2011 level (1-8), Mikrozensus EF517; -1 if unknown or under 15 |
| `municipality` | Int32 | Municipality id |
| `schoolclass` | Int32 | School class id; -1 if none |
| `office` | Int32 | Office id; -1 if none |

Code meanings are listed in the
[Mikrozensus 2019 data handbook](https://www.forschungsdatenzentrum.de/sites/default/files/mz_2019_suf_dhb.pdf).

## Building

`gesyland_create_populations_v3.1.jl` creates all files from the GESyLand raw data, which is not
part of this repository.

## License

The code in this repository is licensed under GPL-3.0.
The population data is derived from GESyLand (© gesyland.eu) and used with the permission of its
developers. It contains data from © OpenStreetMap contributors, available under the
[ODbL](https://opendatacommons.org/licenses/odbl/).
