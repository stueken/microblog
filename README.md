# microblog
##Description
tbd

Created on basis of the [Flask Mega-Tutorial by Miguel Grinberg](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-now-with-python-3-support) in Python 3.4.

##Features
- Dual language (English/German) support depending on the browser properties.
- Instant translations of blog posts in other languages using Ajax calls.

##Planned
- Deployment on Linux VPS

##Requirements
tbd

##Setup Instructions
tbd

##Known issues and solutions
- "TypeError: must be str, not bytes" when updating translations in Python 3.4. This can easily be solved by changing a line in the babel package (see https://github.com/mitsuhiko/flask-babel/issues/43)
- The OpenID-service is not supported anymore by several providers like Google or MyOpenID. However, the login with Yahoo or AOL should still function.
- The full text search functionality is disabled on the demo url as the heroku server doesn't support mysqlite (file based) databases. Making the full text search work on a Postgresql database would require several changes to the application. It is planned to deploy a fully working demo to a Linux VPS.

##Executables
tbd

##Deployment
tbd
