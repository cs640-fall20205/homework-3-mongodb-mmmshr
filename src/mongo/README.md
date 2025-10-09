# Mongo

## Start the database

```
./up.bash
```

## Stop the database

It's data will be lost. Make sure you dump it first.

```
./down.bash
```

## Connect to the database

```
./shell.bash
```

## Run a script in the database

```
./run.bash < script-file.js
```

## Dump your running database

Replace `dump_dir` with the name of the directory you want to
dump your data to.

```
./dump.bash dump_dir
```

## Load dump into your running database

Start with a fresh database. Replace `dump_dir` with the directory that
contains the data you want to load.

```
./load.bash dump_dir
```
# Modify your dump.bash file to look like:
```
#!/usr/bin/env bash

SCRIPT_DIR="$( cd -- "$( dirname -- "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )"
cd "${SCRIPT_DIR}"

docker compose exec mongo mongodump --uri="mongodb://mongo:gonmo@localhost" --out /data/db/dump
sudo cp -R /tmp/mongo/dump "${1}"
sudo rm -rf /tmp/mongo/dump
```

# Do the following process when developing where "name" is the name of your database.
```
rm name  #  If the folder already exists, skip if it does not exist

./dump.bash name

sudo chown -R $(whoami) /workspaces/homework-3-mongodb-HeidiEllis/src/mongo/name

./shell.bash    # Do all your work

./dump.bash name
```
