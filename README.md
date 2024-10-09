# 4training.net local development version
Get a local version of the 4training.net website with just one command!
```
docker compose up
```

Then you should be able to access it on port 8082 on your local computer: http://localhost:8082

## Remarks
The database is a cleaned up version of the live website (no revisions included, personal / maybe sensitive data removed).
Port 8082 is hard coded at the moment (if you want to change that you would need to change `$wgServer` in `/var/www/html/mediawiki/LocalSettings.php` as well)

If you mess around with the database / files you can reset everything with `docker compose down --volumes`