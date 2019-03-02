[2016 242 What's New in Core Data](https://developer.apple.com/videos/play/wwdc2016/242/)


- Melissa Turner, Software Engineer
- Scott Perry, Software Engineer

Roadmap

```
Query Generations 
Concurrency
Core Data Stack Configuration
New API
Swift - Generic? 
Xcode Integration
Demo - Walking tour | 3020
What's New in SQLite |  | | p156
```

## Xcode - Automatic Subclass Generation | | 2830 | 

### Always up to date

- Configured per entity
- DerivedData
- Automatically regenerated
- Class or extension

### Class generation (in Objective-C)

- MyApp+CoreDataModel.h
- Subclass+CoreDataClass.h
- Subclass+CoreDataProperties.h

### Category/Extension generation (in Objective-C)

- MyApp+CoreDataModel.h
- Subclass+CoreDataProperties.h
- Subclass.h

## What's New in SQLite | Scott Perry | 3325 | p156


### Multithreading Assertions (NEW)

- Database connections are not thread-safe
- Multithreading bugs manifest as crashes deep inside SQLite
- SQLITE_ENABLE_THREAD_ASSERTIONS=1

### Built-in Logging

- SQLite allows user-defined logging functions via SQLITE_CONFIG_LOG
- sqlite3_config must be called before library initialization
- SQLITE_ENABLE_LOGGING=1 (NEW)

### File Operations and SQLite - Or: How to corrupt your database

- Databases are represented by multiple files
- File operations cannot be atomic across multiple files
- All file operations are unsafe


### The problem with file operations


### Database file tracking

- SQLite now uses dispatch sources to track illegal file operations
- API calls after illegal operations will return SQLITE_IOERR_VNODE
NEW
- SQLITE_ENABLE_FILE_ASSERTIONS=1

https://www.sqlite.org/howtocorrupt.html

### What Is Safe? - How to avoid database corruption

- Clear database ownership
- Guarantee exclusive file access
- Use Core Data!
  - replacePersistentStore()
  - destroyPersistentStore()

