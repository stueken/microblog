# microblog

## Description

A small social microblogging platform created on basis of the [Flask Mega-
Tutorial by Grinberg](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-now-with-python-3-support)
in Python 3.4.

You are welcome to try it out at <http://socialmicroblog.herokuapp.com/> and
follow [my profile](http://socialmicroblog.herokuapp.com/user/Norbert)!

## Screenshots

![Profile](http://img5.fotos-hochladen.net/uploads/profilesmz0xn56qe43.jpg)

## Features

*   [OpenID](http://openid.net/)-login (please see *Known Issues* below)

*   Create and delete posts

*   Pagination

*   Profile pages with [(Gr)avatars](https://en.gravatar.com/)

*   Follow and unfollow users

*   E-mail notifications for new followers

*   Dual language (English/German) support depending on the browser properties

*   Instant translations of blog posts in other languages by using Ajax calls
with the [Microsoft Translator service](https://datamarket.azure.com/dataset/1899a118-d202-492c-aa16-ba21c33c06cb)

*   Full text search (please see *Known Issues* below)

## Requirements

*   See requirements.txt

## Setup and configuration (on local Ubuntu 14.04)

1.  Clone this repository:
`git clone https://github.com/stueken/microblog.git` and change into the
application folder: `cd microblog`  

2.  If not done already, install the virtual environment package for Python 3.4:
`sudo apt-get install python3.4-venv`

3.  Create a virtual environment: `python3 -m venv flask`

4.  Activate the virtual environment: `source flask/bin/activate`

5.  Install all required packages: `pip install -r requirements.txt`

    **Note**: If you experience problems with installing the
    psycopg2-package in your virtual environment, run `sudo apt-get
    install libpq-dev python-dev` as explained in [this post](https://web.archive.org/web/20110305033324/http://goshawknest.wordpress.com/2011/02/16/how-to-install-psycopg2-under-virtualenv/).

6.  Open the file `config.py` and fill in/replace the following information:

    1.  **Email server and address(es) of the admins**

        For example, if you want the application to send emails via your
        GMail account you would enter the following:

        ```python
        # email server
        MAIL_SERVER = 'smtp.googlemail.com'
        MAIL_PORT = 465
        MAIL_USE_TLS = False
        MAIL_USE_SSL = True
        MAIL_USERNAME = os.environ.get('MAIL_USERNAME')
        MAIL_PASSWORD = os.environ.get('MAIL_PASSWORD')

        # administrator list
        ADMINS = ['your-gmail-username@gmail.com']
        ```

        **Note**:

        *   `MAIL_USERNAME` and `MAIL_PASSWORD` are read from environment
        variables. Set them with `export
        MAIL_USERNAME=your-gmail-username@yourdomain.com` and `export
        MAIL_PASSWORD=your-mail-password`. If you want to store your login
        credentials persistently, then place the mentioned commands in the
        `~/.profile`-file.

        *   In order to function with GMail, you need to login into your
        account and activate ["Access for less secure apps"](https://www.google.com/settings/u/1/security/lesssecureapps).


7.  Create the database: `./db_create.py`

8.  Start up the web server with the application in production mode:`./runp.py`
and open <http://127.0.0.1:5000> in your browser

## Executables

Run with `./foo.py` from root directory. If permission is denied,
give it executable permission with `$ chmod a+x foo.py`. The following
executables out of the following categories are available:

**Run**

*   `run.py`: Start up the development web server with the application.

*   `runp.py`: Start up the development web server with the
application, but with debugging disabled (production mode).

**Test**

*   `tests.py`: Run all unittests.

**Database**

*   `db_create.py`: Create the database.

*   `db_migrate.py`: Generate a database migration after changes to
the database structure occured.

*   `db_upgrade.py`: Upgrade the database to the latest revision.

*   `db_downgrade.py`: Downgrade the database one revision. This can
be done multiple times to downgrade several revisions.

**Languages**

*   `tr_init.py`: Add a language to the translation catalog.

*   `tr_compile.py`: Update the catalog with new texts from source
and templates.

*   `tr_update.py`: Compile the catalog (messages.mo file)

## Deployment

*   tbd

## Known issues and Solutions

*   "TypeError: must be str, not bytes" when updating translations in
Python 3.4. This can easily be solved by changing a line in the babel
package (see <https://github.com/mitsuhiko/flask-babel/issues/43>)

*   The OpenID-service is not supported anymore by several of the
listed providers (Google, MyOpenID, flickr). However, the login with
Yahoo or AOL should still work.

*   The full text search functionality is disabled on the demo url as
the heroku server doesn't support mysqlite (file based) databases.
Making the full text search work on a Postgresql database would
require several changes to the application. It is planned to deploy a
fully working demo to a Linux VPS.

## Planned

*   Deployment on Linux VPS

## License

tbd

## References

Styleguides used:

*   for Commits: [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)
*   for Markdown: [Remark rules](https://github.com/wooorm/remark-lint/blob/master/doc/rules.md)
