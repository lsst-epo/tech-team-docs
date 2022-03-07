# Global Dependencies

Currently, the EPO team exclusively uses Macs. Therefore all of the tools and processes described are going to be Mac specific, but many tools have direct analogs on Windows or Linux, and alternative commands, software, etc. should be readily available (we're not discussing anything too crazy here).  In 2020 Apple released a new chip architecture.  This new architecture necessitates a few important and particular workflows. When commands or technologies are specific to one architecture or the other, `Intel` will designate the legacy architecture and `M1` will designate the new architecture.

### Zsh

As of Big Sur Apple machines ship with [Zsh (as oppose to bash)](https://medium.com/@harrison.miller13_28580/bash-vs-z-shell-a-tale-of-two-command-line-shells-c65bb66e4658) as the official terminal.  This change brings a couple minor differences like editing `.zprofile` and `.zshrc` files instead of `.bashprofile` and `.bashrc` files, but otherwise is very similar.  A couple suggested conveniences to include in your `.zprofile`:

**Exports**

```bash
export EDITOR=<your fave text editor>
export VISUAL="$EDITOR"
```

**Aliases**

```bash
alias ls='ls -GFh'

alias gs='git status'
alias gf='git fetch --all'
alias gr='git log'
alias gre='git log --pretty=full'

alias arm="arch -arm64 zsh --login"
alias intel="arch -x86_64 zsh --login"
```

That first alias gussies up the standard `ls` output to be a bit more verbose and a bit more human readable.  The git aliases are all just shortcuts to typing less.  And the last 2 are only applicable if you are on a M1 mac.  These commands are useful for quickly switching your whole shell between mac architectures (switching between native M1 architecture and Intel architecture emulated with Rosetta 2)

### Oh My Zsh

One neato thing that zsh supports much better than bash is theming and plugins.  [Oh My Zsh](https://ohmyz.sh/#install) is a popular framework for managing your Zsh configurations.

**How to Install:** `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

**Aliases:** Oh My Zsh aliases [a whole bunch of helpful git shortcuts](https://kapeli.com/cheat_sheets/Oh-My-Zsh_Git.docset/Contents/Resources/Documents/index) for ya.

**Theming:** [There are a whole bunch of themes to choose from](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes), and writing your own, or extending existing themes is fairly straight-forward.  

For instance, [Agnoster](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes#agnoster) is theme attuned to working with git.  It will give you some helpful colors and iconography in your prompt that indicate what branch you are on, what kind of commands you may be performing, etc.

### Homebrew

[Homebrew](https://brew.sh/) is one of those where have you been all my life products. In their own words, it's "The missing package manager for macOS." If you've done much web development without Homebrew you have probably run into many moments where packages or shared dependencies collide, or you hunt all over your file system to delete one version of something just to confidently upgrade to another, or some things are in one user directory, or some weird bin directory, or you're always having to `sudo` install all manner of things everywhere, and on and on.  Well, for the most part Homebrew gets you around all that by being your one source of truth for everything you install on your Mac that isn't downloaded from the App Store. 

They have some pretty fantastic [documentation](https://docs.brew.sh/) and there are lots of [installation tutorials](https://www.howtogeek.com/211541/homebrew-for-os-x-easily-installs-desktop-apps-and-terminal-utilities/) out there, so we'll breeze through how to install Homebrew, callout a few commands, and then move on to some critical packages that are installed with Homebrew.  **Note:** Homebrew now prompts you to allow the Xcode Command Line Tools to be installed along with the initial Homebrew install.  We recommend you allow the Xcode Command Line Tools to be installed in this way.  However, if you don't allow, you can always install separately.

**How to Install:** `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

**How to Update Homebrew:** `brew update`

**How to Get a Package:** `brew install PACKAGE-NAME`

**How to Update a Package:** `brew upgrade PACKAGE-NAME`

**How to List Packages Installed with Homebrew:** `brew list`

**What's wrong with Homebrew?:** `brew doctor`

### Git

[Git](https://git-scm.com/) makes the world go 'round.  No really.  If you are building software (for the web or otherwise) you are going to use Git.  Even if you're not committing your work to Github, you're still using Git. So get used to it. It's great.  We're not going to spend anytime here going through the basics, instead we'll callout a couple best practices we aspire to on the EPO team.

**How to Install:** `brew install git`

**Github Authentication:**  We use Github to manage all of our repos.  We highly recommend using [two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/about-two-factor-authentication) and [connecting with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)

**How to Configure Git:** `git config` 

You can find the Git Config at `~/.gitconfig` and you can [configure a lot of things](https://git-scm.com/docs/git-config)

* [Configure a git message template](https://thoughtbot.com/blog/better-commit-messages-with-a-gitmessage-template).  This is our [commit message template](commit-message-template).  Along with the template you'll find a description of how we think it aides in writing stronger commit messages. 
* [Configure a PR message template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository).  This is our [PR message template](pr-message-template).  Along with the template you'll find a description of how we think it aides in writing stronger PR messages. 
* Pick your editor of choice (used for messages, rebases, etc.). If your editor is already aliased: `git config --global core.editor "EDITOR-ALIAS"`.  Otherwise enter the absolute path to the editor: `git config --global core.editor "PATH/TO/EDITOR"`

**How to Branch:** We juggle 3 important branches:  `prod`, `main`, and `develop`.  These branches align with the 3 development environments with Continuous Deployment:

- `prod` deploys to **Production**

- `main` deploys to **Integration**

- `develop` deploys to **Development**.  

In older projects `main` is still `master`. 

Because the **Production** and **Integration** environments are potentially "live" to the public or stakeholders you are restricted from pushing work directly to `prod` and `main`; work must be merged from a PR (more on this in [Deployment Workflows](Deployment-Workflows)).

For feature branches include the JIRA ticket key (like `EPO-1111`) in your branch name to associate your pull request with that JIRA ticket. If you know multiple people are going to be committing work to a single JIRA ticket, but on separate branches, differentiate your branch from theirs (like `YOUR-NAME/EPO-1111`)

**How to Commit:** `git commit` 

Keep it short, sweet, and to the point. This is our [commit message template](commit-message-template) (see above for guidance on implementation).  Each commit should deliver a **feature**, **chore**, or **bug fix** and a reference to the type of commit should be included at the start of the commit log line as `[F]`, `[C]`, or `[B]` respectively.  E.g. `[F] Brand new cool thing`, `[C] Trivial maintenance task`, `[B] Broken thing works better now`.

* Many commits may refer to the same JIRA ticket; no commit should refer to more than one JIRA ticket.  To associate commit to a Jira ticket include a reference to the Jira ticket key in the commit message.  We typically include this reference as a new line at the end of the commit like:
  
```
[F] Brand new cool thing
  
Summary of the coolness
  
[EPO-1111]
```

* It's the end of the day and you're not ready to push a full on commit? Commit and push your work to a branch for safe keeping anyway, but use a placeholder message `git commit -m "[WIP]"`. Later, when you finish your work, amend your work and change the message `git commit --amend`.  Note: because you already have a message you won't see your commit message template when you amend. Observing this practice ensures that even if your computer explodes during the night, at least the next morning you won't have to readdress that pesky problem from the day before.  RIP your exploded computer.

**How to Pull Requests:** You can [submit and merge pull requests from the command line](https://git-scm.com/docs/git-request-pull), but we generally work in Github to create and approve. You can also use pull request templates. This is our [Pull Request Template](PR-Message).  Include the JIRA ticket key (like `EPO-1111`) in your branch name to associate your pull request with that JIRA ticket.

**How to Rebase:** `git rebase <branch>` 

Rebasing is such an awesome thing.

* `git merge` is for squares.  It creates kinda superfluous merge messages in the log and tends to lead to more merge conflicts, and conflicts between collaborators' branches.  To avoid all this, always rebase your work on top of `develop` before submitting or merging a pull request: while on your working branch `git rebase origin/develop`
* If your project has multiple contributors, rebase your work onto`develop` after every commit to avoid any merge conflicts down the line.
* Do a set of commits in your pull request feel too granular? Do they all add up to a single feature, chore, or bug fix?  Do the commit messages in your pull request feel all wrong?  Start an [interactive rebase](https://thoughtbot.com/blog/git-interactive-rebase-squash-amend-rewriting-history): `git rebase -i HEAD~<NUMBER-OF-COMMITS-BACK>`.  Once in an interactive rebase you can combine, rewrite, or even skip commits.

**How to Cherry Pick:** `git cherry-pick <commit-id>`

Cherry picking commits off one branch and plopping them onto another has saved many a merge/rebase troubles headache.  `cherry-pick` is what's happening under the hood when rebasing (i.e. a rebase is just a collection of `cherry-picks` applied in sequence) and it's a good technique to keep in mind when git stuff goes awry.

### nodenv

[nodenv](https://github.com/nodenv/nodenv) is a [Node](https://nodejs.org/en/about/) version manager.  While EPO is in a position to dictate the Node version space across all of our products, using a version manager is still a meaningful pattern because it increases flexibility, allows for ease of experimentation, and it provides a record of the Node version at a project level.

**Install:** `brew install nodenv`

**Global Node:** `nodenv global <VERSION>` (writes version to `~/.nodenv/version`)

**Local Node:** `nodenv local <VERSION>` (creates `.node-version` file in root of your project)

**Note about M1:** Support across node dependencies across versions of node across systems/architectures is somewhat patchy.  Especially so for Apple M1 as it is still relatively new.  For this reason, you will find some repo readmes demand not only specific node versions, but also that it be explicitly installed as `M1` or `Intel`.  There is not currently a way to assert this specificity with only `nodenv` commands.  Instead, you need to spoof your desired architecture for your shell and then run your `nodenv` commands as usual.  For example:

```
$ arch -x86_64 zsh --login
$ arch
i386
$ nodenv install 12.14.0
Downloading node-v12.14.0-darwin-x64.tar.gz...
-> https://nodejs.org/dist/v12.14.0/node-v12.14.0-darwin-x64.tar.gz
Installing node-v12.14.0-darwin-x64...
Installed node-v12.14.0-darwin-x64 to /path/to/.nodenv/versions/12.14.0
```

If you installed an `Intel` version of node, it is recommended that you run all subsequent node-related commands as `Intel`.

### yarn

[yarn](https://yarnpkg.com/en/) is a node package manager.  It acts as a replacement for [npm](https://github.com/npm/cli).  `yarn` and `npm` continue to converge both in terms of functionality and support.

**How to install:** `brew install yarn`

**How to install all dependencies in `package.json` as specified in `yarn.lock`:** `yarn`

**How to add a new dependency:** `yarn add <PACKAGE-NAME>`

**How to add a new dev dependency:** `yarn add -D <PACKAGE-NAME>`

**How to run a node command specified in `package.json`:** `yarn <COMMAND-NAME>`

## Apps

### [See Useful Apps page](../useful-apps)