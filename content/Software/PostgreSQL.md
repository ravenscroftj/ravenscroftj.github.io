---
aliases:
  - postgres
---

- PostgreSQL is an advanced relational [[Databases|database]] server.

## Minimal Docker with [[adminer]]
```yaml
  services:
	db:
	  image: postgres
	  restart: unless-stopped
	  environment:
		POSTGRES_PASSWORD: example
		PGDATA: /var/lib/postgresql/data/pgdata
	  volumes:
		- ./persistence/postgres:/var/lib/postgresql/data
  
	adminer:
	  image: adminer
	  restart: unless-stopped
	  ports:
		- 8080:8080
  ```

### Troubleshooting

- initdb: error: directory "/var/lib/postgresql/data" exists but is not empty
	- Tried:
		- `docker compose down`
		- `rm persistance/postgres` (mapped to the above path)
		- `docker compose up`
	-