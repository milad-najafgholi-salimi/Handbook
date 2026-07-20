### Syntax:
```
CREATE DATABASE database_name;
```

With options:
```
CREATE DATABASE mydb
    OWNER = myuser
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.UTF-8'
    LC_CTYPE = 'en_US.UTF-8'
    TEMPLATE = template0;
```

#### Verify Creation
List all databases:
```
\l
```
