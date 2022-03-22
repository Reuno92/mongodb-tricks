# Mongo DB Tricks

## Different kind of dump

### 1 - Import/ Export

#### Export
```bash
mongodump -d <database_name> -o <directory_backup>
```

#### Import 
```bash
mongodump -d <database_name> -o <directory_backup>
```

> It recommends against using mongodump/mongorestore for big data storages. It is very slow and once you get past 10/20GB of data it can take hours to restore.
>
> [Mentor Reka](https://stackoverflow.com/questions/11255630/how-to-export-all-collections-in-mongodb) 

### 2 - MongoDump/MongoRestore

#### [MongoDump](https://docs.mongodb.com/database-tools/mongodump/)

1 - by URI
```bash
mongodump --uri="mongodb://mongodb0.example.com:27017" [additional options]
```

2 - by host
```bash
mongodump --host="mongodb0.example.com:27017"  [additional options]
```
 
3 - by host and port
```bash
mongodump --host="mongodb0.example.com" --port=27017 [additional options]
```

**[Options](https://docs.mongodb.com/database-tools/mongodump/#std-option-mongodump.--config)**

Specifies the full path to a YAML configuration file containing sensitive values for the following options.

* [password](https://docs.mongodb.com/database-tools/mongodump/#std-option-mongodump.--password)
* [uri](https://docs.mongodb.com/database-tools/mongodump/#std-option-mongodump.--uri)
* [sslPemKeyPassword](https://docs.mongodb.com/database-tools/mongodump/#std-option-mongodump.--sslPEMKeyPassword)

This is the recommended way to specify a password to mongodump, aside from specifying it through a password prompt.

The configuration file takes the following form:
```yaml
password: <password>
uri: mongodb://mongodb0.example.com:27017
sslPEMKeyPassword: <password>
```

> Specifying a password to the password: field and providing a connection string in the uri: field which contains a conflicting password will result in an error.

#### [MongoStore](https://docs.mongodb.com/database-tools/mongorestore/#mongorestore)

The mongorestore program loads data from either a binary database dump created by mongodump or the standard input into a mongod or mongos instance.

The mongorestore command has the following form:

```bash
mongorestore <options> <connection-string> <directory or file to restore>
```

**[Options](https://docs.mongodb.com/database-tools/mongorestore/#options)**

Same as `mongodump`, you may use [YAML configuration file](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--config).

* [uri](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--uri)
* [host](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--host)
* [port](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--port)
* [username](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--username)
* [password](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--password)
* [awsSessionToken](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--awsSessionToken)
* [ssl](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--ssl), [sslCAFile](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--sslCAFile) or [sslPEMKeyPassword](https://docs.mongodb.com/database-tools/mongorestore/#std-option-mongorestore.--sslPEMKeyPassword)

> **Note**: That's options remain valid with `mongodump` command.

### 3 - DockerFile

