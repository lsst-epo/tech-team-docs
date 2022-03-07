# Legacy CIC Rubin Project Setup

**UPDATED:  ** In 2020 the Main Site repo was broken up into separate API and Client repos, and each was dockerized, effectively replacing the STRTA set up described below.  These instructions are here for prosperity, and in the case that someone needs to get the [legacy repo](https://github.com/castiron/rubin) up and running for some reason.

# STRTA Instructions

*These instructions assume you're running macOS Catalina (10.15). We have not installed Big Sur (11.0), and would expect there to be some troubleshooting and issues potentially. We have only tested on Intel macs and there will be significant blockers to installing some of the required dependencies on an Apple Silicon (m1 chip) mac.  There are some workarounds floating around but all at your own risk.*

*You likely have some of these tools mentioned in the instructions below already installed. There is no need to reinstall unless there is a version mismatch.*

*We have given you (Blake) access to the Homebrew tap that provides custom commands for STRTA (Scripts to Rule Them All, see: [https://github.blog/2015-06-30-scripts-to-rule-them-all/](https://github.blog/2015-06-30-scripts-to-rule-them-all/)). We're going to review the code and see if there's any reason why we can't make that repo public.*

1. Back up your computer

2. Install homebrew (https://brew.sh)

3. Install XCode 11.x (app store). We're running 11.7.

4. Install XCode command line tools. Version 11.5 works for us.

XCode version ≥ 12 is not compatible with php versions ≥ 7.4.X and `phpenv install 7.4.X` will fail to compile

5. Run `xcode-select --install`

6. Make sure you have a [github SSH keys](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh) in place, and [test your SSH connection to github](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/testing-your-ssh-connection)

7. Create ~/.gitconfig, add:

```bash
[url "git@github.com:"]
    insteadOf = https://github.com/
```

8. Run `brew tap castiron/bootstrap`

9. Run `brew install nodenv` to install [the node version manager](https://github.com/nodenv/nodenv)

10. Run `brew install rbenv` to install [the ruby version manager](https://github.com/rbenv/rbenv) 

It is not necessary to uninstall the system default ruby that ships on your mac, and, in fact, removing could have unintendend consequences even after installing new versions using rbenv

11. Run `brew install phpenv` to install [the php version manager](https://github.com/phpenv/phpenv)

Recommend uninstalling any existing versions of php before installing phpenv

php versions < 7.4.X are not compatible with XCode versions ≥ 12 and `phpenv install 7.4.X` will fail to compile

12. Run `brew install zlib BZip2 readline libedit libiconv tidy-html5`

On macOS 10.15.x, when installing new/additional versions of php using `phpenv`, you may need to configure that version of php with your brew installed php extensions, on install.  For instance, to install `7.4.3`, configure options like

```jsx
CONFIGURE_OPTS="--with-zlib-dir=$(brew --prefix zlib) --with-bz2=$(brew --prefix bzip2) --with-curl=$(brew --prefix curl) --with-iconv=$(brew --prefix libiconv) --with-libedit=$(brew --prefix libedit) --with-readline=$(brew --prefix readline) --with-tidy=$(brew --prefix tidy-html5) --with-pdo-pgsql" phpenv install 7.4.3
```

13. Run `brew install postgresql`

14. Run `brew install yarn` to install a [node package manager](https://classic.yarnpkg.com/en/docs) (that's not [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm))

15. Add this to ~/.zprofile if you are using [zSh](http://zsh.sourceforge.net/) (the default shell on mac starting in Catalina/10.15) or ~/.bash_profile if you are using bash

```bash
eval "$(nodenv init -)"
eval "$(rbenv init -)"
eval "$(phpenv init -)"
```

16. Verify that starting a terminal doesn't result in errors.

17. Confirm postgres is running: `brew services start postgresql`

If everything goes well, you should now be able to run `script/setup` for the cloned Rubin project.

## Finishing Up

Unless you are managing you local dns in some other manner, you will need to update `/etc/hosts` by adding

```jsx
127.0.0.1 api.rubin.lvh rubin.lvh
```

You will need to fill in some additional environmental variables at the bottom of  `api/.env` in order to access the Amazon S3 bucket (i.e. to CRUD content with any media in it).

See `script/setup` for default CMS credentials.

See README for important info regarding useful dev scripts, project architecture, browser support, etc.

Deployment

# Local Development

Run `script/server` to start the nginx magic

# Deployment

## Deployment Configuration

This project relies on Capistrano for deployment. Managing individual deploy targets requires creating and manipulating files in the `config/deploy/` directory. The name of each file in this directory corresponds with a target environment, and that environment is identified by the filename without the extension. In other words `config/deploy/staging.rb` is associated with an environment that will be referred to as "staging."

The deploy config for staging.rb is currently:

```ruby
set :stage, :staging
set :branch, ENV['REVISION'] || ENV['BRANCH_NAME'] || 'master'
set :craft_url, "https://api-rubin.cicnode.com"
server 'rubin.cicnode.com', user: fetch(:user), roles: %w(app db web)
```

Each line may potentially need to be modified when creating a new environment. The first line specifies the type of environment. If this were a production environment, this line would look like this:

```ruby
set :staging, :production
```

The second line specifies what branch to deploy by default. This can be overridden during deploy by using either of the two ENV vars present on that line. An example of this will be provided below. By default, this config will deploy the master branch.

There are two domains associated with this project. One is the Craft CMS domain, specified by `:craft_url`. The other domain, the next.js domain, is typically referenced on the 4th line as the `server`. However, the server line is really specifying the server to deploy the project to, not the  domain that the site will be accessible at publicly. So it could be, for instance, an IP address.

Note that the `:craft_url` setting is only used during the first deployment of the project in order to set up Craft.

## Deployment Commands

The most typical command to deploy the project will look like this:

`bundle exec cap staging deploy`

This instructions capistrano to deploy the project to the `staging` target.

There are some environment variables to be aware of. As mentioned above, the REVISION and BRANCH_NAME env vars can be used to specify an alternative branch to deploy. Here's an example:

`BRANCH_NAME=foo/bar bundle exec cap staging deploy`

That command will deploy branch `foo/bar` to the `staging` target.

Another environment variable to be aware of is `SKIP_NEXT`. If set to 1, next.js will not be deployed. This is useful when initially setting up the project on a new host, for example, or for deploying changes to Craft which require content changes before next.js can build the pages. In general, consideration should be given to the deployment process to avoid this type of situation, however. Here's an example of what this command would look like:

`SKIP_NEXT=1 bundle exec cap staging deploy`

## Other Capistrano Commands

### Content Sync

To sync content and files from a deploy target to your local host, overwriting your own content, execute the following command:

`bundle exec cap staging content:sync`

There are a handful of other Capistrano task that compose the current and previous deployment systems. You can locate these commands in the `config/deploy.rb` and in the rake tasks defined in `lib/capistrano/tasks/` folder. I would advise against using these on their own unless you fully understand what they do and how they will work out of sequence.

There is, for instance, a command for building the site completely statically in next.js. The command is `publish:static` and it's left here for reference but will likely not work within the context of a node app. Changes to nginx configuration would be required to serve the site statically.

# Setting Up New Environments

This will likely require further discussion. We have various tools we use, most central is Puppet, in order to quickly and reliably configure new web hosts for this and all projects. This isn't something we can hand off. If you're not planning on signing a retainer agreement with CIC, the thing to do might be to have us spin up a new environment, and snapshot it immediately in Digital Ocean so that it can be used for other environments. In theory, this would allow you to make only some small changes to nginx configuration (specifically the domains, and creating SSL certs) and have a working environment. This isn't an ideal approach in many ways, however.