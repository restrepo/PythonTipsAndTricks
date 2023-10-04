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
