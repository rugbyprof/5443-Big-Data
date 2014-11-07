NOT DONE! ALMOST
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
This data is available here: [nfl_stats.tar.gz](http://107.170.214.232/~griffin/nfl_mongo/nfl_stats.tar.gz)

### Using Our Data

At this point we have a complete NFL roster, and stats for each game played since 2009. The stats themselves are stored in more of a linear fashion within each file containing some general stats at the top, and a re-cap of the game as events happened ordered temporally.

Given the data in it's current format doesn't bode well for querying. So, we have some decisions to make. Actually, you have some decisions to make. The major question is how will you store the NFL data within Mongo in order to "optimize" (that's an over statement) the following queries. Optimization is a term thrown around a lot, where our current goal is really to not "diminish" or querying ablities.

### Creating Your Collections

```python
import pymongo,string,json
import sys,os
import requests

#Link up with mongo 
from pymongo import MongoClient
conn = MongoClient()

#Connect to your database
db_nfl = conn.nfl

#Create collections
coll_players = db_nfl.players
coll_games = db_nfl.games

#Grab data from server
players = requests.get('http://107.170.214.232/~griffin/nfl_mongo/nfl_stats/players.json')

#loop through players
for player in players.json():
    _id = player                    # 'player' is actually the 'key'
    player = players.json()[_id]    # grab data using json[key]
    player['_id'] = _id             # place '_id' in the player object
    coll_players.insert(player)     # insert into db
```


- Create collections of teams and players.

1. Find the leading rusher in a given year. 
2. Find the team with the most fumbles.

db.nfl.find()           # Generic find all query
db.nfl.remove()         # Removes the nfl db from mongo
db.getCollectionNames() # Showes all collections in mongo
db.collections.stats()  # Gives you information on your collection (I used it to make sure I was adding proper number of entries)
db.players.find({"last_name":"Griffin"}).pretty()
```python

	"_id" : "00-0029857",
	"first_name" : "Ryan",
	"last_name" : "Griffin",
	"gsis_id" : "00-0029857",
	"weight" : 210,
	"years_pro" : 2,
	"profile_id" : 2541185,
	"number" : 4,
	"birthdate" : "11/17/1989",
	"height" : 77,
	"college" : "Tulane",
	"full_name" : "Ryan Griffin",
	"gsis_name" : "R.Griffin",
	"profile_url" : "http://www.nfl.com/player/ryangriffin/2541185/profile"
}
{
	"_id" : "00-0028377",
	"first_name" : "John",
	"last_name" : "Griffin",
	"gsis_id" : "00-0028377",
	"weight" : 208,
	"years_pro" : 2,
	"profile_id" : 2530842,
	"number" : 24,
	"birthdate" : "12/17/1988",
	"height" : 71,
	"college" : "Massachusetts",
	"full_name" : "John Griffin",
	"gsis_name" : "J.Griffin",
	"profile_url" : "http://www.nfl.com/player/johngriffin/2530842/profile"
}
```
