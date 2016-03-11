# microblog

## Description

A small social microblogging platform created on basis of the [Flask Mega-Tutorial by Miguel Grinberg](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-now-with-python-3-support) in Python 3.4.

You are welcome to try it out at http://socialmicroblog.herokuapp.com/ and follow [my profile](http://socialmicroblog.herokuapp.com/user/Norbert)!

## Screenshots

![Profile](http://img5.fotos-hochladen.net/uploads/profilesmz0xn56qe43.jpg)

## Features

-	Profile Pages with Avatars
-	Follow and Unfollow Users
-	Dual language (English/German) support depending on the browser properties.
-	Instant translations of blog posts in other languages using Ajax calls.
-	OpenID-Login (outdated, more details below)
-	Full Text Search (doesn't work on demo site, more details below)



## Planned

-	Deployment on Linux VPS

## Requirements

See requirements.txt

## Setup Instructions

tbd

## Known issues and Solutions

-	"TypeError: must be str, not bytes" when updating translations in Python 3.4. This can easily be solved by changing a line in the babel package (see https://github.com/mitsuhiko/flask-babel/issues/43\)
-	The OpenID-service is not supported anymore by several of the listed providers (Google, MyOpenID, flickr). However, the login with Yahoo or AOL should still work.
-	The full text search functionality is disabled on the demo url as the heroku server doesn't support mysqlite (file based) databases. Making the full text search work on a Postgresql database would require several changes to the application. It is planned to deploy a fully working demo to a Linux VPS.

## Executables

Run with `$ ./EXECUTABLE.py` from root directory. If permission is denied, give it executable permission with `$ chmod a+x EXECUTABLE.py`. - run.py: Start up the development web server with the application. - runp.py: Start up the development web server with the application, but with debugging disabled (production mode). - tests.py: Run all unittests. - db_create.py: Create the database. - db_migrate.py: Generate a database migration after changes to the database structure occured. - db_upgrade.py: Upgrade the database to the latest revision. - db_downgrade.py: Downgrade the database one revision. This can be done multiple times to downgrade several revisions. - tr_init.py: Add a language to the translation catalog. - tr_compile.py: Update the catalog with new texts from source and templates. - tr_update.py: Compile the catalog (messages.mo file)

## Deployment

tbd
