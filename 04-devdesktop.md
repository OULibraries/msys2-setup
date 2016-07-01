# Acquia Dev Desktop


## Basic Setup

[Download](https://www.acquia.com/downloads) and install the lastest Acquia Dev Desktop.

You may also want to add this alias to your `~/.bashrc` to make running drush easier:
```
alias drush="/C/Program\ Files\ \(x86\)/DevDesktop/drush/drush.bat"
```

## Copy a site from a remote host to Dev Desktop

First, create a site in your local Dev Desktop to sync with the remote site. 

Then log in to the remote host and dump the database for the remote site:
```
d7_dump.sh /srv/example
```

The resulting database dump will be stored at at `/srv/example/db/drupal_docs_dump.sql`. Copy it to your local computer by doing something like:
```
rsync -rv $HOSTNAME:/srv/example/db/drupal_docs_dump.sql /C/Users/jdoe/Sites/db
```
Copy the themes, modules and libraries:
```
rsync -rv $HOSTNAME:/srv/example/drupal/sites/all /C/Users/jdoe/Sites/acquia/example/sites 
```

Next, copy the content files from the remote site to your local site:
```
rsync -rv $HOSTNAME:/srv/example/default/files  /C/Users/jdoe/Sites/aquia/example/sites/defualt
```


