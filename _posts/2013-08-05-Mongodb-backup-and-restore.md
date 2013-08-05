---
published: true
---

---
layout: post
title: Mongodb backup and restore
---
## MongoDB backup
To take backup of mongodb database
    $ monogodb -db database_name > database_name.bson
    
To restore backup file to database
    $ mongorestore -db database_name folder_name