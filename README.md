This is a small helper program that simplifies scraping game information from the website "howlongtobeat.com". The user only needs to provide the name of the game that they wish to look up and the module will return a dictionary with the games details.

I leave it up to the site to do best effort on game matching. If a game cannot be found, a dictionary with an `error` key pair will be returned.

### Installation
Two simple ways to use this package as is:

#### Install via pip
Run the following command to install to your environment (includes dependencies):
`pip install git+git://github.com/fuzzylimes/howlongtobeat-scraper.git`

#### Install via setup.py
* Clone the repo from github
* Navigate into the folder and run `pip install .`

### Usage
The script can be used two different ways: standalone and from within another script. The user will provide the title of the game, and the module will return a dictionary with the following details:

```
{
    game_title: {
        'url': game_url, 
        'Main Story': main_hours, 
        'Main + Extra': extra_hours, 
        'Completionist': complete_hours
    }
}
```

For example, sending a query for `Final Fantasy` would return the following:
```
{
    'Final Fantasy': {
        'url': 'https://howlongtobeat.com/game.php?id=3480', 
        'Main Story': '17½Hrs', 
        'Main + Extra': '23½Hrs', 
        'Completionist': '35Hrs'
    }
}
```

#### Standalone
Run the following from the command line: `python3 scraper.py <game title>`
Example: `python3 scraper.py Final Fantasy`

#### Imported
##### Installed
If you've installed the module using setup.py, you can import by using the following:
```python
from hltbScraper import HLTB
```

Then to use in your script, simply use `HLTB(game_name)` to get a dictionary with the query results.

##### Copied file
* Import scraper.py into your project
* Use scraper.HLTB(game_title) to get game data
   * This will return the python dictionary detailed above

Example: `result = scraper.HLTB('Final Fantasy')`

#### Handling Exceptions
If the searched game cannot be found, an `Exception` will be raised with an error message. Here's an example of how to setup up your search to utlize this:

```python
try:
    HLTB("asdfasdf")
except Exception as e:
    print(e)
```