---
created: 2024-01-29T08:13
updated: 2024-01-30T14:01
---
alias:: Software/Adminer

- Adminer is a [[foss]] GUI tool for administration of [[Databases]]. I tend to use it for [[MySQL]] and [[Public/Software/PostgreSQL]] administration.
- ## Timeouts when connecting to [[Public/Software/PostgreSQL]] over Docker  
  
  Looks like `ufw` can get in the way - disabling this service with `sudo service ufw stop` can help.
- ## Minimal Docker-Compose Config  
  
  ```yaml
  version: "3.0"
  services:
  
    adminer:
      env_file: .env
      image: adminer:latest
      #restart: always
      links:
          - db
      ports:
        - 8080:8080
  ```
-