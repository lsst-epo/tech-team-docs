# Tech Team mkdocs Test

## Dependencies

This project requires Python 3 & pip.  Check what versions of python and pip you have installed:

```
$ python --version
Python 3.8.2
$ pip --version
pip 20.0.2 from /usr/local/lib/python3.8/site-packages/pip (python 3.8)
```

## Inital Set-up

```
pip install -r requirements.txt
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