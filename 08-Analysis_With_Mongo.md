## NFL Analysis With MongoDB

Thanks to [BurntSushi](https://github.com/BurntSushi) for providing some really cool repo's.

### Data Sources

The NFL provides data through a couple of public api's that is available here:

- ___Roster:___ http://www.nfl.com/teams/roster?team=DAL
- ___Players:___ http://www.nfl.com/players/profile?id=2505629
- ___Schedule:___ http://www.nfl.com/ajax/scorestrip?season=2014&seasonType=REG&week=13
- ___Game Stats:___ http://www.nfl.com/liveupdate/game-center/2011111301/2011111301_gtd.json

There is probably much more available, but for what we need, this is sufficient. 

### Roster & Players

Using a file I found at [BurntSushi](https://github.com/BurntSushi), I've made available all the players for you to insert into your Mongo database. It is available here: [Players.json](http://107.170.214.232/~griffin/nfl_mongo/nfl_stats/players.json). A sample can be seen below.
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

### Game Stats

Using my own python script, I pulled the raw data from Nfl.com, using the aforementioned urls.
- ___Schedule:___ http://www.nfl.com/ajax/scorestrip?season=2014&seasonType=REG&week=13
- ___Game Stats:___ http://www.nfl.com/liveupdate/game-center/2011111301/2011111301_gtd.json

```python
import requests, json, urllib2, os, time
from lxml import etree

for year in range(2009,2015):
    for week in range(1,17):
        print year , week
        filename = 'json/games/'+str(year)+'-'+str(week)+'.json'
        
        if(os.path.isfile(filename) == False):
            f1 = open(filename,'w')
            url = 'http://www.nfl.com/ajax/scorestrip?season='+str(year)+'&seasonType=REG&week='+str(week)
            xml = urllib2.urlopen(url).read(10000)
            root = etree.XML(xml)

            gms = root[0]

            week_attr = dict(gms.attrib)
            f1.write(json.dumps(week_attr)+"\n")
            #print json.dumps(week_attr, sort_keys=True,indent=4, separators=(',', ': '))

            for game in gms:
                game_attr = dict(game.attrib)
                eid = game_attr['eid']
                print eid
                filename = 'json/stats/'+str(eid)+'.json'
                        
                if(os.path.isfile(filename) == False):
                    f2 = open(filename,'w')

                    #print json.dumps(game_attr, sort_keys=True,indent=4, separators=(',', ': '))
                    f1.write(json.dumps(game_attr)+"\n")

                    stats = requests.get('http://www.nfl.com/liveupdate/game-center/'+str(eid)+'/'+str(eid)+'_gtd.json')
                    if(stats.status_code != 200):
                        time.sleep(1)
                        stats = requests.get('http://www.nfl.com/liveupdate/game-center/'+str(eid)+'/'+str(eid)+'_gtd.json')
                        time.sleep(1)
                        
                    f2.write(json.dumps(stats.json()))

                    f2.close();
            f1.close();
```

- http://107.170.214.232/~griffin/nfl_mongo/nfl_stats.tar.gz

- Create collections of teams and players.


1. Find the leading rusher in a given year. 
2. Find the team with the most fumbles.

