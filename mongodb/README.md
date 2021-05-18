# Resotre mongodb

sudo mongorestore --db newdb --drop /var/backups/mongobackups/01-20-16/newdb/

mongorestore --db admin --drop /tmp/data/mongodb/mongodb_back_up/admin
mongorestore --db iot_log --drop  /tmp/data/mongodb/mongodb_back_up/iot_log

# Connect to mongodb

```
$ mongo --host <IP> --port <PORT>
$ mongo --username <USER> --password <PASSWORD> --authenticationDatabase admin --host <IP> --port 27017
```
