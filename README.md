# smskrupp

smskrupp **implements SMS lists** on top of [gammu](https://github.com/gammu/gammu). Gammu does all the lower-level talking to the modem.

It has a command-line interface and a Web interface for list management.

## Usage

Use the `smskrupp` command to manage groups:

    $ ./smskrupp add-group test t
    $ ./smskrupp add-member 0731234567 member1 test
    $ ./smskrupp add-member 0731234568 member2 test
    $ ./smskrupp set-sender 0731234567 test
    $ ./smskrupp list-members test

Now if you have gammu-smsd set up correctly you should be able to send a message from 0731234567 to the phone you've setup with gammu and it will deliver to all members in the group.

## Setup

Dependencies: sqlite3, gammu-smsd, python-gammu

On debian:

    # apt-get install gammu-smsd python-gammu sqlite3 libdbi-dev libsqlite3-dev libdbd-sqlite3

If you want the webapp you also need:

    # apt-get install python-bcrypt python-flask

Setting up the sqlite database:

    $ cat sql/*.sql | sqlite3 smskrupp.db && cat sql/*.sql | sqlite3 smskrupp-test.db

Create the config file:
    
    $ cp config.py.default config.py

Edit the config file so it points to the correct locations.

For gammu to work you also need a gammu-smsdrc, there is an example file in the doc/ directory.

## Tests

If your config.py points to a test-db and a test-smsdrc -- this is the default configuration -- simply run:

    $ nosetests
