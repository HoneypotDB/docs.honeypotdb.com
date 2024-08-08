# docs.honeypotdb.com

This is our public documentation hosted at https://docs.honeypotdb.com.

These docs are written in markdown, and built using MkDocs with the Material theme.

## Running locally

To run locally create a Python 3 venv, install the requirements-small file and bring up a local mkdocs environment

Guide for Linux:

```
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements-small.txt
mkdocs serve
```