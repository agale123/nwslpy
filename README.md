# nwslpy <img src='man/figures/nwslR.png' align="right" height="139" />

`nwslpy` is a Python wrapper around the [nwslR](https://github.com/nwslR/nwslR) package. The goal of this package is to make the data from `nwslR` available to even more people.

If you see anything you’d like added, changed, or updated, please open up a new issue of your own. If you are interested in contributing, please contact us directly. If you use this data in any work, please cite us.

## Installing the package

This package requires an R installation with the `devtools` library installed.

### Temporary development steps

First you will need to clone this repository and switch into that directory:

```
git clone https://github.com/agale123/nwslpy.git
cd nwslpy
```

To install the package, run:

```
python setup.py install
```

## API

- `load_player_match_stats(match_id)`: Loads player level stats for a given
  match
- `load_player_season_stats(team_id, season)`: Loads player level stats for a
  team/season
- `load_team_match_stats(match_id)`: Loads team level stats for a given match
- `load_team_season_stats(team_id, season)`: Loads team level stats for a team/season
- `load_matches()`: All matches from 2016-present with information and
  match IDs
- `load_players()`: All players rostered from 2016-present with
  information and player IDs
- `load_teams()`: All teams active from 2016-present with information
  and team IDs
- `load_metrics()` All metrics available from scrapers with definitions.
  Not all metrics are available for all players/matches/teams/etc.

## Usage

If you wanted to see the list of matches that were won on penalties, you could try:

```py
import nwslpy

# Load all matches and filter to ones in the year 2022
matches = nwslpy.load_matches()
matches[matches["won_on_penalties"]]
```

If you wanted to see which players took the most shots in the 2022 NWSL Championship, you could try 

```py
import nwslpy

stats = nwslpy.load_player_match_stats("portland-thorns-fc-vs-kansas-city-current-2022-10-29")
players = nwslpy.load_players()

stats[["player_id", "shots_total"]].groupby("player_id").sum("shots_total").join(
    players.set_index("player_id")
)[["shots_total", "player_match_name"]].sort_values("shots_total", ascending=False)
```

For more complicated examples, including how to visualize the data, check out the [examples](examples/) directory.


## Package structure

<pre>
nwslpy
├── LICENSE
├── README.md
├── examples
│   └── example_1.ipynb
├── nwslpy
│   ├── __init__.py
│   └── nwslpy.py
└── setup.py
</pre>