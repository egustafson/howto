The following is the process I followed to install MediaWiki:

* lighttpd
* sqlite  (mysql)
* php5

----

I.  Install prerequisites:

```
(apt-get install mysql-server mysql-client)
apt-get install lighttpd
apt-get install php5-cgi php5
```

    * edit /etc/php5/cgi/php.ini to enable php5 in lighttpd
        - uncomment the line 'cgi.fix_pathinfo=1
    * enable the fastcgi configuration in lighttpd

```
lighttpd-enable-mod fastcgi
lighttpd-enable-mod fastcgi-php
service lighttpd force-reload
```

    * install php5-sqlite  (php5-mysql)

``` 
apt-get install php5-sqlite  (apt-get install php5-mysql)
service lighttpd restart
```

    * Optional add-ons

```
apt-get install imagemagick php5-gd php5-cli 
service lighttpd restart
```

II.  install MediaWiki ( and optional add-on(s) )
    sudo apt-get --no-install-recommends install mediawiki 
    sudo apt-get install mediawiki-math

III. map the MediaWiki installation (/var/lib/mediawiki) into lighttpd's space
    * Add the following to lighttpd's configuration
    alias.url += ( "/wiki" => "/var/lib/mediawiki/" )

4. Reload/start lighttpd to effect configuration changes
    service lighttpd restart

5. (Sqlite) Create a data directory
    mkdir /var/lib/mediawiki-data
    chown www-data.www-data /var/lib/mediawiki-data

5. Browse to the wiki root [http://hostname/wiki] and complete
   configuration.

6. Copy configuration as directed on final configuration web page.
    cp /var/lib/mediawiki/config/LocalSettings.php /etc/mediawiki/LocalSettings.php
    chown www-data /etc/mediawiki/LocalSettings.php
    chmod 600 /etc/mediawiki/LocalSettings.php
    rm -rf /var/lib/mediawiki/config

7. Done.
