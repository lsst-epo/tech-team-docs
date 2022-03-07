# LSST Education Hub

The home of our Formal Education Investigations, all educational support materials, and a means for our end users to manage their experiences with the work they do inside the investigations.  The ed-hub repo is primarily the CMS driving the content for both all the support material pages, as well as the Investigations themselves.  The investigations themselves do not live in the ed-hub repo.  The investigation experiences are encapsulated in a react app that uses Craft as a headless CMS: make queries and mutations on the JSON API provided by craft by way of GraphQL (and the CraftQL plugin).

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Below, I'll throw out some basic commands to get stuff going, but please refer to the linked tutorials/articles if you haven't worked with or installed these technologies before (i.e. don't learn the hard way that it's never a good idea to blindly install stuff on your machine).

#### Homebrew

We're going to be using Homebrew to install and manage various packages necessary for this project.  Luckily it's [easy to install](https://treehouse.github.io/installation-guides/mac/homebrew) and easy to use.  The [Starting from Scratch](https://github.com/lsst-epo/web-dev-docs/wiki/Starting-from-Scratch) section of our general docs more detailed/opinionated info about Homebrew, including some critical commands.

#### Git

Version control like woah. I mean if you're on this page you probably already have it, but, you know, just trying to be thorough.  It can be [installed in all the ways you'd expect](https://git-scm.com/book/en/v1/Getting-Started-Installing-Git), and, as ever, I'll reccommend installing it with homebrew.

```
brew install git
```

#### PHP 7.0+

Even if you're on a brand new shiny mac, it still only ships with PHP 5.6.  I would strongly reccommend [installing PHP using homebrew](https://medium.com/@romaninsh/install-php-7-2-xdebug-on-macos-high-sierra-with-homebrew-july-2018-d7968fe7e8b8).

```
brew install php
```

If you need to manage multiple version of PHP on your machine, homebrew offers a way to switch global versions through ["linking" and "unlinking"](https://tommcfarlin.com/running-multiple-versions-of-php-with-homebrew/).  If you need to mmore deeply manage php versions, say on a project directory by project directory basis, [phpenv seems like a good option](https://github.com/phpenv/phpenv), but its set up is beyond the scope of this readme.

#### Composer

[Composer](https://getcomposer.org/doc/00-intro.md) is npm for php plugins.  Install it with homebrew (also install php first).

```
brew install composer
```

#### PostgreSQL 10.10+

PostgreSQL is another dependency [Homebrew makes too easy to install](https://www.robinwieruch.de/postgres-sql-macos-setup). The CLI tool for postgres is `psql` and it comes with a number of handy commands you can run without having to know `SQL` ([here's a few to get you started](http://www.postgresqltutorial.com/postgresql-cheat-sheet/)).  But you can also always connect to you `db` and run `SQL` commands/queries in all the usual ways. 

```
brew install postgresql
```

If you want a GUI to CRUD your postgres, probably the most ubiquitous free option is [pgAdmin](https://www.pgadmin.org/download/), however it is neither "the best" nor "the prettiest."

#### Valet

Valet is a (somewhat Laravel focused) dev tool that runs ningx (a php server) in the background, and proxies all requests to a specified TLD to your local. This is a total nice to have and you can absolutely manage any and all local development without it.  That said, [installation is dead simple](https://laravel.com/docs/5.7/valet#installation) and has [a couple reasonable and simple ways](https://laravel.com/docs/5.7/valet#serving-sites) to run the php server.

```
composer global require laravel/valet
```

#### Craft CMS 3.3

[Craft](https://docs.craftcms.com/v3/) is a blissfully unopinionated (optionally headless) CMS written in PHP. This is not a prerequisite in the sense that it's something you need to install globally, but it's worth calling out here as this is definitely a **Craft Project**. So if this is the first time you've worked with Craft, maybe familiarize yourself with their docs and such.

### Installing

Ok. You installed and set up all of the above tools.  You're ready to get down to businesstime.

#### Get and go to the project directory

```
git clone https://github.com/lsst-epo/ed-hub.git
```

```
cd ed-hub
```

#### Install some php stuff and things

```
composer install
```

**Note**: Craft has a rich plugin marketplace, all of which are, in essence, php modules installed with composer. Currently adding plugins to staging is a one way trip from local.  That is to say, to maintain staging as a destination and not a source of truth any plugins should be installed locally, the `composer.json` and `composer.lock` should always be checked in, and then `composer install` will be automatically run on staging.  You should not install plugins on staging and then try to pull down changes.

#### Set up a local database

These instructions assume you are working on the command line, but you can perform all of these commands in pgAdmin or the like if you prefer.

**Note**: The following assumes you already set up a `your_user_name` with the right privalges to create/edit/own databases, and that your database server is running.

Connect to your database server:

```
psql -U your_user_name
```

Depending on how you set up your user you will be prompted to enter a password, or use some other stored token.

Create an empty PostgreSQL database:

```
CREATE DATABASE your_database_name WITH OWNER = your_user_name ENCODING = 'UTF8';
```

Doublecheck that you see your new database listed:

```
\l
```

If it's there, that's it for now.  This repo contains a `/config/project.yaml` that essentially acts as a schema/scaffolding for the associated database.

If it's not there?!? Oh man, I don't know man, you're on your own dude.  Just kidding.  It's always something.  Shoot [@blnkt](https://github.com/blnkt) a message and we'll figure it out together. 

Disconnect from your database server:

```
\q
```

**Note**: There is not currently an automatic mechanism to sync a remote database to your local.  If you feel like you might need some really real data to do your local development, contact [@blnkt](https://github.com/blnkt).

#### Update your Environmental Variables

The root of this project includes a `.env.example` which should cover all of the necessary environmental variables currently in use, so go ahead and start by copy/pasting this into a new file in the root of the project called `.env`.

`ENVIRONMENT="dev"` Leave this be unless your testing some environment specific behavior.

**Note**: This is not currently set up as a multi-environment project. This means each environment gets its own special, manually updated, `.env` file.

`SECURITY_KEY=""` I'm not sure how much it matters that all developers use matching `SECURITY_KEYS` but if you're doing regular development on this project, you can get it from [@blnkt](https://github.com/blnkt).  Otherwise you can [generate it manually](https://docs.craftcms.com/v3/installation.html#step-3-set-a-security-key). Either way, you need to copy/paste it into your `.env` and then set it:

```
cd ed-hub
```

```
./craft setup/security-key
```

`DB_DRIVER="pgsql"` Leave it be.

`DB_SERVER="localhost"` Leave this be unless you're developing with a remote database server, or have some interesting and awesome local setup.

`DB_USER=""` This is `your_user_name` that has access to the database you created above.

`DB_PASSWORD=""` This is the password `your_user_name` uses to access the database you created above.

`DB_DATABASE=""` This is the name of the database you created above.

`DB_SCHEMA="public"` Leave this be.

`DB_PORT="5432"` This is the port your database is at.

`DEFAULT_SITE_URL="http://domain"` Depending on whether you're proxying your localhost using Valet or something of that ilk, this could be whatever.

`ES_SITE_URL="http://domain/es/"`  But this should be `DEFAULT_SITE_URL` but just with `/es/` on the end.

#### Point your php web server at the web directory

If you're using Valet:

```
cd ed-hub/web
```

```
valet link DEFAULT_SITE_URL
```

Where `DEFAULT_SITE_URL` is the value of your `DEFAULT_SITE_URL` environmental variable, BUT without the TLD (i.e. if DEFAULT_SITE_URL is `http://blahblah.woofwoof` your valet command is `valet link blahblah`).

#### "Install Craft"

Alright.  If everything is working as it should, when you visit `http://DEFAULT_SITE_URL/admin/install` (where `DEFAULT_SITE_URL` is the value of your `DEFAULT_SITE_URL` environmental variable), you should see a button inviting you to "Install Craft."

Click that button and walk through the "Install" process.  It'll invite you to create an admin account, and ask you fill out some different setup fields.  If any of those fields are empty, it's ok for you to fill them.  If they are being prepopulated with values, **DON'T** fill them out.  Those values are getting read out of the `project.yaml` and altering them in this "Install" flow will change them in that config file, and doing so might percipitate a nasty `merge conflict` down the road for someone (maybe you). Don't forget to take note of your Craft admin credentials.  You will need this to access the Craft Control Panel.

At the end of the "Install" flow you should land on the dashboard.  Thanks to the `project.yaml` you should have the same entry types, same fields, same groups, sites, globals, plugins, etc, as your fellow developers.  If stuff feels suspiciously empty, something went wrong. But if you see stuff and things, you're golden.  Start building something rad.

If you prefer, you may step through this very same install process on the command line instead:

```
./craft install
```

If you do, please stay similarly vigilant as to not overwrite those values provided by the `project.yml` file (as noted above).

## Running the tests

This project uses [Codeception](https://codeception.com/docs/01-Introduction) for testing.  It currently only supports Functional and Unit testing. Currently this testing suite is configured to be non-destructive when it comes to its interactions with the database, however, a poorly written test could still do some damage to the database. Therefore, ideally you will run your tests on a different database than what you're developing on.  For this (and other) reasons the craft instance powering the tests uses its own `.env` located in `/tests/.env`.  It should look very similar to your primary `.env` except it'll include information about some other database.

### Break down into end to end tests

Coming soon

## Deployment

See @blnkt](https://github.com/blnkt) about setting up a remote to push to staging using git over ssh.

1. Connect to staging over ssh `ssh root@0.0.0.0` (hosted on DigitalOcean; [see their docs](https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/openssh/); you will need a private SSH key saved/whitelisted to connect to host)
2. `cd` into project directory `cd /var/www/edhub/`
3. Create DB backup and save to storage/backups `./craft backup` (see addiitonal [Craft 3 CLI commands](https://nystudio107.com/blog/exploring-the-craft-cms-3-console-command-line-interface-cli))
4. Update to desired commit
5. Restore DB from externally provided DB backup (if applicable) `rsync -avz /path/to/my/files root@0.0.0.0:/path/on/my/server`
6. Update packages `make install`
7. Sync Craft Project config `./craft project-config/sync`
8. Build frontend assets `make build-fe`
9. Check frontend and admin for any indications of failed deploy

## Built With

[Craft 3](https://docs.craftcms.com/v3/)
[CraftQL](https://github.com/markhuot/craftql)...and therefore [GraphQL](https://graphql.org/learn/)
[Codeception](https://codeception.com/docs/01-Introduction)

## Authors

* **LSST EPO Team** - [Github Organization](https://github.com/orgs/lsst-epo)

See also the list of [contributors](https://github.com/lsst-epo/ed-hub/graphs/contributors) who participated in this project.