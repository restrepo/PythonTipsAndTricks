# Mongo
## Dump
```bash
mongodump -d la
#To restore in a new mongo without the la database:
mongorestore ./dump/
```
## Extract JSON
```bash
mongoimport --db la --collection data --file /scratch/restrepo/argentina.json --jsonArray
```
## PyMongo
```python
from pymongo import MongoClient
client = MongoClient()
client.list_database_names()
```
Output:
```
[...
br,
...]
```
Select database
```python
db = client['br']
db.list_collection_names()
```
Output:
```
[...
stage,
...]
```
Select collection
```python
cn=db.get_collection('stage')
cn.count_documents({})
```

Operations:
* PyMongo
  * `client.drop_database('br')`
  * `empty = list(client["br"]["cache_cites_count"].find({"empty":True}))`
* Moai    
  * `./moai_gscites_count_run --db_name br --create_cache && ./moai_gscites_count_run --db_name la --jobs 72 --apikey XXX`
* ScraperAPI
 * http://api.scraperapi.com/account?api_key=XXX  
    
 
