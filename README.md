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

Next to basic features for a microblog like [OpenID](http://openid.net/)-login
(please see *Known Issues* below), create and delete posts, pagination, profile
pages with [(Gr)avatars](https://en.gravatar.com/), follow and unfollow users
as well as email follower notifications, the following features are not always
included:

*   Internationalization (i18n) and localization (l10n) through:

    *   Multi-language support depending on the browser properties with the
    [Babel package](https://pythonhosted.org/Flask-Babel/)

    *   Instant translations of blog posts in other languages by using Ajax
    calls with the [Microsoft Translator service](https://datamarket.azure.com/dataset/1899a118-d202-492c-aa16-ba21c33c06cb)

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

6.  Configure email server and address(es) of the admin(s)

    1.  Open the file `config.py` and fill email and admin information. For
        example, if you want the application to send emails via your GMail
        account you would enter the following:

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

    2.  `MAIL_USERNAME` and `MAIL_PASSWORD` are read from environment
    variables. Set them with `export
    MAIL_USERNAME=your-gmail-username@yourdomain.com` and `export
    MAIL_PASSWORD=your-mail-password`. If you want to store your login
    credentials persistently, then place the mentioned commands in the
    `~/.profile`-file.

    **Note**:
    In order to function with GMail, you need to login into your account
    and activate ["Access for less secure apps"](https://www.google.com/settings/u/1/security/lesssecureapps).

7.  Optional: Add additional language(s) (English and German already supported)

    1.  Add the language to the list of available languages, e.g. Spanish:

        ```python
        # available languages
        LANGUAGES = {
            'en': 'English',
            'de': 'Deutsch',
            'es': 'Español'
        }
        ```

    2.  Add a language to the translation catalog, e.g. Español
    (language-code = es): `./tr_init.py es`

    3.  If not done already, install [Poedit Translations Editor](http://poedit.net/): `sudo apt-get install poedit`

    4.  Run `poedit`, fill in the target language in *catalog > properties*,
    install the respective spellchecker directory if asked for, open the
    `messages.po`-file from the language folder, e.g. `app/transaltions/es`,
    add all translations and save the file.

    5.  Compile the `messages.po` file: `./tr_compile.py`

    6.  Show timestamps in the target language as well. Open
        `app/templates/base.html` and add an 'elif'-statement to the header
        like shown here for Spanish (es):

        ```htmldjango
        ...
        <script src="/static/js/moment-with-locales.min.js"></script>
        {% if g.locale == 'de' %}
            <script>moment.locale('de');</script>
        {% elif g.locale == 'es' %}
            <script>moment.locale('es');</script>
        {% else %}
            <script>moment.locale('en');</script>
        {% endif %}
        ...
        ```

    7.  To check translation, modify the language settings in your browser so
    that like in this example Spanish is the preferred language.

8.  Create the database: `./db_create.py`

9.  Start up the web server with the application in production mode:`./runp.py`
and open <http://127.0.0.1:5000> in your browser. Enjoy!

## Commands

Run with `./command.py` from root directory. If permission is denied, give it
executable permission with `$ chmod a+x command.py`. The following are
available:

| Command           | Description                                             |
| ----------------- | ------------------------------------------------------- |
| `run.py`          | Start up the development web server with the application. |
| `runp.py`         | Like above, but with debugging disabled (production mode). |
| `tests.py`        | Run all unittests.                                      |
| `db_create.py`    | Create the database.                                    |
| `db_migrate.py`   | Generate a database migration after changes to the database structure occured. |
| `db_upgrade.py`   | Upgrade the database to the latest revision.            |
| `db_downgrade.py` | Downgrade the database one revision. This can be done multiple times to downgrade several revisions. |
| `tr_init.py`      | Add a language to the translation catalog.              |
| `tr_compile.py`   | Update the catalog with new texts from source and templates. |
| `tr_update.py`    | Compile the catalog (messages.mo file)                  |

## Deployment

*   tbd

## Known issues and Solutions

*   "TypeError: must be str, not bytes" when updating translations in
Python 3.4. This can easily be solved by changing a line in the babel
package (see <https://github.com/mitsuhiko/flask-babel/issues/43>)

*   The login over OpenID is limited to a Yahoo or AOL account as several
providers (like Google) dropped their support for the OpenID-service.

*   The full text search functionality is disabled on the demo url as
the heroku server doesn't support mysqlite (file based) databases.
Making the full text search work on a Postgresql database would
require several changes to the application. It is planned to deploy a
fully working demo to a Linux VPS.

## Planned

*   Deployment on Linux VPS
*   Update user authentication to OAuth 2.0

## License

tbd

## References

Styleguides used:

*   for Commits: [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)
*   for Markdown: [Remark rules](https://github.com/wooorm/remark-lint/blob/master/doc/rules.md)
