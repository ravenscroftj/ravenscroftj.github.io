alias:: Software/Adminer

- Adminer is a [[foss]] GUI tool for administration of [[Databases]]. I tend to use it for [[mysql]] and [[Public/Software/PostgreSQL]] administration.
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