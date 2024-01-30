---
created: 2024-01-29T08:13
updated: 2024-01-30T14:12
---
## Minimal [[Docker]] Compose example with MySQL and [[adminer]]

```yaml
version: "3.0"  
services:
  mysql:
    env_file: .env
    image: mariadb
    environment:
      MARIADB_ROOT_PASSWORD: example
    volumes:
      - ./mysql:/var/lib/mysql
    ports:
      - 3306:3306
  
  adminer:
    env_file: .env
    image: adminer:latest
    ports:
	  - 8081:8080
```
	
## Converting Text to Varchar
  
 Use case: we want to add a `KEY` index to a text column in order to do exact match lookups

### Data Too Long
  
  Use `set sql_mode='';` to allow mysql to silently truncate stuff [^1]
  
### Doing the Conversion
  
  ```sql
  ALTER TABLE `tablename`  MODIFY `columnName`  varchar(255) 
  ```
  
  [^1]: https://dba.stackexchange.com/questions/298724/data-too-long-for-column-when-to-alter-column-definition