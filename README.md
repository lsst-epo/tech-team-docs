# Tech Team mkdocs Test

## Dependencies

This project requires Python 3 & pip.  Check what versions of python and pip you have installed:

```
$ python --version
Python 3.8.2
$ pip --version
pip 20.0.2 from /usr/local/lib/python3.8/site-packages/pip (python 3.8)
```

### mkdocs

[mkdocs](https://www.mkdocs.org/) is a python-based static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.

### mkdocs-material

[mkdocs-material](https://squidfunk.github.io/mkdocs-material/) is a theme for mkdocs based on the [Google Material UI](https://material.io/design)  design system.  There are many [setup/configuration options](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/) for mkdocs-material.

### mkdocs-static-i18n

[mkdocs-static-i18n](https://github.com/ultrabug/mkdocs-static-i18n/) is a mkdocs plugin to easily support/manage internationalization/localization of documentation.

## Inital Set-up

```
pip install -r requirements.txt
```

or

```
pip3 install -r requirements.txt
```

## Local Dev

Local Dev Server @ `http://127.0.0.1:8000/`

```
mkdocs serve
```

Build to `sites/`:

```
mkdocs build
```

## Deploying

This project is currently a [github page](https://lsst-epo.github.io/tech-team-docs).  To deploy to github pages:

```
mkdocs gh-deploy
```