+++
title = 'PostgreSQL'
date = 2025-07-22T12:17:56+07:00
tags = ["dbms", "sql", "database", "cheatsheet", "postgres"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A short guide on working with PostgreSQL"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# PostgreSQL guide

## Connection Commands

1. **psql**
    - Definition: The PostgreSQL interactive terminal for connecting to a PostgreSQL database.
    - Usage:
        
        ```sql
        psql -h hostname -p port -U username -d database
        ```
        
2. **\connect (or \c)**
    - Definition: Connects to a new database and/or under a different user.
    - Usage:
        
        ```sql
        \\c database_name [username]
        ```
        
3. **\password**
    - Definition: Changes the password for the currently connected user.
    - Usage:
        
        ```sql
        \\password [username]
        ```
        
4. **\conninfo**
    - Definition: Displays information about the current database connection.
    - Usage:
        
        ```sql
        \\conninfo
        ```
        
5. **\encoding**
    - Definition: Shows or sets the client encoding.
    - Usage:
        
        ```sql
        \\encoding [encoding_name]
        ```
        
6. **\quit (or \q)**
    - Definition: Exits the psql program.
    - Usage:
        
        ```sql
        \\q
        ```
        

## Database Management

1. **CREATE DATABASE**
    - Definition: Creates a new PostgreSQL database.
    - Usage:
        
        ```sql
        CREATE DATABASE database_name
        WITH
          OWNER = role_name
          ENCODING = 'UTF8'
          LC_COLLATE = 'en_US.UTF-8'
          LC_CTYPE = 'en_US.UTF-8'
          TEMPLATE = template0
          CONNECTION LIMIT = -1;
        
        ```
        
2. **DROP DATABASE**
    - Definition: Removes a database from the PostgreSQL server.
    - Usage:
        
        ```sql
        DROP DATABASE [IF EXISTS] database_name;
        
        ```
        
3. **ALTER DATABASE**
    - Definition: Changes the attributes of a database.
    - Usage:
        
        ```sql
        ALTER DATABASE database_name RENAME TO new_name;
        ALTER DATABASE database_name OWNER TO new_owner;
        ALTER DATABASE database_name SET parameter TO value;
        
        ```
        
4. **\list (or \l)**
    - Definition: Lists all databases in the PostgreSQL server.
    - Usage:
        
        ```sql
        \\l
        ```
        
5. **\db+**
    - Definition: Lists all tablespaces with additional information.
    - Usage:
        
        ```sql
        \\db+
        ```
        
6. **CREATE TABLESPACE**
    - Definition: Defines a new tablespace for the database cluster.
    - Usage:
        
        ```sql
        CREATE TABLESPACE tablespace_name
        OWNER role_name
        LOCATION 'directory_path';
        
        ```
        
7. **pg_dump**
    - Definition: Extracts a PostgreSQL database into a script file or other archive file.
    - Usage:
        
        ```sql
        pg_dump -h hostname -p port -U username -F format -f output_file database_name
        ```
        
8. **pg_restore**
    - Definition: Restores a PostgreSQL database from an archive file created by pg_dump.
    - Usage:
        
        ```sql
        pg_restore -h hostname -p port -U username -d database_name archive_file
        ```
        
9. **\copy**
    - Definition: Performs a frontend (client) copy operation to import or export data.
    - Usage:
        
        ```sql
        \\copy table_name FROM 'filename' WITH (FORMAT csv, HEADER true);
        \\copy table_name TO 'filename' WITH (FORMAT csv, HEADER true);
        ```
        
10. **VACUUM**
    - Definition: Garbage collection and optional analysis of a database.
    - Usage:
        
        ```sql
        VACUUM [FULL] [FREEZE] [VERBOSE] [ANALYZE] [table_name [(column_name [, ...])]]
        ```