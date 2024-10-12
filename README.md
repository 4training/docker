# 4training.net local development version
Get a local version of the 4training.net website with just one command!
```
docker compose up
```

Then you should be able to access it on port 8082 on your local computer: http://localhost:8082

To change the port or make it available to other devices on your (local) network, see [.env](.env)

## Login
When the system is running locally, you can login here: http://localhost:8082/Special:UserLogin

There is different users, all having the same password `4training.net`:
* `admin`: full admin rights
* `ResourcesBot`, `CorrectBot`, `AutoTranslateBot`, `GenerateOdtBot`: bot users for different [python tools](https://github.com/4training/pywikitools/)
* `Translator`: with translator rights

To see what translators see look e.g. here: [Translate Hearing from God](http://localhost:8082/mediawiki/index.php?title=Special:Translate&group=page-Hearing+from+God&action=page&filter=&language=en)

Access to the mediawiki API: http://localhost:8082/mediawiki/api.php

## Using this for development
You can override a specific folder inside the docker container by mounting a host directory to the container. E.g. if you want to work on the [skin (frontend)](https://github.com/4training/mediawiki-skins-ForTraining) add a line in [docker-compose.yaml](docker-compose.yaml) so it looks like this:
```
 mediawiki:
    image: 4training/mediawiki
    ports:
      - "${MEDIAWIKI_PORT}:80"
    environment:
      MEDIAWIKI_HOST: ${MEDIAWIKI_HOST}
      MEDIAWIKI_PORT: ${MEDIAWIKI_PORT}
    volumes:
      - vol-www:/var/www/html/mediawiki
      - /your/path/to/mediawiki-skins-ForTraining:/var/www/html/mediawiki/skins/ForTraining
```
Then you can work in your local folder and changes will directly be reflected in the container (well after refreshing the page in the browser).

## Remarks
The database is a cleaned up version of the live website (no revisions included, personal / maybe sensitive data removed).
Port 8082 is hard coded at the moment (if you want to change that you would need to change `$wgServer` in `/var/www/html/mediawiki/LocalSettings.php` as well)

If you mess around with the database / files you can reset everything with `docker compose down --volumes`