## Analysis With MongoDB

Thanks to [BurntSushi](https://github.com/BurntSushi) for providing some really cool repo's.


- http://www.nfl.com/liveupdate/game-center/2011111301/2011111301_gtd.json
- http://www.nfl.com/ajax/scorestrip?season=2014&seasonType=REG&week=13

- http://107.170.214.232/~griffin/nfl_mongo/nfl_stats.tar.gz

## Loading the data

Below is an example file of NFL players. It is available here: http://107.170.214.232/~griffin/nfl_mongo/nfl_stats/players.json
```json
[
    00-0003035: {
        birthdate: "4/20/1977",
        college: "Wake Forest",
        first_name: "Desmond",
        full_name: "Desmond Clark",
        gsis_id: "00-0003035",
        gsis_name: "D.Clark",
        height: 75,
        last_name: "Clark",
        profile_id: 2500080,
        profile_url: "http://www.nfl.com/player/desmondclark/2500080/profile",
        weight: 249,
        years_pro: 13
    },
    00-0003239: {
        birthdate: "8/16/1976",
        college: "East Carolina",
        first_name: "Rod",
        full_name: "Rod Coleman",
        gsis_id: "00-0003239",
        gsis_name: "R.Coleman",
        height: 74,
        last_name: "Coleman",
        profile_id: 2500137,
        profile_url: "http://www.nfl.com/player/rodcoleman/2500137/profile",
        weight: 285,
        years_pro: 10
    }
]
```

- Create collections of teams and players.


1. Find the leading rusher in a given year. 
2. Find the team with the most fumbles.

