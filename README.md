# pullpushlive

This is a companion project to the https://github.com/SSVC/pullpush/wiki project.

As part of the deployment process a live server needs to push a copy of a live website down to the Pullpush development server.  The data from this website is extracted and imported into the latest version of the site.  This new merged copy (called the deploy copy) is then pulled up from the dev server to the live server.

To make the deployment process as fast as possible the sending of the live copy and the pulling up of the deploy copy should be scripted.  The two scripts in this project are designed to be starter scripts which can be used on the live server.  They can be downloaded from Github and modified to match the set up of the live server.

The idea is that all parts of the deployment process can be scripted and fully tested - and that good use is made of tools such as rsync to save time.  That way it may be possible to have the whole deployment process carried out in a matter of minutes - this will allow for frequent site updates.

# Script details

## pushlivetolivecopy

Before this script is run the website should be put into a sort of 'read-only' state.  How this is carried out will vary from site to site.

Once the site has completed the merging processes should be run on the development server.

## pulldeploytolive

This script will pull the deploy (merged) copy up from the dev server to the live server.

Before this script is run website space and a database will need to have been created.  The steps needed are:

* For Drupal sites make sure Drush is available.
* Create the the account to hold the website.
* Create database and database user account.
* Create vhost.
* Set up test URL to point to the new site for testing.
* Make sure the account on the live server can log in to the dev server over SSH.

# Set up

Basically the scripts should be installed on the live server and made available to the standard accounts.

They can be pulled down from Github with:

    # cd /usr/local/share
    # git clone https://github.com/freewayprojects/pullpushlive.git

Then they can be made available to standard users with:

    # ln -s /usr/local/share/pullpushlive/pushlivetolivecopy /usr/local/bin/pushlivetolivecopy
    # ln -s /usr/local/share/pullpush/pulldeploytolive /usr/local/bin/pulldeploytolive
    # chmod 755 /usr/local/share/pullpushlive/pushlivetolivecopy
    # chmod 755 /usr/local/share/pullpush/pulldeploytolive

The idea is that to be safe the scripts are run under the local user account to limit any damage which might caused.